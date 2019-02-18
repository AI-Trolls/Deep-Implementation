

## SphereFace MNIST를 나의 데이터셋으로 변경
유명한 얼굴 인식 모델인 [SphereFace](https://github.com/YunYang1994/SphereFace)의 tensorflow implementation을 활용하는 도중 문제가 발생했다.

### 데이터셋에 대한 문제

```python
from tensorflow.examples.tutorials.mnist import input_data
```

MNIST 데이터셋은 위와 같이 import한다.

```python
#batch_images, batch_labels = mnist.train.next_batch(batch_size)
batch_images, batch_labels = read_data_batch('training_data.csv')
```

내가 수정한 부분은 매우 많지만, 위 처럼 데이터세을 read하고 batch하는 방식에 대한 함수를 바꾼 것이 가장 큰 변화이다.

```
TypeError: The value of a feed cannot be a tf.Tensor object. Acceptable feed values include Python scalars, strings, lists, numpy ndarrays, or TensorHandles.
```

나타난 에러 메세지는 위와 같다.

```python
  feed_dict = {images:batch_images, labels:batch_labels}
  _, _, batch_loss, batch_acc, embeddings[i:j,:] = sess.run([train_op, add_step_op, loss, accuracy, network.embeddings], feed_dict)
```

에러가 생기는 부분은 위의 코드

### 문제 방법 찾기
#### 시도해 본 방법
1. read_data_batch가 return하는 형태 맞추기
2. placeholder의 타입 맞추기

#### 시도해보지 않은 방법
1. feed_dict 형태로 batch를 input할 때는 Tensor의 형태가 아닌 ndarray의 형태여야 한다는 것.
  - Tensor에서 ndarray로 변환하는 방법
    -  다양하게 있지만, session의 설계 방법 때문인지, 제대로 수행 안됨.
2. mnist의 클래스와 같이 데이터셋을 구축하는 것.
