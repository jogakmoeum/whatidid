# XAMPP & 그누보드 세팅

로컬세팅을 저주한다.
진짜 너무 힘들었다.
깔려있던 XAMPP는 phpmyadmin이 접속되지 않았다. 참고로 나는 백엔드 지식이 전무하다. phpmyadmin과 mysql이 무슨 차이가 있는지도 모른다. 
에러메시지의 대부분은 user 'root'@'localhost' (using password NO) (using password YES) 둘 다 나왔다. 
구글링해보니 커맨드라인을 사용하여 mysql에 접속해서 grant를 바꿔서 접속 후 root 계정의 비밀번호를 NULL로 설정하고 net stop MySql80 명령어로 mysql을 껐다 켜고... 
근데 저거는 완전히 다른 문제 같았다. (해결되진 않았다. 기껏 초기화 후 비밀번호를 새로 세팅해도 다시 커맨드라인을 실행해 musql -u root -p 로 접근하면 접근이 안된다.)

xampp나 라라곤 같은 건 로컬에 php 개발 환경을 세팅하기 위한 묶음 프로그램인데 내 컴퓨터에 깔려있는 mysql이랑은 무슨 상관이지? 

xampp로 phpmyadmin에 접속할 수가 없어서 지우고 라라곤으로 세팅을 하려고 했는데 역시 얘도 phpmyadmin 접속이 안되었다. 
한참 구글링을 하다가 이 영상을 보고 그누보드 세팅을 끝냈다. 결국 다시 xampp로 세팅 완료.
https://www.youtube.com/watch?v=xqx5nuo18n0

처음에 xampp로 mysql 실행이 안되었다.
작업관리자에 들어가 mysql을 모두 강제 종료하고 다시 시작하니 작동됐다.
그누보드 세팅을 하면서 mysql 정보 입력하는 부분부터 막혔는데 영상 후반부 보고 따라하니 됐다.
그누보드는 보안상 **root user로 접근이 안되게 막아놨기 때문에!!!** root로 로그인이 안되었던 모양.
이를 알았어도? 새로 user 생성하고 권한 주는 일을 커맨드라인으로 했다면 분명히 또 뭔가 에러가 생겼겠지.
역시 GUI 만세다.

```
HOST: localhost
User: phpmyadmin에서 새로 추가
Password: user 추가하면서 만든 비밀번호
DB: phpmyadmin에서 새로 추가
```

DB 추가
phpmyadmin > new > 새 데이터베이스만들기에 DB명 입력

User 추가
새로 만든 DB누르고 SQL 클릭 > CREATE user '만들유저명'@'localhost' IDENTIFIED by '만들비밀번호';
아래 실행 누르기

권한 부여 (*모든 권한이란 뜻)
같은 곳에서 GRANT ALL PRIVILEGES on 아까만든유저명.* to '아까만든유저명'@'localhost';
아래 실행 누르기
이후 mysql > 구조에 보면 user table에 아까 만든 유저명이 나와있으면 성공.

그누보드 설치페이지 가서 위의 항목을 채워주면 된다.
최고관리자 아이디랑 비번은 알아서 만들면 됨.
