폰트 변경

- 사용하는 스킨은 attila 스킨임. https://github.com/zutrinken/attila
- 적용시키고 보니 body의 font-family가 'Cardo', sans-serif 로 되어있음.
- Cardo 라는 폰트가 뭔진 모르겠으나 한글이 궁서체처럼 나와서 안 이쁨. 개인적으로 좋아하는 나눔고딕으로 바꾸려고 함
- 잘 보면 font-family를 정의하는 파일이 있음. style.scss에서는 정의해둔 파일을 import하는데 (@import "fonts";) 저기에 나눔고딕이라는 폰트에 대해 알려줘야 함
    - ttf파일을 추가하고 url을 정의했다.
- body 블록에서 font-family의 첫번째를 'NanumGothic'으로 바꿔준다. 

- 그리고 잘 보니 word-break가 keep-all로 되지 않아서 `할 수 있다` 같은 문장에서 윗줄에는 `있` 까지만 나오고 `다`가 아래쪽으로 내려가는 안타까운 상황도 보였다. (pic1)
- 그래서 body bloc에 word-break: keep-all; 도 같이 추가해줬다.

- grunt build 로 빌드, grunt zip 으로 zip파일을 만들고 블로그에 다시 업로드한다
- 적용된 화면을 확인(pic2) - 편안

