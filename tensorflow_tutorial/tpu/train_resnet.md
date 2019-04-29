ref: https://cloud.google.com/tpu/docs/tutorials/resnet

TPU가 핫한 요즘- TPU를 사용하려 해보았는데, <br/>
tnesorflow 2.0 혹은 keras 코드에 는 호환성이 좋은데, <br/>
tensorflow 1.x 코드는 좀 바꿔야할 부분이 많았다.

이 외에도 cloud를 사용해야하는 issue가 있기에, 스터디해보며 자료를 남겨본다.

# 클라우드 TPU에서 ResNet 학습하기
- 사용 모델: [Deep Residual Learning for Image Recognition](https://arxiv.org/pdf/1512.03385.pdf)
- 사용 코드: [ResNet-50 on TPU](https://github.com/tensorflow/tpu/tree/master/models/official/resnet)
- 사용 장치: Cloud TPU device 혹은 Cloud TPU Pod lice (multiple TPU devices)
- 사용 환경: Colab(https://colab.research.google.com/)

~~저같이 돈이 없으신 분은~~ Colab을 사용하셔서 튜토리얼/테스트 하시기를 추천합니다!

## Colab
- TPU 사용 셋팅 방법
  - Edit > Notebook Settings > Hardware Accelerator > select TPU
- TPU 확인 코드
    ```python
    import os
    import pprint
    import tensorflow as tf

    if 'COLAB_TPU_ADDR' not in os.environ:
      print('ERROR: Not connected to a TPU runtime; please see the first cell in this notebook for instructions!')
    else:
      tpu_address = 'grpc://' + os.environ['COLAB_TPU_ADDR']
      print ('TPU address is', tpu_address)

      with tf.Session(tpu_address) as session:
        devices = session.list_devices()

      print('TPU devices:')
      pprint.pprint(devices)
    ```
    - 잘 연결된 경우, 결과로 TPU address와 TPU devices가 나옵니다.

## Code for Run
1. 최상위 `/models` 폴더를 python path에 추가.
    ```bash
    export PYTHONPATH="$PYTHONPATH:/usr/share/tpu/models"
    ```
    - (resnet-50 model이 설치된 위치)

2. 아래의 경로로 이동합니다:
    ```bash
    cd /usr/share/tpu/models/official/resnet/
    ```
3. DATA_DIR 환경변수를 아래와 같이 설정합니다:
    ```
    gs://cloud-tpu-test-datasets/fake_imagenet
    ```
4. 학습 script를 실행합니다:
    ```bash
    python resnet_main.py \
      --tpu=${TPU_NAME} \
      --data_dir=gs://cloud-tpu-test-datasets/fake_imagenet \
      --model_dir=${STORAGE_BUCKET}/resnet \
      --param_file=configs/cloud/${ACCELERATOR_TYPE}.yaml
    ```
    > --tpu specifies the name of the Cloud TPU. Note that ctpu passes this name to the Compute Engine VM as an environment variable (TPU_NAME). <br/>
    > --data_dir specifies the Cloud Storage path for training input. <br/>
    > --model_dir specifies the directory where checkpoints and summaries are stored during model training. If the folder is missing, the program creates one. When using a Cloud TPU, the model_dir must be a Cloud Storage path (gs://...). You can reuse an existing folder to load current checkpoint data and to store additional checkpoints.<br/>
    > --param_file specifies default training values. ACCELERATOR_TYPE is the accelerator version and the number of cores you want to use, for example, v2-32 (32 cores). Refer to supported TPU versions for the supported TPU sizes.<br/>


## Cloud Storage
- 제가 생각할 때에 첫번째 issue인 것 같습니다. 구글 클라우드에 익숙하신 분이라면 쉬울 수 있지만, 제게는 cloud bucket이 익숙치 않아서...
- Cloud TPU device(혹은 Pod slice)와 cloud storage bucket은 같은 region에 속해있어야 합니다!

###  Cloud TPU provisioning tool (ctpu)
- Cloud TPU project resource를 생성하고 관리하는 툴
- 이 resource는 Virtual Machine(VM)과 (이름이 같아서 포함관계가 어색하지만)Cloud TPU resource로 구성됩니다.
- resource를 생성하기 위해서 ctpu up를 실행합니다! (윗줄은 tpu device, 아랫줄은 tpu pod)
    ```bash
    ctpu up --machine-type n1-standard-8
    ctpu up  --zone=us-central1-a --tpu-size=v2-32 --disk-size-gb=500 --machine-type n1-standard-8 --preemptible
    ```
  - 한 개 이상의 project를 가지고 있을 경우, project 이름을 명시해야한다고 합니다.

### Export the storage bucket
- 학습 중에 checkpoints를 저장하거나, log를 작성하기 위해서는 STORAGE_BUCKET 환경 변수를 설정해야합니다.
  - YOUR-BUCKET-NAME 이라는 부분을, 여러분의 Cloud Storage bucket 이름으로 채우시면 됩니다!
    ```bash
    (vm)$ export STORAGE_BUCKET=gs://YOUR-BUCKET-NAME
    ```
  
  
