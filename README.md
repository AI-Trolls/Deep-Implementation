# Deep-Implementation
딥러닝 '구현'에 관련해서 흥미롭게 볼만한 것들 정리 및 변형 예제 생성

# Contents
- tensorFlow
  - tutorial
    - [Dataset class](tensorflow_tutorial/dataset.md)
- Keras
  - tutorial
    - [Tips](keras_tutorial/keras.md)
    - [training data와 validation data를 split하는 code](keras_tutorial/csv_split_training_validation.ipynb)
    - [fcae recognition example code](keras_tutorial/face_recognition.ipynb)
  - attention
    - [Dense](keras_tutorial/attention/attention_dense.ipynb)
    - [LSTM](keras_tutorial/attention/attention_lstm.ipynb)
    - [BiGRU](keras_tutorial/attention/attention_BiGRU.ipynb)
- pyTorch
  - tutorial
    - [installation](pytorch_tutorial/installation.ipynb)
    - [pytorch_tutorial_01](pytorch_tutorial/pytorch_tutorial_01.ipynb)

# Attention Model
- Todo; 재미있는 예제 못찾음
- 강의: https://www.youtube.com/watch?v=7ivUO7ER0iE&index=7&list=PLep-kTP3NkcN43rnM4WrOYk7eXeB4s3DM 

# Style Transfer 
- 하나의 이미지 안에서 feature들 간의 상관관계를 측정하는 Gram Matrix를 정의하고
  - 두 개의 이미지(하나는 스타일이미지, 하나는 바꾸고 싶은 인풋이미지)를 넣으면
  - 각각 이미지의 Gram Matrix를 구해서 서로간의 Error가 최소화 되도록 트레이닝을 하되
  - 네트워크의 weight을 트레이닝 하는 것이아니라
  - gradient를 input 까지 전파해서 이미지 자체를 바꿔버린다!! 엄청난 발상의 전환으로 재미있는 결과를 뽑음
- 강의: https://www.youtube.com/watch?v=VC-YFRSp7lM&index=8&list=PLep-kTP3NkcN43rnM4WrOYk7eXeB4s3DM 
- 코드
  - https://github.com/lengstrom/fast-style-transfer
  - https://github.com/hwalsuklee/tensorflow-style-transfer
  - https://github.com/hwalsuklee

# Knowledge Graph
- [kegra: Deep Learning on Knowledge Graphs with Keras](https://towardsdatascience.com/kegra-deep-learning-on-knowledge-graphs-with-keras-98e340488b93)

# 추천 자료
- ([요기](https://github.com/fchollet/keras-resources))에 중간에 가보면 재미있는 예시 몇개 있음

# Face Recognition
  - [openFace](https://github.com/cmusatyalab/openface)
    - [한국 블로그 예제 자료](https://www.popit.kr/openface-exo-member-face-recognition/)
  - [shpereFace](https://github.com/wy1iu/sphereface)
    - [re-implementation of asoftmax in tensorFlow](https://github.com/pppoe/tensorflow-sphereface-asoftmax)
