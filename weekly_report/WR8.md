First, I would like to discuss the value of SSR for Ara. Admittedly, for vector processors, load-store instruction fetching and decoding have been eased by data-level parallelization. (For MatMul (D1 x D2 * D2 x D3), # vld instruction = D1*D2*D3/vl) Therefore, Applying SSR will not bring so many advantages as the scalar processor. However, another benefit of SSR is data buffering. The SSR will always load data from memory unless 1. the FIFO is full and 2. the data is exhausted. The problem with my intrinsic MatMul (link1) is that the compiler always uses the same register. For example:
1. vle v9 (a3) 
2. vfmacc v8, ft0, v9
3. vle v9, (a4). 
4. vfmacc v8, ft0, v9

The second load instruction cannot be executed even after completing the first load instruction (no structure hazard) because register v9 is used by the vfmacc instruction (data hazard). The fmatmul benchmark written by Matheus and Samuel (link2) solved this problem by:
1. use more registers (use v10 instead of v9, 3. vle v10), 
2. Manually disrupt the execution order, e.g., execute FPU instructions while also executing other load-store instructions (if possible).

It is true that these methods provide the best performance, but the program itself is complex and not programmer friendly. I think that using SSR can also solve this problem for the following reasons:
1. If SSR is enabled, the MAC instruction always receives the data from the same register (SSR) with a handshake signal; there will be no need for register renaming.
2. Since the SSR has its own address pattern and loop counter, memory accesses from the SSR are independent of the other execution units. In this case, the FPU can maintain a high utilization; delaying FPU instructions because of waiting for load instructions to complete does not happen.

Progress:
* Because the old matmul offers better performance, I rewrote kernels like matmul+transpose, matmul+bias, and matmul+bias+matadd based on the old matmul in assembly.
* I updated the Ara repo and re-ran the benchmark with the new matmul. The results show that the layernorm I spent time optimizing earlier is not a bottleneck (about less than 2% of the total execution time).

Next Week:
* Maybe I can start the third phase: optimizing from the hardware side.

link1: https://github.com/xiaorui-yin/ara/blob/0de0fa766355d8de5d3a731b5205cb5639aa3a9f/apps/utils/kernel/utils.c.bkp#L42
link2: https://github.com/xiaorui-yin/ara/blob/0de0fa766355d8de5d3a731b5205cb5639aa3a9f/apps/fmatmul/kernel/fmatmul.c#L370
