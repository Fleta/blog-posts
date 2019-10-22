지난 글에서 다루지 않았던 블로그를 올리면서 했던 다른 설정들을 이번 글에서 다루고자 한다. 

Nginx 설정

블로그의 주소는 현재 `blog.yuigahama.moe`인데, 메인 도메인인 `yuigahama.moe`에도 다른 웹 서비스가 올라가 있다. ghost로 블로그를 올리면서 SSL를 사용하도록 설정했다면 생성된 ghost 폴더의 하위 경로에서 nginx 설정을 발견할 수 있다. 특별히 경로를 바꾸지 않았다면 `/system/files/${blog_domain}.conf` 파일이 그 파일이다. `location` 블록 설정은 되어 있겠지만 블로그만 먼저 세팅하고 ssl 인증서를 받은 경우 ssl_certificate 관련 설정이 안 되어있을 것이다.

```
    ssl_certificate /etc/letsencrypt/live/${blog_domain}/fullchain.pem; 
    ssl_certificate_key /etc/letsencrypt/live/${blog_domain}/privkey.pem;
    include /etc/letsencrypt/options-ssl-nginx.conf; 
    ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem; 
```

이런 설정이 있는지 확인해보자.



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

