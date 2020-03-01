---
layout: post
categories: dev
title: "딥러닝칼리지 cs231n HW (2017)"
date: 2017-12-15T13:01:27-05:00
share: true
---

## dlc homework #1 
- Q: from dataset.mnist import load_mnist was not working
  - NoModuleFoundError
  - A: just moved the running python file into dataset folder, and all other ones that need the import from different directory

## deep learning from scratch ch.5 code
- Q: self.layers.value(), layer['Affine1'].db or dW -- return values?
  - print them out

## dlc hw  == cs231n 16/17 spring hw 1
- git bash on windows: run ./get_datasets.sh
  - Q: error: wget: commnand not found
    - A: https://gist.github.com/evanwill/0207876c3243bbb6863e65ec5dc3f058
    - download extra modules and add .exe file into mingw64/bin folder
    - it works.


## dlc hw assignment 1 - SVM
- http://yamalab.tistory.com/40
- http://aikorea.org/cs231n/optimization-1/ + http://cs231n.github.io/linear-classify/

1. what is kernel trick? 
- http://juggernaut.tistory.com/31
- an effective way of tranforming the current dimension of data into higher-dim space, to find the clear classifiable division line or plane
- 비선형 매핑(Mapping)을 통하여 고차원으로 변환시킨 뒤 ... (생략)
- 결론적으로, 그리고 약식으로 말해서, 한 커널은 일반 점들을 내적 공간으로 포함시키는 것을 포함한다.
- youtube (20:00) 
  - kernel options: linear / radial basis function ('rbf') / polynomial/ sigmoid
  - gamma value: small gamma: less complexity, large gamma: more complexity (prob prefer small gamma)

2. 그렇게 초평면...
- 가장 효과적인 초평면을 찾아가면서 그룹간의 categorization을 할 때 발생하는 오류를 최소화해야 하는데,
이 과정에서 라그랑즈 승수법이라는 것을 사용해서 가장 적절한 변수들을 찾는다.


2. 마진을크게하자
- if there are several lines/planes/ways to divide/classify data points, the larger the margin is, the better
- 관대한 SVM을 소프트 마진 분류법: 여유변수 = 선형분류에대한제약. 여유변수가 크면 엄격하게 따진다는 뜻
- how do you maximize the margin?
  - youtube: https://www.youtube.com/watch?v=N1vOgolbjSc [Support Vector Machines: A Visual Explanation with Sample Python Code]
  - This is constrained optimization problem
    - optimization: bc we want biggest margin possible
    - constrained: the data points can't be insdie the margin
  - Solution to use: Lagrange multipliers

 4. multiple classes: comparison
 - ovo: one vs one; comparing one class at a time: less sensitive over errors
 - ovr: one vs rest
 
5. helpful links
- https://bruceoutdoors.wordpress.com/2016/05/06/cs231n-assignment-1-tutorial-q2-training-a-support-vector-machine/
- https://github.com/bruceoutdoors/CS231n/blob/master/assignment1/cs231n/classifiers/linear_svm.py
- https://github.com/aroetter/cs231n-assignment1/blob/master/cs231n/classifiers/linear_svm.py
