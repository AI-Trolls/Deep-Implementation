## Keras에서 GPU 사용해서 연산/학습하기
1. 사용 가능한 device 보는 방법
  - 방법1. tensorflow 라이브러리 사용
  ```python
  from tensorflow.python.client import device_lib
  print(device_lib.list_local_devices())
  ```
  - 방법 2. keras 라이브러리 
  ```python
  from keras import backend as K
  print(K.tensorflow_backend._get_available_gpus())
  ```
2. GPU 사용하는 방법
  - 방법 1. with문 사용
  ```python
  import keras.backend.tensorflow_backend as K
  with K.tf.device('/gpu:0'):
    # your code
  ```
  - 방법 2. multi_gpu_model 사용
  ```python
  from keras.utils.training_utils import multi_gpu_model
  model = multi_gpu_model(model, gpus=4)
  ```
3. GPU 사용량 보는 방법 (Ubuntu)
  ```bash
  nvidia-smi
  ```
