# MySQL 실행 과정

mysql서버를 실행해야 접속 가능.
서버안 켜놓으면 백날 로그인 하려해도 로그인 안됨.

설치파일을 통하여 설치를 하였으면
제어판-관리도구-서비스 에서 Mysql 실행 --하는 방법이 있으나, 나같이 zip파일을 풀어 설치한 경우엔

서버 강제 실행방법. 관리자권한 cmd 후, 해당 mysql 설치 위치의 bin 파일 위치로 가서
mysqld --console --explicit_defaults_for_timestamp --skip-grant-tables &
실행 하면 서버 실행 완료.
출처: https://shxrecord.tistory.com/90 [첫 발]

서버 실행후, 다른 명령 프롬폼트 관리자 권한으로 실행 후, 로그인.
설치 폴더의 bin 폴더에서 mysql -u root -p 입력. (작성자는 계정 이름 root으로 설정함.)
패스워드는 1234로 설정함. //2020-02-21
