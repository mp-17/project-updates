Progress:
* Optimized LayerNorm execution: To calculate the normalization of the layers, we need to load the input data three times. 1. mean, 2. variance, and 3. scaling. I use an online variance calculation trick to calculate the variance and the mean together. (In calculating the variance, use the current mean) However, the accuracy loss has to be analyzed. I first fine-tuned the BERT-base model and replaced all the original LayerNorm modules in the model with my implementation, and then I compared the MCC scores of the two models. However, it seems that my implementation is incompatible with the Huggingface BERT model and scores very low, I need to investigate further.
* Optimized heads concatenation: Previously the concatenation waited until all head calculations were completed, but now it is embedded directly in the matrix calculation, just like bias/scaling.
* Corrected bias calculation: The bias value of a row is actually the same, rather than each element having a different bias value.
* Instead of generating all input and weight data randomly, I decided to use real data: Extract all data from a Huggingface transformer model and use it in simulation.

Next Week:
* Fix the hardware simulation problem, and evaluate all kernels
* Analyze the accuracy impact of new LayerNorm
