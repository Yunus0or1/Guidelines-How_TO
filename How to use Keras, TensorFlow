
############### Installation

install python 3.6.2 64-bit version or Newest Version
run this command : pip3 install --upgrade tensorflow
				 : pip3 install --upgrade tensorflow-gpu (it will become default tensorflow)	(May be visual C++ 2015 v3 update required)
install cuda 9.0.176 (9.1 is not currently stable for windows). I have installed cuda v11.
Download cudNN from Nvidia after Login.
copy contents of cuDNN 9.0 to C:\Program Files\NVIDIA GPU Computing Toolkit. Mine is cudNN v11.
You might need other cudNN downloads to copy-paste dll files.

You may find several missing dll.
Look at the versioning. Example: cudart64_101.dll is from cuda 10.1. So download that Cuda and install it. Copy Paste the file to the latest
Cuda. For example copy dll files from v10.1 to v11 in C:\Program Files\NVIDIA GPU Computing Toolkit

############### Check TensorFlow

To check if your GPU is enlisted:

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

Tutorial: https://medium.com/@liyin2015/tensorflow-cpus-and-gpus-configuration-9c223436d4ef



############### Check Keras

import os
os.environ['CUDA_VISIBLE_DEVICES'] = '0' # 0 = GPU use; -1 = CPU use

import keras
import tensorflow as tf

config = tf.compat.v1.ConfigProto( device_count = {'GPU': 1 , 'CPU': 3} )
sess = tf.compat.v1.Session(config=config)
keras.backend.set_session(sess)

















































