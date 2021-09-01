# setting

## MySQL Setting

## mariadb 설치 및 설정

```text
[windows OS]
- scoop 패키지 관리자를 이용하여 mariadb 설치
scoop install mariadb

- 서비스에 등록 
  - mysqld --install "서비스명"
mysqld --install "mariadb"

- 서비스 시작 
  - net start 서비스명
net start mariadb    (windows)

- 서비스 종료
  - net stop 서비스명
net stop mariadb
```

```text
[mac]
- mariadb 설치
brew install mariadb

- mariadb 실행
brew services start mariadb
brew services stop mariadb
또는
mysql.server start
mysql.server stop
```

```text
[linux]
- mariadb 설치
sudo apt update
sudo apt install mariadb-server
sudo systemctl status mariadb
mysql -V

- mariadb 설치 후 root 암호 변경
sudo mysql_secure_installation

- mariadb 실행
service mariadb start
service mariadb stop
service mariadb status
```

## mysql 서버에 접속하기

로컬 MySQL 서버에 접속

```text
mysql -u root -p
Enter password: 암호입력
```

원격 MySQL 서버에 접속

```text
mysql -h 서버주소 -u root -p
Enter password: 암호입력
```

## mysql root 암호 변경

```text
alter user 'root'@'localhost' identified by '1111';
```

## MySQL 사용자 추가

```text
CREATE USER '사용자아이디'@'서버주소' IDENTIFIED BY '암호';
```

* 로컬에서만 접속할 수 있는 사용자를 만들기:

  ```text
  CREATE USER 'study'@'localhost' IDENTIFIED BY '1111';
  ```

  =&gt; 이 경우 stidu 사용자는 오직 로컬\(서버를 실행하는 컴퓨터\)에서만 접속 가능한다. =&gt; 다른 컴퓨터에서 실행하는 MySQL 서버에 접속할 수 없다는 것을 의미한다.

* 원격에서만 접속할 수 있는 사용자를 만들기:

  ```text
  CREATE USER 'study'@'%' IDENTIFIED BY '1111';
  ```

  =&gt; 이 경우 study 사용자는 원력에서만 접속 가능하다.

## MySQL 사용자 목록 조회

> select user, host from 데이터베이스명.테이블명;
>
> ```text
> select user, host from mysql.user;
> ```
>
> ## MySQL 데이터베이스 생성
>
> mariadb에서는 default 키워드를 사용하지 않는다.
>
> ```text
> CREATE DATABASE 데이터베이스명
> CHARACTER SET utf8
> COLLATE utf8_general_ci;
> ```
>
> ```text
> CREATE DATABASE studydb
> CHARACTER SET utf8
> COLLATE utf8_general_ci;
> ```

## MySQL 사용자에게 데이터베이스 사용 권한 부여

GRANT ALL ON 데이터베이스명.\* TO '사용자아이디'@'서버주소';

```text
GRANT ALL ON studydb.* TO 'study'@'localhost';
```

## 데이터베이스 목록 조회

```text
show databases;
```

## 사용자 교체

```text
quit or exit  (프로그램 종료 후)
mysql -u study -p   (다시 실행)
```

## 기본으로 사용할 데이터베이스 지정하기

use 데이터베이스명

```text
use studydb;
```

## 데이터베이스의 전체 테이블 목록 조회

```text
show tables;
```
