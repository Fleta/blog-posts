---
title: 'Javadoc 작성기'
date: 2019-9-5 02:00:00
category: 'Java'
---


최근에 Jetty기반의 서버를 하나 개발하게 되었다. 릴리스를 할 수 있는 수준까지 개발이 되었고, 진척이 됨에 따라 중간중간에 주석으로만 남겨두거나 간단하게만 적었던 설명들을 Javadoc을 이용해서 구체화하게 되었다. Javadoc은 소스코드 주석을 이용해 API 문서를 만드는 유틸리티고, 지금까지도 Java 문서화하면 먼저 나오는 단어들 중 하나일만큼 유명하다. 유명하고 자주 봐서 그런지 그만큼 사용하기 편한 것 같아서 나도 이용하게 되었다. 이번 글에서는 내가 어떻게 Javadoc을 사용했는지 남겨본다.


## 1. Javadoc이 필요한가?

일단 소스코드 상으로 보는 문서가 아니라 페이지 형태로 정리된 문서는 내가 원하는 클래스를 찾기 편하게 만든다고 생각한다. JDK API reference들도 보면 javaadoc으로 만들어졌는데, 패키지와 클래스가 왼쪽 메뉴에 있다. 이를 통해서 원하는 이름의 클래스를 쉽게 찾을 수 있고, 클래스를 쉽게 찾으면 원하는 인터페이스를 찾는데 더 도움이 된다고 생각한다.

또한 소스코드 상에서도 Javadoc은 `//` 으로 적는 주석보다 낫다고 생각한다. `@link` 같은 태그들로 다른 인터페이스를 연결해두면 분석을 위해 소스를 보는 시간이 크게 줄어든다고 생각한다. 


## 2. 기본적인 사용법

문서화할 주석을 다는 경우에는 `/** */` 안에 내용이 들어가 있으면 된다. 특별한 내용을 다룰 때는 `@`로 시작하는 태그들을 사용한다. 주로 사용하는 태그는 `@link`, `@param`, `@throws` 정도이고, 그 외에도 사용되는 태그들에는 `@author`, `@deprecated`, `@since`, `{@code}` 정도가 있다. 

[Orcale에서 제공하는 Javadoc guide](https://www.oracle.com/technetwork/articles/java/index-137868.html)에는 어떻게 작성하는지 대략적인 가이드가 나와 있다. 가이드와 나의 경험을 섞어서 요약하자면 아래와 같다.

- 첫 줄에는 주석 시작을 나타내는 문자(`/**`)
- 첫 문장은 현재 작성하는 메서드에 대한 요약.
    - 메서드 요약 테이블과 인덱스에 위치됨
    - 메스드 요약 같은 경우에는 두 줄까지 나오더라.
- `{@link URL}` 형식으로 참조하게 할 링크를 명시하라는데, `${className}#${interfaceName}` 형식으로 작성하면 Javadoc을 생성했을 때 해당 인터페이스의 링크가 걸린다.
- 만약 할 말이 많아서 문단이 구분되어야 한다면 구분되는 라인에 `<p>` 태그를 넣으면 된다. newline을 넣고 싶다면 `<br>` 로 넣을 수 있다.
- 설명과 태그 사이에는 공백 라인을 하나 넣을 것
- `@` 으로 시작하는 라인이 나오면 설명 부분은 끝나게 된다고 한다. `@` 로 시작하는 라인 이후에 다시 설명 부분이 나오거나 할 수는 없다고 한다. 
- 마지막 라인은 주석이 끝났음을 나타내는 문자(`*/`)

그래서 예시를 들자면 아래와 같다.

```
/**
 * This controls certian functions.
 * Parameter argument should satisfy certain contains. See {@link SomeClass#someInterface}
 * <p>
 * Other paragraphs can also be made.
 *
 * @param   parameter   object giving something of something
 * @return              object of the result processed by the given parameter
*/


public SomeClass someMethod(SomeOhterClass parameter) {
    // do something...
    return new SomeClass().someSetter(something);
}
```

## 3. 내가 마주했던 문제들

### 3-1. 커스텀 태그

### 3-2. 인코딩