# Deep-Implementation
딥러닝 '구현'에 관련해서 흥미롭게 볼만한 것들 정리

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
  - https://github.com/hwalsuklee


# 추천 자료
- [요기](https://github.com/fchollet/keras-resources)에 중간에 가보면 재미있는 예시 몇개 있음
