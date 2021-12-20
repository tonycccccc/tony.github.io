# FLAT DataFlow

This GitHub repo contains FLAT dataflow implementation. FLAT is a specialized algorithm designed for optimizing attention layer calculation.
The code uses Tensorflow2.0 and should all be run in colab. It relies on the Colab GPU to do the memory profiling.  

To use the code, the user only needs to run FinalDemo.ipynb!!  

# Purpose
The purpose of running FinalDemo is to find the best granularity of the model input. Function inside this notebook will return a graph plotting the peak and current memory usage under current granularity condition, as well as GPU runtime. All test statistics are stored in a separate .json file so that users can do visualization later.

# Steps
1. The first step is to retrieve the query, key, value, and bias matrix from the model input. Here we suggest using tf.io.serialize_tensor() and tf.io.write_file() for storing , and tf.io.read_file() and tf.io.parse_tensor() for reading. This seems to be the only way of saving intermediate matrix during running time of tensorflow model.  
2. The second step is to load the sequence of input matrix stored into the test notebook. We suggest storing all of them into Google Drive and read from there.  
3. It is time to test! Try different granularities on our function and find the one that works best.  
4. Visualize test result using statistics store in the .json file.  

# Notice
The priority of the granularity level is Batch > Head > Length. If the user doesn't want to use batch as the lowest granularity level, please set the input to 1. Otherwise, it will automatically select batch and not care what you type for the head and length.  

# Reference
For the behind principles, please refer to this article!
https://arxiv.org/pdf/2107.06419.pdf
