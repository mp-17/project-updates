Progress:
* Studied the structure of the vanilla transformer model with PyTorch implementation.
* Evaluated the parameter size and accuracy of different SoA transformer models in Huggingface. Since the parameter size of most popular models exceeds 100M, I decided to shift to smaller models that can fit IoT devices. (~600k parameters)
* Explored different improvement methods to alleviate the quadratic complexity issue of self-attention calculation, e.g., pruning the token size based on the similarity to the previous token at runtime; using kernelization trick and matrix associativity law to reduce the complexity from N^2 to N.

Next Week:
* Train the linear transformer model on the Google Speech Commands dataset and compare the results with other models.
* Meanwhile study the SoA ML accelerator design.