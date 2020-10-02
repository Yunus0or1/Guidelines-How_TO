
# Installation

  - Install python 3.6.2 64-bit version or Newest Version
  - Run these commands : 
    ```
    pip3 install tensorflow==1.14
    pip3 install tensorflow-gpu==1.14 (Stable but visual C++ 2015 v3 update required)
    ```
    or you can try these.
    ```
    pip3 install --upgrade tensorflow
    pip3 install --upgrade tensorflow-gpu (it will become default tensorflow)
    ```
 - Install cuda 10 
 - Download [cudNN](https://developer.nvidia.com/cudnn) from Nvidia after Login.
 - Copy contents of cuDNN 10 to C:\Program Files\NVIDIA GPU Computing Toolkit. I have used cudNN v11.
 - You might need other cudNN downloads to copy-paste dll files.
   > You may find several missing dll. Look at the missing dll versioning. Example: cudart64_101.dll is from cuda 10.1. So download that Cuda and install it. Copy Paste the file to the latest Cuda. For example copy dll files from v10.1 to v11 in **C:\Program Files\NVIDIA GPU Computing Toolkit**

>You may find several missing dll. Just find them on internet or go to C:\Program Files\NVIDIA GPU Computing Toolkit. Find the similar dll and rename it.

**This is the chart to make accurate versioning between tensorflow GPU, cuda and cudNN**

>[StackOverFlow](https://stackoverflow.com/questions/50622525/which-tensorflow-and-cuda-version-combinations-are-compatible) | 
>[TensorFlow](https://www.tensorflow.org/install/source#tested_build_configurations)


# Check TensorFlow

To check if your GPU is enlisted:

```Python
import os
os.environ['CUDA_VISIBLE_DEVICES'] = '0' # 0 = GPU use; -1 = CPU use
from tensorflow.python.client import device_lib
print(device_lib.list_local_devices())

import tensorflow as tf
print("Num GPUs Available: ", len(tf.config.experimental.list_physical_devices('GPU')))

if tf.test.gpu_device_name():
    print('GPU found')
else:
    print("No GPU found")
```
[Tutorial from Medium](https://medium.com/@liyin2015/tensorflow-cpus-and-gpus-configuration-9c223436d4ef)


# Check Keras

```Python
import os
os.environ['CUDA_VISIBLE_DEVICES'] = '0' # 0 = GPU use; -1 = CPU use

import keras
import tensorflow as tf

config = tf.compat.v1.ConfigProto( device_count = {'GPU': 1 , 'CPU': 3} )
sess = tf.compat.v1.Session(config=config)
keras.backend.set_session(sess)
```

>If you face problem with 'import keras.something' convert it to'tensorflow.python.keras.something'


# TensorFlow Version check 

```Python
import tensorflow as tf
print(tf.version.VERSION)
```







