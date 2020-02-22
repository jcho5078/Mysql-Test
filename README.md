# MySQL 실행 과정

mysql서버를 실행해야 접속 가능.<br>
서버안 켜놓으면 백날 로그인 하려해도 로그인 안됨.<br>
<hr>
설치파일을 통하여 설치를 하였으면<br>
제어판-관리도구-서비스 에서 Mysql 실행 --하는 방법이 있으나, 나같이 zip파일을 풀어 설치한 경우엔
<hr>
<div>
서버 강제 실행방법. 관리자권한 cmd 후, 해당 mysql 설치 위치의 bin 파일 위치로 가서<br>
mysqld --console --explicit_defaults_for_timestamp --skip-grant-tables &<br>
실행 하면 서버 실행 완료.<br>
</div>
출처: https://shxrecord.tistory.com/90 [첫 발]<br>
<hr>
서버 실행후, 다른 명령 프롬폼트 관리자 권한으로 실행 후, 로그인.<br>
설치 폴더의 bin 폴더에서 mysql -u root -p 입력. (작성자는 계정 이름 root으로 설정함.)<br>
패스워드는 1234로 설정함.<br>
<hr>
<div>
<h1>이클립스와 mysql의 connect 테스트에서 error가 발생할 경우!</h1><br> 
  <p>1.설정한 DB와 url 이름 불일치 한 경우. ==> 이름 동일하게 고치기. (show databases; 로 현재 존재하는 DB목록 확인.)</p>
  <p>2.mysql connector 버전 이클립스에서 지원하는 버전으로 다운로드. ==> 현 5.1버전 까지.</p>
  <p>3.time zone 에러 발생한 경우. set time_zone='Asia/Seoul'; 실행.</p>
  <p>==> set time_zone='Asia/Seoul'; 실행</p>
  <p>만약 <h4>ERROR 1298 (HY000): Unknown or incorrect time zone: 'Asia/Seoul'</h4>가 뜬다면 아래 방법 시도.</p>
  <p>   ==> https://dev.mysql.com/downloads/timezones.html 에서 버전에 맞게 sql파일 다운로드.(윈도우 유저는 Non Posix)</p>
  <p>약 47000줄의 sql 구문 실행 (use mysql 명령 적용.- mysql 이란 이름의 초기 DB에서만 적용됨.)</p>
  <p>실행 후 <h5>select b.name, a.time_zone_id<br>
	from mysql.time_zone a, mysql.time_zone_name b<br>
    where a.time_zone_id = b.time_zone_id and b.name like '%Seoul';<br></h5> 실행. 오류 안나고 정상출력되면 성공.</p>
    <p>그 다음 my.ini 파일확인.</p>
    <p>(my.ini파일은 최신버전의 mysql엔 없다. 그런데 이걸 쓰는건 이 빌어먹을 time_zone 오류를 고치기 위해서다ㅠ.) </p>
    <p>https://to-dy.tistory.com/29 여기서 my.ini파일 만들기</p>
    <hr>
<p>
  <h2>my.ini파일 명을 이렇게  바꾸자.</h2>
  [mysqld]<br>
basedir=C:\Users\jcho5\Downloads\mysql-5.7.23-winx64\mysql-5.7.23-winx64\<br>
datadir=C:\Users\jcho5\Downloads\mysql-5.7.23-winx64\mysql-5.7.23-winx64\data\<br>
port=3306<br>
<h4>//여기 mysqld구간은 내 mysql 설치 위치임. 위 링크보고 자신 설치위치에 맞게 제대로 만들어야 함.</h4>
[client]<br>
default-character-set = utf8<br>
 
[mysqld]<br>
character-set-client-handshake=FALSE<br>
init_connect=&quot;SET collation_connection = utf8_general_ci&quot;<br>
init_connect=&quot;SET NAMES utf8&quot;<br>
character-set-server = utf8<br>
collation-server = utf8_general_ci<br>
 
[mysqldump]<br>
default-character-set = utf8<br>
 
[mysql]<br>
default-character-set = utf8<br>
[mysqld_safe]<br>
timezone=UTC<br>
default-time-zone=Asia/Seoul<br>
<h5>이렇게하면 utf-8 깨짐도 고칠 수 있고 일석이조. 위 default-time-zone=Asia/Seoul이건 없어도 될듯. 아래 명령어로 값을 바꾸자.</h5><br>
</p>
<p>
  만들었으면 SELECT @@global.time_zone, @@session.time_zone; 실행 해봄.<br>
<img src="https://user-images.githubusercontent.com/60742556/75094333-794d7f00-55cd-11ea-80f0-fdb203cdee6f.PNG"><br>
  @@global.time_zone값과  @@session.time_zone값이 빌어먹을 SYSTEM 으로 나와있다면, 
  set time_zone='Asia/Seoul';<br> 과 set @@global.time_zone='Asia/Seoul';<br> 실행.
	<img src="https://user-images.githubusercontent.com/60742556/75094451-8e76dd80-55ce-11ea-8002-ff54b677cea5.PNG"><br>
	<img src="https://user-images.githubusercontent.com/60742556/75094335-79e61580-55cd-11ea-81e8-27aeee6df01b.PNG"><br>
	<img src="https://user-images.githubusercontent.com/60742556/75094337-7a7eac00-55cd-11ea-8bda-e981e3120306.PNG"><br>
  명령어 전부 실행 완료 했다면, @@global.time_zone값과  @@session.time_zone값이 Asia/Seoul로 바뀐 것을 확인 할 수 있을 것 이다. 오류 해결 완료!<br>
	<img src="https://user-images.githubusercontent.com/60742556/75094338-7b174280-55cd-11ea-98b9-899d153e90c8.PNG">

</p>
</div>
