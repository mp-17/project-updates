Progress:

* Studied the Snitch core, 1. stream semantic register SSR (use special registers for memory access), 2. freq instruction (repeat and issue floating-point instructions). I think these two techniques can also be applied to Ara.
* Finished the hardware simulation of transformer kernels. Because I wrote the program with rvv-intrinsic, the performance is not comparable to the deep-optimized assembly implementation. The main issue is that in my program, there are many false data dependencies that can be resolved by register renaming (or by the SSR).
* Analyzed the accuracy impact of new layernorm. I tried another two methods: 1. replace the layer in the pretrained model and fine-tune this new model. 2. Write the model layer by layer, one with the new layernorm, the other with the standard version, then train both models on the same dataset. All results show that the new layernorm has a huge accuracy loss. (Will follow up later if layernorm is a bottleneck)


Next Week:

* Develop a plan to optimize Ara based on simulation results (need to discuss with my supervisors).
* If possible, further optimize the transformer program.
