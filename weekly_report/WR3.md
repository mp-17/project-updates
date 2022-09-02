Progress:
* Reworked the data flow of transformer computation: input/output shape, typical size ranges (in Byte) for each kernel, and the corresponding operators and computation complexity for Ara.
* Organized all literature, including transformer models and transformer accelerator designs.
* Read some accelerator designs: 1. CIM-based with configurable pipeline/parallel modes. 2. Hierarchical 2D-mesh NOC and compressed sparse column(CSC) format. 3. Fully-quantized model (all weights, activations, softmax, LayerNorm are quantized with 3% accuracy loss)
* Studied a bit of rvv-intrinsic to prepare for vector processor programming
 
Next Week:
* Implement matrix multiplication of arbitrary shapes without reductions (the example in rvv-intrinsic uses reduction)

1. A 28nm 15.59µJ/Token Full-Digital Bitline-Transpose CIM-Based Sparse Transformer Accelerator with Pipeline/Parallel Reconfigurable Modes
2. Eyeriss v2: A Flexible Accelerator for Emerging Deep Neural Networks on Mobile Devices
3. Hardware Acceleration of Fully Quantized BERT for Efficient Natural Language Processing
