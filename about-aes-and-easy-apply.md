---
title: '암호화에 대한 기본적인 이해 및 간단한 적용기'
date: 2019-12-01 20:30:00
category: 'Tech'
---

## 서론

근래 어떤 서비스를 구현하는 과정에서 요청의 유효성을 판단할 용도인 키의 처리를 위해 암호화를 고민하게 되었다. 그래서 이번 글에서는 암호화 알고리즘 적용 과정에서 나왔던 질문에 대한 내 나름대로의 정리를 남겨보고자 한다.

## 1. Hash

> 해시 함수(hash function)는 임의의 길이의 데이터를 고정된 길이의 데이터로 매핑하는 함수이다. 해시 함수에 의해 얻어지는 값은 해시 값, 해시 코드, 해시 체크섬 
또는 간단하게 해시라고 한다. 

https://ko.wikipedia.org/wiki/%ED%95%B4%EC%8B%9C_%ED%95%A8%EC%88%98 에 나온 해시 함수에 대한 정의이다. 

정의에도 나와 있듯이 hash는 길이가 다양한 데이터를 고정된 길이의 데이터로 변환하는데, 그렇다보니 Digest의 개수보다 key값이 더 많을 수 밖에 없다. 서로 다른 key를 가지고 hashing해도 같은 값이 나오는 경우가 있을 수 있다. 이를 Hash collision이라고 부른다. 나는 Hash collision이 없는 hash function은 없는 것으로 알고 있다. 디디클레의 원리(비둘기집의 원리)를 생각하면 된다.

또한 Hash function을 통해 생성된 Digest로는 원본을 구할수가 없어야 한다. 그래서 Hash function 자체는 암호화를 할 때 이용할 수 있지만 암호화/복호화를 같이 할 수 있게 만들어진 함수가 아니다. 

Hash algorithm의 종류는 대표적으로 SHA(Secure Hash Algorithm), MD5 (Message Digest) 정도가 있다. 커밋에 붙어있는 해쉬라던가 소프트웨어가 릴리스 될 때 나오는 checksum 등에서 그 예를 찾아볼 수 있다.

## 2. Hash의 단점 및 보완

Hash에는 널리 알려진 단점이 존재한다. Hash collision이 발생하기 때문에 Hash value가 중복되는 입력값을 찾기만 하면 입력값이 같다고 속일 수 있다. Birthday paradox와 접목되면 일부 Algorithm(대표적으로 MD5)에서는 아주 빠른 속도로 중복되는 Hash value를 찾을 수 있게 되는데, 이를 Birthday attack이라고 한다. Hash function자체가 아주 빠른 속도를 가지고 있기 때문에 공격자들이 아주 빠르게 임의의 문자열의 Digest와 해킹할 대상의 Digest를 비교할 수 있다. 

이를 보완하기 위해 원문에 임이의 문자열을 붙여서 Hash function을 거치도록 만들 수 있다. 이를 Salting이라고 하고 이 때 붙이는 문자열을 Salt라고 한다. 이 방법을 사용하면 공격자가 Digest를 알아내더라도 Salt와 함께 확인을 하게 되므로 공격자가 Salt까지 찾아야 해서 공격 난이도가 상승한다. [Naver D2의 안전한 패스워드 저장](https://d2.naver.com/helloworld/318732) 글에서는 모든 패스워드가 고유의 Salt를 갖고 Salt의 길이가 32바이트 이상이어야 Salt와 Digest를 추측하기가 어렵다고 얘기하고 있다. 

Key stretching을 통해서 Hash function의 속도와 관련된 단점을 보완할 수 있다. Hash function의 수행을 여러번 반복하는 방식이다. 원문을 가지고 Hash function을 통해 Digest를 만들고, 생성된 Digest를 가지고 또 다시 hash function을 거쳐 Digest를 만들고.. 이를 반복하여 하나의 Digest를 생성할 때 어느정도 이상의 시간이 소요되도록 만든다. Rainbow table을 활용한 rainbow attack및 brute force attack으로 패스워드를 추측하기 힘들게 만든다. 마찬가지로 [위에서 언급한 Naver D2의 포스팅](https://d2.naver.com/helloworld/318732) 에 따르면 Key stretching을 적용하면 동일한 장비에서 비교할 수 있는 Digest 수를 격감시켜준다고 한다. 

Adaptive Key Derivation Function은 Digest 생성 시 Salting과 Key stretching을 반복하고 Salt와 password 외에도 입력값을 더 받아서 공격자가 Digest를 유추하기 더 힘들도록 하는 방법이다. PBKDF2, bcrypt, scrypt등의 방식이 있다고 한다. ([참고](https://d2.naver.com/helloworld/318732)) [Java의 PBEKeySpec](https://docs.oracle.com/javase/8/docs/api/javax/crypto/spec/PBEKeySpec.html)를 사용하면 PBKDF2를 쉽게 적용할 수 있다.