---
title: "cs231n.github.io translation"
date: 2018-04-17 08:26:28 -0400
categories:
  - Deep Learning
tags: 
  - deep learning
  - cs231n
  - 
---


> Translating http://cs231n.github.io/convolutional-networks/ to Korean 스탠포드강의노트 한국어번역중

# Convolutional Neural Networks (CNNs/ConvNets)

CNN은 우리가 이전 장에서 본 일반적인 뉴럴 네트워크와 흡사하다. CNN은 학습하며 업데이트 되는 편향치(bias)와 가중치(weight)를 가진 뉴런으로 구성되어 있다. 

각 뉴런은 몇가지의 인풋을 받은 후, 행렬의 내적(dot product)를 수행하고, 원한다면 non-linearity를 취해줄 수 있다. 이 뉴런들로 큰 하나의 네트워크를 만든다 할지라도, 네트워크는 여전히 하나의(single) 미분가능한 스코어 함수이다: 한쪽은 원본 이미지 픽셀, 다른쪽은 클래스 스코어. 더불어, CNN에서도 마지막 레이어 (fc layer)에 손실 함수 (svm, softmax 등)를 적용한다. 일반적인 뉴럴 네트워크에 썼던 팁/트릭/기법들을 거의 그대로 적용할 수 있다고 생각하면 된다. 

그럼 뭐가 다른걸까? ConvNet 구조에서는 한가지 확실한 가정을 해두고 가야한다. "인풋은 이미지이다. 그리고 우리는 그 이미지들의 특정 속성들을 구조로 인코딩할 수 있어야 한다." 이게 가능해야지 우리가 forward function 을 더 효율적으로 실행할 수 있고, 네트워크의 수많은 파라미터를 확 줄일 수 있다. 

## 구조 훑어보기

#### _일반적인 뉴럴 넷 (신경망)을 기억해보자._
우리가 이전 장에서 보았던 것처럼, 뉴럴 네트워크는 벡터 하나를 인풋으로 받고, 그것을 여러 hidden 레이어들에 통과시켜서 변형한다. 각 hidden 레이어는 여러 뉴런들의 집합으로 구성되어 있다. 이 때 이 hidden 레이어의 뉴런 하나하나는 그 전 레이어의 뉴런들에 모두 빠짐없이 연결되어 있다. 그리고 같은 레이어 안에 있는 뉴런들끼리는 전혀 연결되어 있지 않다. 마지막 fully-connected 레이어는 'output layer' (결과값 레이어)로 불리며, 분류 문제(classification)에서는 이 최종 레이어가 클래스 스코어를 나타낸다. 

일반적인 뉴럴 넷은 큰 이미지 전체 사이즈로 잘 확장할 수가 없다. CIFAR-10에서 이미지들은 32x32x3 (32폭, 32높이, 3 칼라 채널)사이즈 정도 밖에 안된다. 그래서 첫 hidden 레이어에 있는 한개의 뉴런 (fully-connected neuron: 아까 위에서 뉴런은 그 전 애들과 다 연결되어 있다고 했으니까)은 32x32x3 = 3072 개의 가중치를 갖는다. 이 정도면 감당할 수 있을 것처럼 보이는가? 하지만 이런 fully-connected 구조(폭x높이x칼라 다 곱하고 뉴런끼리 다 이어주는 구조...)는 더 큰 이미지 사이즈에는 적용할 수가 없다. 예를 들어, 좀 더 흔히 사용되는 이미지 사이즈는 더 클 것이고, 200x200x3이라고 가정해보자. 그렇다면 200x200x3 = 120,000개의 가중치를 갖는 뉴런이 생기고, 그러한 뉴런들이 모인다면 순식간에 파라미터 개수는 불어날 것이다. 즉, 이러한 full connectivity 는 소모적이며, 수많은 파라미터는 멀지않아 오버피팅을 자초할 것이다.

#### _3차원 볼륨의 뉴런들_

CNN은 _인풋이 이미지로 이루어져 있고 이미지들은 나름 합리적으로 구조를 이루고 있다_ 는 점을 유리하게 이용한다. 일반적인 뉴럴 네트워크와 다르게, ConvNet의 뉴런들은 3차원에 배열되어 있다: 폭, 넓이, 깊이 (여기서 깊이는 활성 volume의 3번째 차원이며, 전체 신경망의 깊이/네트워크의 전체 레이어 개수가 아니다). 예를 들어, CIFAR-10에서 구해오는 인풋 이미지들은 **input volume of activation** 이며, volume은 32x32x3 의 차원을 가지고 있다. 잠시 후에 같이 보겟지만, 레이어의 뉴런들은 이전 레이어에 부분적으로만 연결될 것이다. 그전처럼 fully-connected 되는 것이 아니라. 나아가, CIFAR-10 
을 인풋으로 돌린 네트워크의 마지막 최종 레이어는 1x1x10 차원을 가지게 된다. 왜냐하면 ConvNet 구조의 끝에서는 이미지 통짜 하나를 스코어 클래스를 나타내는 벡터 하나로 줄여버리기 때문이다. 이 때 이 단일 벡터는 depth 차원을 따라서 배열되어 있는 형태이다. (depth 차원의 사이즈를 따른다는 의미로 해석하면 될 것 같다.)

[이미지]

좌: 일반적인 3층의 신경망 구조. 
우: ConvNet 는 자기 뉴런들을 3차원으로 배열한다 (폭, 넓이, 깊이). ConvNet의 각 레이어는 3D 인풋 볼륨을 뉴런들이  활성화된 3D 아웃풋 볼륨으로 바꿔준다. 이 예시에서, 빨강 인풋 레이어가 이미지이고, 빨강의 폭과 넓이는 이미지의 사이즈이다. 그리고 깊이는 빨, 초, 파 칼라 채널이다. 

> ConvNet은 레이어로 이루어져 있다. 각 레이어는 간단한 API이다. 3차원 인풋을 3차원 아웃풋으로 바꿔준다. 파라미터를 가지고 있을 수도, 아닐 수도 있는, 몇몇 미분 가능한 함수를 이용해서.

## Layers used to build ConvNets ConvNets 만드는 데 필요한 레이어들


### Pooling Layer

### Normalization Layer

### Fully-connected layer

### Converting FC layers to CONV layers

## ConvNet Architectures

### Layer Patterns

### Layer Sizing Patterns

### Case Studies

### Computational Considerations

## Additional Resources
