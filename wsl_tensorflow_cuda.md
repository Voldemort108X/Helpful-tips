# How to install tensorflow with GPU in WSL (currently only support 1.15)
1. Check https://docs.microsoft.com/en-us/windows/ai/directml/gpu-tensorflow-wsl. Get ready the NVIDIA driver, anaconda(miniconda) and WSL 2(if not yet installed).
2. Set up virtual environment 
```
conda create --name directml python=3.6 

conda activate directml
```
3. Set up tensorflow-directml
```
pip install tensorflow-directml
```
4. Import tensorflow in a slightly different way
```
import tensorflow.compat.v1 as tf 

tf.enable_eager_execution(tf.ConfigProto(log_device_placement=True)) 

print(tf.add([1.0, 2.0], [3.0, 4.0]))
```
5. Test whether GPU is good to go
```
print(tf.test.is_gpu_available())
```

# if not doing it with directml, the following error might occur 
Could not load dynamic library 'libcudnn.so.8'; dlerror: libcudnn.so.8: cannot open shared object file: No such file or directory
