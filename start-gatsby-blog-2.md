---
title: 'Gatsby(개츠비) 블로그 시작하기 2 - 세팅 및 배포'
date: 2019-11-21 10:37:00
category: 'Tech'
---

이전 글에서는 Gatsby가 무엇인지 아주 대충 알아봤다. 이번 블로그에서는 내가 이 블로그를 어떻게 세팅했는지 기록한다.


---


## 1. 개발환경 세팅

Gatsby 템플릿을 하나 사용한다. 나는 [gatsby-starter-bee](https://github.com/JaeYeopHan/gatsby-starter-bee) 템플릿을 사용했다. 포크해서 따로 repository를 관리하고 있다. fork한 뒤에는 아래처럼 개발환경을 세팅할 수 있다.

```
npx gatsby new ${directory_name} ${repo_link}

cd ${directory_name}
yarn start
```

yarn을 사용할지 npm을 사용할 지는 `gatsby new` 진행 중에 물어보니 선택할 수 있다.

## 2. 개인정보(?) 수정

- `gatsby-meta-config.js` 파일에서 내 정보를 수정할 수 있다. title, description, author, introduction 등 블로그 전반에 대한 정보를 수정할 수 있다. 나는 comment로 utterances를 사용하고 있는데, utterance같은 경우 app 설치가 필요하다. https://utteranc.es/ 를 참고하자.

- `package.json`에서 일부 항목을 수정할 수 있다.

- `/content/assets` 에 있는 프로필 사진 및 favicon 사진을 수정할 수 있다. favicon 파일 이름을 felog가 아닌 다른 이름으로 하고 싶다면 `gatsby-meta-config.js` 에서 `icon` 항목의 내용을 수정하자.

- `/static` 에서 favicon과 robots.txt를 수정할 수 있다. 

- author name을 눌렀을 때 연결되는 resume page를 수정하고 싶다면 `/content/__about` 에 있는 resume를 수정하자. `resume-en.md`는 기본적으로 있어야 하는 것으로 보인다. 싫다면 `/src/pages/about.js` 의 line 10~12를 수정하는 것으로 변경할 수 있어 보인다. (아직 안 만져봄)

## 3. 배포

### 1. AWS Amplify + AWS Route 53

### 2. Netlify