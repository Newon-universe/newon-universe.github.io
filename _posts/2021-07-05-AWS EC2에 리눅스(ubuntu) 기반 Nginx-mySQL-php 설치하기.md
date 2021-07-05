---
title : "AWS EC2에서 (리눅스 기반)우분투 20.04LTS 인스턴스 생성하기 "
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
###### AWS EC2에 (리눅스 기반)우분투 20.04LTS 인스턴스 생성하기  

> **목표**
> 1. AWS EC2 에서 우분투 20.04 LTS (프리티어) 인스턴스를 생성한다.
> 2. 생성한 인스턴스에 접속하고 종료해본다.
> _빠르게 해결하고 싶다면 TMI가 아닌 부분만 숫자 부분만 따라하면 된다._  
>
> 추가 목표 1. AWS EC2 가 무엇인지 인지한다. (TMI)
> 추가 목표 2. 리눅스와 우분투의 차이가 무엇인지 인지한다. (TMI)
<br/>

###### AWS EC2란 무엇인가?  

 회사 아마존이 제공하는 EC2 서비스를 AWS(Amazon Web Service) EC2(Elastic Computer Cloud)라고 한다.  
 현재 전 세계에서 클라우드 [점유율 1위](https://eiec.kdi.re.kr/publish/reviewView.do?idx=44&ridx=4&fcode=000020003600002)를 달리고 있으며 특히 IaaS(Infrastructure as a Service) 분야에서 강점을 보이고 있다. IaaS를 간략히 요약하면 기업이 제공하는 환경과 자원(용량, cpu, 네트워킹 등) 을 통해 원하는 내용을 구축하는 서비스이다.[자세한 설명](https://wnsgml972.github.io/network/2018/08/14/network_cloud-computing/)  
  아마존의 EC2 는 대표적인 Iaas 사업이자 아마존의 핵심 사업으로, 사용자가 원하는 OS와 컴퓨터 사양을 정한 후 해당 자원을 임대받을 수 있는 서비스이다. 다음은 아마존에서 제공하는 EC2의 설명이다.  
<br/>
>Amazon Elastic Compute Cloud(Amazon EC2)는 Amazon Web Services(AWS) 클라우드에서 확장 가능 컴퓨팅 용량을 제공합니다. Amazon EC2를 사용하면 하드웨어에 선투자할 필요가 없어 더 빠르게 애플리케이션을 개발하고 배포할 수 있습니다. Amazon EC2를 통해 원하는 만큼 가상 서버를 구축하고 보안 및 네트워크 구성과 스토리지 관리가 가능합니다. 또한 Amazon EC2는 요구 사항이나 갑작스러운 인기 증대 등 변동 사항에 따라 신속하게 규모를 확장하거나 축소할 수 있어 서버 트래픽 예측 필요성이 줄어듭니다.
  [링크](https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/concepts.html)  

AWS 서비스를 사용할 때, 우리는 프리티어 사용을 목표로 한다. EC2 기준 프리티어는 월 750시간(24시간*31일 = 744)을 무료로 제공한다. [자세한 내용](https://aws.amazon.com/ko/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc&awsf.Free%20Tier%20Types=*all&awsf.Free%20Tier%20Categories=*all)  
<br/>

###### AWS EC2 에 인스턴스 생성하기  
<br/>

1. [아마존 콘솔](https://aws.amazon.com/ko/console/) 에 로그인 한 후 AWS 서비스 항목에서 EC2를 선택한다.  
<img width="720" alt="AWS EC2 위치" src="https://user-images.githubusercontent.com/80164141/124434063-67c5db00-ddae-11eb-92d2-c71156108b2d.png">  
<br/>

2. AWS EC2에 접속하면 왼쪽 메뉴바에서 인스턴스 -> 인스턴스 시작을 누른다.  
<img width="720" alt="AWS EC2 인스턴스 시작 누르기" src="https://user-images.githubusercontent.com/80164141/124434668-1c5ffc80-ddaf-11eb-9a44-4592b93495a1.png">  
<br/>

3. 단계 1: Amazon Machine Image(AMI) 선택 에서 프리티어에 속한 Ubuntu 20.04 LTS 를 선택한다.  
`TMI 1. Ubuntu 는 우분투 OS / 20.04 는 20.04 버전 / LTS 는 Long Term Support 라는 뜻이다. LTS 버전은 일반적인 경우보다 장기간에 걸쳐 지원한다는 뜻으로, 윈도우 xp가 현재도 사용은 가능하지만 MS사에서 서비스를 종료하였다는 맥락에서 이해하면 편할 것 같다.`  
`TMI 2. 리눅스는 UNIX 운영체제를 기반으로 만들어진 운영체제이다. 다중 사용자, 다중 작업(멀티태스킹), 다중 스레드를 지원하며 UNIX가 그러하였듯 서버로서 작동하는데 최적화 되어있는 OS이다. 리눅스는 오픈소스로 배포되었으며, 이에 따라 회사 혹은 개인의 편의대로 수정된 수 많은 버전의 리눅스가 존재한다. 대표적으로 레드햇이라는 회사가 배포한 센토스(Cent OS), 캐노니컬 회사가 배포한 우분투(Ubuntu OS)가 있다.`  
<img width="720" alt="AWS EC2 Ubuntu 20.04 LTS 프리티어 버전 선택하기" src="https://user-images.githubusercontent.com/80164141/124439491-731c0500-ddb4-11eb-9792-547ef730d00f.png">  
<br/>

4. 단계 2: 인스턴스 유형 선택에서는 프리티어에 해당하는 (2021.07.05 기준 1개밖에 없다.) 유형, t2.micro 유형을 선택하고, 다음:인스턴스 세부 정보 구성을 선택한다.  
<img width="720" alt="EC2 인스턴스 유형 선택 t2.micro" src="https://user-images.githubusercontent.com/80164141/124442202-7369cf80-ddb7-11eb-81e6-8f03c78fd183.png">  
`TMI 3. t2.micro 유형은 vCPU (가상 cpu)를 제공하는데, 최대 3.3GHZ cpu1개, RAM 메모리 1GB 사양이며 물리 cpu 사양의 절반의 성능이다.`
[출처](https://aws.amazon.com/ko/ec2/instance-types/)  

<br/>
5. 단계 3: 인스턴스 세부 정보 구성은 설정없이 바로 다음:스토리지 추가로 넘어간다.  
<img width="720" alt="EC2 세부 정보 구성 설정 없이 넘어가기" src="https://user-images.githubusercontent.com/80164141/124443032-48cc4680-ddb8-11eb-933e-aebc68efae0d.png">  
`TMI 4. 인스턴스 세부 정보 구성은 여러개의 인스턴스, 여러개의 서버가 있을 때 어떻게 설정할 것인가에 대한 내용이다. auto scrolling 은 비정상적인 인스턴스를 다른 인스턴스로 대체할 때의 옵션, 서브넷 설정이란 IP를 부여받았을 때, 필요한 양의 IP만 설정할 수 있게끔 하는 내용이다. 퍼블릭 IP는 인스턴스를 전부 생성한 후에 따로 설정할 예정이다.`  
<br/>

6. 단계 4: 스토리지 추가에서는 기본 설정인 8GB 를 프리티어 최대 용량인 30GB로 설정만 하고 태그추가로 넘어간다.  
<img width="720" alt="EC2 스토리지 기존 8GB 에서 30GB로 설정" src="https://user-images.githubusercontent.com/80164141/124444635-c80e4a00-ddb9-11eb-8892-95ccfe8b7b81.png">  
`TMI 5. 프리티어는 SSD와 마그네틱 버전을 지원하는데, 마그네틱 버전은 HDD를 의미한다. 속 터지고 싶지 않다면 SSD를 선택하자.`  
`TMI 6. 프리티어를 제외하면 AWS는 프로비저닝된 SSD를 제공하는 것을 알 수 있다. '프로비저닝' 이란 프로비저닝은 사용자의 요구에 맞게 시스템 자원을 할당, 배치, 배포해 두었다가 필요 시 시스템을 즉시 사용할 수 있는 상태로 미리 준비해 두는 것을 말한다. 일상 경험에 빗대어 말하면 스스로 부품을 구하는 조립 PC를 사느냐, 대기업 PC를 사느냐 (삼X을 사면 X성 복원 솔루션이 추가되어 있다.) 차이` [출처](https://glqdlt.tistory.com/268)  
<br/>

7. 단계 5: 태그 추가에서는 인스턴스에 태그를 붙일 수 있다. 원한다면 붙이도록 한다. 다음: 보안 그룹 구성으로 넘어간다.  
<img width="720" alt="EC2 태그 설정하기 - 원한다면 붙이고 아니면 넘어가기" src="https://user-images.githubusercontent.com/80164141/124446245-34d61400-ddbb-11eb-9576-e35302f2ce78.png">  
<br/>

8. 단계 6: 보안 그룹 구성은 넘어가도록 한다. 해당 내용은 Nginx등 웹 서버를 설치했을 때 다시 와서 설정한다. 검토 밑 시작으로 넘어간다.  
<img width="720" alt="스크린샷 2021-07-05 오후 6 04 36" src="https://user-images.githubusercontent.com/80164141/124446636-926a6080-ddbb-11eb-8505-eef296b76959.png">  
`보안 그룹 구성은 인바인드 설정, 아웃바인드 설정에 해당한다. 즉 웹 서버의 어떤 포트를 열어줄 것인지, 닫을 것인지 등에 관한 설정이다. 이와 관련한 자세한 내용은 Nginx-mySQL-php 설치 포스트에서 설명한다.`  
<br/>

9. 단계 7: 인스턴스 시작 밑 검토에서 설정한 내용들을 다시 한번 확인한 후, 시작하기를 누른다. 시작하기를 누르면 인스턴스를 처음 생성하는 것이라면 새 키 페어 생성이라는 창이 나온다. (이미 생성한 적이 있다면 기존의 키 페어를 사용하거나, 새로운 키페어를 사용하던지 무관하다.) 키페어의 이름을 정해주고, 다운로드 해준다.
<img width="720" alt="인스턴스 시작하기 밑 키 페어 생성하기" src="https://user-images.githubusercontent.com/80164141/124447253-26d4c300-ddbc-11eb-9696-d31ae2216a72.png">  
집에 도어락이 아닌 열쇠로 들어갈 때, 사용하는 키에 해당하는 것이 키페어이다. 잃어버리더라도 재발급 받을 수 있겠지만 열쇠공을 찾아가는 번거로움이 따른다. AWS가 제공하는 잃어버렸을 때의 방법은 [다음](https://aws.amazon.com/ko/premiumsupport/knowledge-center/ec2-windows-replace-lost-key-pair/)과 같다.  
<br/>

###### 생성한 AWS EC2 인스턴스에 접속해보기
1. 생성한 인스턴스를 선택한 후, 연결을 누르고 예시에 있는 부분을 복사한다.
<img width="720" alt="생성한 인스턴스에 접속하기 1. 인스턴스를 눌러서 개요를 본다." src="https://user-images.githubusercontent.com/80164141/124449977-f2163b00-ddbe-11eb-8ca9-74b78b53155b.png">
<img width="720" alt="생성한 인스턴스에 접속하기 2. 개요에서 연결을 누른다." src="https://user-images.githubusercontent.com/80164141/124449981-f2aed180-ddbe-11eb-9b34-1b1b02669cc9.png">
<img width="720" alt="생성한 인스턴스에 접속하기 3. 예시에 나온 부분을 복사한다." src="https://user-images.githubusercontent.com/80164141/124449983-f3476800-ddbe-11eb-94a6-3796c9c0b25c.png">

2. 맥의 경우 터미널을 키고서, 다운로드 받은 위치로 간다.  
 2-1. `cd 폴더이름` 을 사용하면 현재 위치에서 해당 폴더로 갈 수 있다.  
 2-2. `ls`를 사용하면 현재 폴더에서 어떤 파일들이 있는지 확인할 수 있다.
 2-3.  `pwd`를 사용하면 터미널이 현재 위치한 정보를 알려준다. 
 2-4. `파일명을 일부 치고 탭`을 사용하면 파일이름을 자동완성해준다.
 다음은 필자의 터미널을 처음 켰을 때, rising_programmer -> AWS_key_pair 폴더에서 키페어(RP3_Server_a.pem)를 찾는 gif이다.  
 ![터미널 사용법](https://user-images.githubusercontent.com/80164141/124453825-ba10f700-ddc2-11eb-9e14-7ff906034554.gif)  

 *윈도우의 경우 [다음](https://victorydntmd.tistory.com/62)을 참조한다.
<br/>

3. 키페어가 있는 위치에서 복사한 내용을 붙여넣기 한다.
다음 gif는 2번에서 바로 복사한 내용을 붙여넣기 했을 때의 결과이다. 초록색으로 ubuntu@... 가 떳다면 성공
![EC2 접속](https://user-images.githubusercontent.com/80164141/124455241-4bcd3400-ddc4-11eb-9b25-4a34c3e5ea10.gif)  
`TMI 7. 터미널에서 사용한 명령어들은 리눅스 명령어들이다. cd, ls, pwd 외에도 다양한 리눅스 명령어들이 있으나 모든 명령어들을 당장에 알 필요는 없다. 필요한 명령어만 그때 그때 찾아서 쓰면 되는 부분.` 

> ***출처***  
> _KDI정보센터 - 클라우드 (종합)편[출처](https://eiec.kdi.re.kr/publish/reviewView.do?idx=44&ridx=4&fcode=000020003600002)_  
> _클라우드 컴퓨팅, IaaS, PaaS, SaaS이란?[출처](https://wnsgml972.github.io/network/2018/08/14/network_cloud-computing/)_  
> _Amazon EC2이란 무엇입니까?[출처](https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/concepts.html)_  
> _AWS 요금제도 [출처](https://aws.amazon.com/ko/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc&awsf.Free%20Tier%20Types=*all&awsf.Free%20Tier%20Categories=*all)_  
> _Amazon EC2 인스턴스 유형 [출처](https://aws.amazon.com/ko/free/?all-free-tier.sort-by=item.additionalFields.SortRank&all-free-tier.sort-order=asc&awsf.Free%20Tier%20Types=*all&awsf.Free%20Tier%20Categories=*all)_  
> _프로비저닝이란 [출처](https://glqdlt.tistory.com/268)_  
> _EC2Config 또는 EC2Launch를 사용하여 관리자 암호를 재설정할 때 EC2 Windows 인스턴스의 분실 키 페어를 교체하려면 어떻게 해야 하나요?[출처](https://aws.amazon.com/ko/premiumsupport/knowledge-center/ec2-windows-replace-lost-key-pair)_  
> _🙈[AWS] EC2 (2) - 윈도우에서 EC2 인스턴스 접속하기🐵[출처](https://victorydntmd.tistory.com/62)_  

> Thanks to
> Rising Programmer3 / [Colt](https://velog.io/@banjjoknim)

