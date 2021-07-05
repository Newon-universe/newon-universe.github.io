---
title : "AWS EC2(Ubuntu OS)에 Nginx-mySQL-php 설치하기"
category :
    - server
tag : 
    - AWS
    - Nginx
    - mySQL
    - php
use_math : true
use_mermaid : true
toc : true
author_profile: true
sidebar:
    nav: "sidebar"
---

###### 시작하기 전에
AWS EC2 에서 Ubuntu(20.04LTS) 기반 인스턴스가 있다는 것을 전제로 한다. 아직 인스턴스가 없거나 인스턴스가 무엇인지 모른다면 [해당 링크](https://velog.io/@newon-seoul/AWS-EC2에-리눅스-기반우분투-20.04LTS-인스턴스-생성하기)로 가서 확인바란다.

>목표
>1. EC2, Ubuntu 기반 OS에 Nginx, mySQL, php 를 설치한다.
>2. 인스턴스에 탄력적 IP 주소를 할당한다.

---

###### Nginx, mySQL, php 설치하기
설치하고자 하는 EC2 에 접속을 한 후, 명령어 창에 다음과 같이 진행한다.
```
sudo apt update // 우분투의 패키지관리 최신으로 업데이트하기
sudo apt upgrade // 우분투의 패키지관리 최신으로 업그레이드하기
sudo apt-get install nginx // nginx 설치하기
nginx -v // nginx 설치 및 버전 확인
sudo apt install mysql-server // mySQL 설치하기

sudo mysql_secure_installation // 실행 전 밑에 내용 참조

sudo apt install php-fpm php-mysql // php 설치(언제나 nginx, mysql 이후에)
```

---
_mysql_secure_installation 을 하는 이유와 진행방법_

>mysql 은 데이터베이스로, 시작 전 데이터베이스의 기초 상태를 설정할 수 있으며 그 명령어가 mysql_secure_installation 이다.
>mysql_secure_installation 을 진행하면 다음과 같은 질문들을 받게 된다.

첫번째로 강력한 비밀번호만 적용할 수 있는 플러그인을 설치할 것인지 묻는다. 편의를 위해 No
<img width="650" alt="mysql 설정 1. 강력한 비밀번호 플러그인 설치 여부" src="https://user-images.githubusercontent.com/80164141/124490753-767fb280-dded-11eb-8896-3a6e5e11294e.png">  

두번째로 mySQL 에 사용될 비밀번호를 묻는다. 이 비밀번호는 데이터베이스 최고관리자 접속 시 사용된다. 2번 입력한다.
<img width="650" alt="mysql 설정 2. 비밀번호 설정, 2번 입력" src="https://user-images.githubusercontent.com/80164141/124491165-edb54680-dded-11eb-916a-ada4ebb3bf6f.png">  

세번째로 익명 사용자를 제거할 지 묻는다. Y 를 입력해 제거한다.
<img width="650" alt="mysql 설정 3. 익명 사용자 제거 여부" src="https://user-images.githubusercontent.com/80164141/124491332-1d644e80-ddee-11eb-9227-0dd311bd189d.png">  

네번째로 최고 관리자 권한으로 외부 접속을 허용할 것인지 묻는다. Y를 입력해 허용한다.
<img width="650" alt="mysql 설정 4. 최고 관리자 권한 외부 접속 허용 여부" src="https://user-images.githubusercontent.com/80164141/124491558-5f8d9000-ddee-11eb-871d-1c21fe985612.png">  

다섯번째로 설치 시 존재하는 테스트 데이터베이스를 삭제할 것인지 묻는다. Y를 입력해 삭제한다.
<img width="650" alt="mysql 설정 5. 테스트 데이터베이스 삭제 여부" src="https://user-images.githubusercontent.com/80164141/124491716-89df4d80-ddee-11eb-940d-e70a40d8ca4b.png">  

여섯번째로 priviliges table 을 다시 로드할 것인지 묻는다. 사용자들에 대한 권한 기본 옵션을 그대로 사용할 것인지 묻는 것이다. Y를 입력해 로드한다.
<img width="650" alt="mysql 설정 6. priviliges table 로드 여부" src="https://user-images.githubusercontent.com/80164141/124492030-e17db900-ddee-11eb-9ffb-c449ec7ac365.png">  

---

위의 내용대로 진행했다면 현재 우분투에는 nginx, mySQL, php 가 설치되어있는 상태이다. 이제 실제 인터넷에서 확인하기 위한 작업을 진행한다. 

우선 AWS의 EC2 콘솔로 돌아가서, 사용하고 있는 인스턴스를 클릭하고 보안을 누른 후, 보안 그룹을 누른다.
<img width="720" alt="AWS EC2 보안그룹 들어가기" src="https://user-images.githubusercontent.com/80164141/124492519-88faeb80-ddef-11eb-8441-b2eb65dbea88.png">

인바운드 규칙 편집을 들어간 후 유형에서 HTTP, 소스에서 위치 무관을 선택 후 저장한다.  
_ssh 인바운드 규칙을 삭제하면 안된다._
<img width="720" alt="AWS EC2 보안그룹 설정하기 - HTTP,위치무관" src="https://user-images.githubusercontent.com/80164141/124492915-032b7000-ddf0-11eb-9be7-ff5fccd6f22c.png">

인스턴스로 돌아가서, 퍼블릭 IPv4 주소에 있는 IP주소를 복사한 후 인터넷에 그대로 붙여넣어서 접속해본다. 다음과 같은 창이 뜬다면 Nginx 가 제대로 설치된 것.  
<img width="559" alt="Nginx 설치 성공 화면" src="https://user-images.githubusercontent.com/80164141/124493282-674e3400-ddf0-11eb-9ae1-4b75b5b1f7e1.png">

AWS 에서 보안그룹은 인바운드 규칙, 아웃바운드 규칙에 관한 내용을 설정할 수 있는 곳이다. 이를 통해 해당 보안그룹을 사용하는 EC2, RDS 등에게 어떤 포트를 통해서 들어올 것인지, 어떤 프로토콜을 사용할 것인지, 어떤 이용자에게 허용할 것인지 등에 대해서 설정할 수 있다
보안그룹에서 진행한 작업이 구체적으로 무엇인지 궁금하다면 [여기]()로.

---
1번 (Nginx, mySQL, php 설치하기)의 마지막 작업으로 php 설치 여부를 확인하기 위해서 php info 파일을 생성, 인터넷에서 확인하는 작업을 진행한다.
```
cd /var/www/html
sudo vi phpinfo.php

>
<?
phpinfo();
?>

// 저장 후 나오기

cd /etc/nginx/sites-available
sudo vi default
>
...
location ~\.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php7.4-fpm.sock;
}
...
// 해당 부분 주석 풀고 저장 후 나오기 (# 제거)

sudo service nginx restart
```  
_편집이 잘 안된다면 [여기]()를 확인_

nginx 를 확인한 퍼블릭 IP주소에서 /phpinfo.php 를 추가로 입력해서 접속한 후, phpinfo 화면이 제대로 뜨는지 확인한다.
<img width="720" alt="스크린샷 2021-07-06 오전 12 40 57" src="https://user-images.githubusercontent.com/80164141/124495253-daf14080-ddf2-11eb-9f0e-cf1bac4f303a.png">  

---
###### 탄력적 IP 주소 할당하기
현재 인스턴스가 갖고 있는 IP주소는 고정 IP가 아닌, 시간에 따라 변하게 되는 IP이다. 따라서 지금은 접속할 수 있는 IP이지만 몇 시간만 지나면 사용할 수 없거나 엉뚱한 곳으로 접속하게 된다. 이런 문제점을 해결하기 위해 인스턴스에 탄력적 IP 주소를 할당하는 작업을 진행한다.

EC2 에서 탄력적 IP를 찾는다.
<img width="245" alt="스크린샷 2021-07-06 오전 12 56 12" src="https://user-images.githubusercontent.com/80164141/124497491-de39fb80-ddf5-11eb-8860-093082366071.png">  

이후 탄력적 IP주소 할당을 클릭한다.
<img width="720" alt="스크린샷 2021-07-06 오전 12 46 41" src="https://user-images.githubusercontent.com/80164141/124497545-f3168f00-ddf5-11eb-9a9a-09473e5f89f5.png">

별 다른 설정 없이 할당을 클릭한다.
<img width="720" alt="스크린샷 2021-07-06 오전 12 46 52" src="https://user-images.githubusercontent.com/80164141/124497631-18a39880-ddf6-11eb-8e6d-4b0b71cac4c7.png">

생성된 탄력적 IP주소에 들어간 후, 탄력적 IP 주소 연결을 선택한다.
<img width="720" alt="스크린샷 2021-07-06 오전 12 47 01" src="https://user-images.githubusercontent.com/80164141/124497711-3c66de80-ddf6-11eb-88f7-2cd907535b45.png">

탄력적 IP주소를 연결하고자 하는 인스턴스를 선택하고 연결을 선택한다.
<img width="820" alt="스크린샷 2021-07-06 오전 12 47 20" src="https://user-images.githubusercontent.com/80164141/124497764-56a0bc80-ddf6-11eb-9ba1-1335c49dad64.png">

확인을 위해서 탄력적 IP주소를 인터넷 주소창에 연결해본다. Nginx, phpinfo 가 정상적으로 나온다면 잘 연결된 것이다.

> 탄력적 IP주소는 다음 3가지 사항을 지키지 않으면 과금의 요소가 된다.
> 1. 프리티어가 아닌 인스턴스에 연결하거나, 2개 이상의 탄력적 IP주소를 사용한다.
> 2. 탄력적 IP주소를 생성하고서 연결하지 않는다.
>> 인스턴스를 삭제하거나, 중단한 경우 탄력적 IP주소를 수동으로 중지 혹은 삭제시켜야 한다.

---

>출처
>[MySQL]MySQL 우분투 20.04 설치 [출처](https://velog.io/@hyeseong-dev/MySQLMySQL-우분투-20.04-설치)  
>[AWS] EC2 + 탄력적IP로 고정 IP만들기 [출처](https://artiiicy.tistory.com/17)