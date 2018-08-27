기본적으로 ssl 을 confluence에서 지원하지 않는다.
confluence나 jira는 tomcat 위에서 돌아가기 때문에
tomcat을 ssl 설정하면 자연습럽게 confluence도 ssl 위에서 동작한다.

최근 confluence 에서 모바일 앱을 내놓았는데 이게 ssl이 동작하지 않으면 연결이 되지 않는다.

그렇다고 개인 confluence ssl을 위해서 인증서를 구해 할 수동 없는 노릇이다.
그래서 찾아낸 것이 letsencrypt 인증서다.
90일 마다 갱신해줘야 하지만 크게 불편한 작업은 아니다.

하지만 letsencrypt 인증을 위해서는 개인 도메인이 있어야 하는데

집에서 서버를 구동하는 입장에서는 유동IP를 어떻게 개인 도메인에 연결하는지가 문제가 된다.

기존에 iptime의 ddns 서비스를 통해서 ip를 dns 맵핑을 시켰다.

username.iptime.org 도메인으로 집의 PC들에 붙을 수가 있다.

그런데 iptime.org는 letsencrypt 에서 인증을 허용하지 않는다.

그래서 개인 도메인을 구입했다. www.username.com (가비아)

가비아의 도메인 서비스 중에 conf.username.com 을 username.iptime.org 로 연동 시켜주는 기능이있다.

iptime의 ddns의 경우 cname 서비스를 받을 수 있게 되어서
가비아에서 cname, conf, username.iptime.org. 를 등록하게 되면

conf.username.com 를 호출하면 집의 PC 접속을 할 수 있게 된다.

이 상태에서 letsencrypt 로 인증을 받으면 정상적으로 통과가 된다.
* letsencrypt에서 인증 받을때 중요한 팁이 인증포트가 80 이라는 점이다.
* 기존에 80포트를 사용하고 있으면 중지한 뒤에 진행해야하고 iptime 관리자에서 포트 포워딩을 시켜주어야한다.

인증서가 발급되면 해당 인증서를 tomcat에서 적용하는 방식을 이용해서 적용하면 된다.

마지막으로 앱에서 접속 확인을 해보면 성공~

약 1일의 설정 시간이 걸린듯 하다.

letsencrypt 의 파일을 p12로 변환하는 명령
```
openssl pkcs12 -export -out certificate.p12 -inkey /etc/letsencrypt/live/.org/privkey.pem -in /etc/letsencrypt/live/.org/cert.pem -certfile /etc/letsencrypt/live/.org/chain.pem
```