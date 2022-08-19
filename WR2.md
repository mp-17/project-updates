Progress:
* Summarized the execution of different transformer operations in Ara and each sublayer's data flow and dimensionality.
* Studied the application of transformers in computer vision. ViTPose shows that a plain transformer model can also achieve SoA performance. But transformers usually have a larger parameter size compared to CNNs. To reduce the size, MobileViT combines CNN and transformer, in which CNN extracts local features and feeds it to the transformer for global features extraction.
* Studied Nvidia's transformer accelerator design. Some highlights are: 1) quantize data precision per vector to 4-bit. 2) replace softmax with base 2 exponent. 3) 95.6 TOPS/W in 5nm tech.

Next Week:
* Continue the study of transformer accelerator designs
* Start to implement transformer with bare-metal programming
