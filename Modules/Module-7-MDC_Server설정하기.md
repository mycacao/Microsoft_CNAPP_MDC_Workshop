# MDC for Server 살펴 보기

<p><img width="137" height="161" alt="image" src="https://github.com/user-attachments/assets/2eabc4c2-b96a-407b-be9b-63a73b066254" /></p>

#### 🎓 레벨: 200 (중급)
#### ⌛ 이 랩의 예상 완료 시간: 60분

## 목표
- 이번 랩은 MDC 에서 Server(예, Azure VM) 구성(에이전트 구성, 정책 설정) 및 동작 테스트를 목표로 한다.
- Azure VM 즉, 서버 워크로드에 대한 보호를 위한 구성, 정책 설정, 업데이트 설정 하는 방법을 이해한다.
- 보안 분석 방법도 익힐수 있다.
- ※ 단, Azure VM 이외, 즉 On-Prem Server 나 AWS, GCP 등의 VM 설치는 내용에 포함하지 않았다. 
  이 경우는 Azure Arc agent 를 설치하고 구성하면 되는데 포함하지는 않았다. 그외 사용방법은 동일하다. 

#### 가이드 링크
Microsoft Defender for Cloud - Server 설명 참고

- 국문 https://learn.microsoft.com/ko-kr/azure/defender-for-cloud/defender-for-servers-overview
- 영문 https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-servers-overview

<br><br>
---
<br><br>

#### Server 용 MDC 의 2가지 Plan
- 서버용 Defender 플랜 1(P1) 은 기본 수준, 엔드포인트용 Defender에서 제공하는 EDR 기능에 중점을 두고 제공한다.
- 서버용 Defender 플랜 2(P2) 는 플랜 1 + 기타 기능(아래 표 참고) 하여 많은 기능을 제공한다.

| 특징                                                 | 플랜 1(P1) | 플랜 2(P2) | 클라우드 가용성                                                                                                        |
| ---------------------------------------------------- | ---------- | ---------- | ---------------------------------------------------------------------------------------------------------------------- |
| 다중 클라우드 및 하이브리드 지원                     | ✅     | ✅     | Azure, AWS 및 GCP VM 및 클라우드용 Microsoft Defender에 연결된 온-프레미스 머신에서 VM(Virtual Machines)을 보호합니다.<br>서버용 Defender 지원 및 요구 사항을 검토합니다.  |                                                                                                                   |
| 엔드포인트용 Defender 자동 온보딩                    | ✅     | ✅     |                                                                                                                        |
| 엔드포인트용 Defender EDR                            |✅     | ✅     | Azure, AWS 및 GCP                                                                                                      |
| 통합 경고 및 인시던트                                | ✅     | ✅     | Azure, AWS 및 GCP                                                                                                      |
| 소프트웨어 인벤토리 검색1                            | ✅     | ✅     | Azure, AWS 및 GCP                                                                                                      |
| 규정 준수 평가                                       | ✅     | ✅     | 다양한 환경에서 다양한 표준을 사용할 수 있습니다. 규정 준수 클라우드 가용성에 대해 자세히 알아봅니다.                  |
| 취약성 검사(에이전트)                           | ✅     | ✅     | Azure, AWS 및 GCP                                                                                                      |
| 취약성 검사(에이전트리스)                           | -          | ✅     | Azure, AWS 및 GCP                                                                                                      |
| 위협 감지(Azure 네트워크 계층)                       | -          | ✅     | 애저 (Azure)                                                                                                           |
| OS 시스템 업데이트                                   | -          | ✅     | Azure, AWS, GCP 및 온-프레미스 <br> Azure ARC를 사용하여 온보딩된 머신에만 적용됩니다. 자세히 알아보기.  |
| Defender for Vulnerability Management 프리미엄 기능3 | -          | ✅     | Azure, AWS, GCP                                                                                                        |
| 맬웨어 검사(에이전트리스)                           | -          | ✅     | Azure, AWS 및 GCP                                                                                                      |
| 컴퓨터 비밀 검사(에이전트리스)                      | -          | ✅     | Azure, AWS 및 GCP                                                                                                      |
| 파일 무결성 모니터링                                 | -          | ✅     | Azure, AWS 및 GCP <br>  Azure ARC를 사용하여 온보딩된 AWS 및 GCP 머신에만 적용됩니다.      |
| Just-In-Time 가상 머신 액세스                        | -          | ✅     | Azure 및 AWS                                                                                                           |
| 네트워크 맵                                          | -          | ✅     | 애저 (Azure)                                                                                                           |
| 무료 데이터 수집(500MB)                              | -          | ✅     |                                                                                                                        |

## 화면에서 설정 확인
구독 단위로 활성화 시킬수 있다. 즉 Subscription 을 선택하고 들어간다.
<img width="1377" height="900" alt="image" src="https://github.com/user-attachments/assets/c82e2050-5266-485a-847a-f77293fed08b" />

#### 화면에서 설정 확인 
인벤토리 메뉴에 들어가서 가상머신으로 필터링하여 확인해보면 현재 활성화되어 있는 가상머신을 조회해 볼 수 있다. 
<img width="1539" height="744" alt="image" src="https://github.com/user-attachments/assets/06a61ec3-9737-47cd-a5be-37ac78de8140" />

<br><br>
---
<br><br>

## [참고] 내용 추가하기
기본으로 구독단위로 설정이 되기떄문에, 하나의 구독에 포함된 모든 VM 이 적용되고 과금이 된다.
그렇다면, 특정 리소스, VM 을 제외할수 있을까? 많은 질문주시는데 가능하다. 

리소스 단위로 Disable 시킬수 있다. 크게 2가지 방법으로 설정할수 있는데
- (1) 첫번째는 다음 azure policy 를 이용해서 제외시킬수 있음
(Configure Azure Defender for Servers to be disabled for all resource(resourcelevel) ---> 리소스 단위로 비활성화 시킬수 있음
즉 특정 VM 제외시킬수 있음


- (2) 또는 MDC API 로도 특정 리소스나 그룹에 제외시킬수 있다.
과금이 이루어지고있는지 등도 조회해볼수 있다.
pricings - Get - REST API 


<br><br>
---
<br><br>


## 2 설치 에이전트 버전 확인

Microsoft Defender 보안 포털에서 (https://security.microsoft.com)  디바이스 관리 또는 메뉴를 통해 각 디바이스에 설치된 Microsoft Defender Agent 버전을 확인할 수 있다.

Microsoft 365 Defender 포털(https://security.microsoft.com)에 접속
-	[자산] > [디바이스] 메뉴로 이동
-	디바이스 목록에서 확인하고자 하는 디바이스 선택
-	디바이스 세부 정보에서 Defender클라이언트 버전 및 엔진 버전 확인 가능 

<img width="865" height="468" alt="image" src="https://github.com/user-attachments/assets/86b317ae-8c34-49fc-9348-57ffe7c5b334" />

전체 설치된 에이전트 현황을 확인할 수 있으며, 각 디바이스를 클릭하면 세부 에이전트 정보를 확인할 수 있다.
다음 예시는 리눅스 (redhat) 을 선택한후 설치된 에이전트의 세부 버전 정보이다.

<img width="900" height="682" alt="image" src="https://github.com/user-attachments/assets/2d338029-ceba-4479-8ee9-f0b043c796cd" />

<img width="1451" height="884" alt="image" src="https://github.com/user-attachments/assets/ccab19df-1fab-474b-b883-d125a76a1658" />

에이전트의 버전은 3가지로 구분된다.  Platform 버전과 Engine 버전 그리고 Security Intelligence 버전으로 구분된다.

-	업데이트 구성 요소

|구성 요소|설명|
| ------ | ---------- | 
| Security Intelligence업데이트 |	하루에 여러 번 릴리스되며, 최신 악성코드 탐지 룰 포함 <br>즉, 탐지 패턴 | 
| Platform 업데이트	| 월별 릴리스, Defender 기능 개선 포함 업데이트 |
| Engine 업데이트 |	보안 인텔리전스에 포함되며, 탐지 성능 향상 |

또한 각 서버에서 다음과 같은 “mdatp health” 명령어를 통해 제품 버전을 확인할 수 있다.
### 2.1 리눅스 서버 예시

<img width="900" height="489" alt="image" src="https://github.com/user-attachments/assets/06c208f6-3811-49ca-b2f0-aa43a3bf9984" />

### 2.2 윈도우 서버 예시

<img width="698" height="135" alt="image" src="https://github.com/user-attachments/assets/b9809fa6-9a27-4459-bd04-d19d2150462c" />


<br><br>
---
<br><br>


## 3 설치 에이전트 버전 업데이트 방법

### 3.1 리눅스 에이전트  자동 업데이트 방법
리눅스 에이전트는 Yum Update 방식 명령어를 활용하여 업데이트 할 수 있다. 
주기적으로 업데이트 하는 경우 각 서버에 Crontab 스케줄링 기능을 활용하여 업데이트 체크하고 업데이트 하도록 설정한다. 

(국문) https://learn.microsoft.com/ko-kr/defender-endpoint/linux-update-mde-linux
(영문) https://learn.microsoft.com/en-us/defender-endpoint/linux-update-mde-linux

0 6 * * sun [ $(date +\%d) -le 15 ] && sudo yum update mdatp -y >> ~/mdatp_cron_job.log

위 예시는 분, 오전 6시(24시간 형식을 사용하는 시간), 월의 일, 모든 월, 일요일을 지정 00 했습니다. [$(date +\%d) -le 15] 은 15일(세 번째 주)보다 작거나 같지 않으면 실행되지 않습니다. 
즉, 작업은 매주 일요일 오전 6시에 실행되지만 월의 날이 15일 이하인 경우에만 실행됩니다.

즉 아래와 같은 수동 명령어를 스케줄링 등록하여 자동 업데이트 하도록 지정한다. 

<img width="900" height="199" alt="image" src="https://github.com/user-attachments/assets/c3611e1f-cf65-4a32-a3b4-ed540e645eeb" />

### 3.2 리눅스 에이전트  수동 업데이트 방법

리눅스 에이전트는 Yum Update 방식을 수동으로 수행하여 업데이트 할 수 있다
<img width="854" height="268" alt="image" src="https://github.com/user-attachments/assets/c59c01a4-76b9-4f09-87cd-f01fb3999dc1" />

다음 명령어로 버전 확인이 가능하다
<img width="900" height="199" alt="image" src="https://github.com/user-attachments/assets/1e87037c-d81f-4466-84bd-c5e1526c72e1" />

리눅스 환경의 경우, MDE.Linux Extension 이 자동으로 업데이트를 수행한다. 
수동으로 업데이트를 하는 경우, 자동 업데이트를 끄고, 최신 패키지를 중앙 저장소에서 배포한후, 각 시스템에 설치한다. 


> RHEL/CentOS/Fedora/Amazon Linux
>> sudo yum check-update 
>> sudo yum update mdatp

또는
>> 	sudo dnf check-update 
>>	sudo dnf upgrade mdatp

> SUSE Linux
>> sudo zypper refresh 
>> sudo zypper update mdatp


>	설치 확인 명령
업데이트가 완료된 후, 아래 명령어로 에이전트 버전을 확인한다.
>>	mdatp health --field product_version

또는
>>	mdatp version

### 3.3 윈도우 에이전트 자동 업데이트 방법
Defender 윈도우 에이전트 (탐지 룰 포함) 을 자동 업데이트하는 주요 방법은 **4가지**가 있다. 
본 가이드는 4가지 방법 중, 첫번째 방안 1, **Microsoft Intune 을 활용한 방법**을 가이드 한다. 방안 1을 통해 별도 물리적 서버 구성 없이 즉시 활용가능하다.
리눅스의 경우 플랫폼 에이전트가 아닌 탐지 정책을 같이 업데이트 할수 있다.

| 방안 | 설명 |
| --- | --- |
|•	방안 1, Microsoft Intune 사용 (Window, Linux 지원) |Intune을 통해 맬웨어 방지 정책을 설정하고, 자동 업데이트를 구성한다.<br> **내부 정의 업데이트 서버** 옵션을 통해 Mirror Server / WSUS를 원본으로 지정할 수도 있다.<br> 클라우드 기반 보호(MAPS)와 함께 사용하면 최신 위협에 빠르게 대응도 가능하다. |
|•	방안 2,  Microsoft Endpoint Configuration Manager (MECM) 사용 | MECM의 **소프트웨어 업데이트 지점(SUP)**을 통해 Defender 업데이트를 배포할 수 있다. <br> 자동 승인 규칙을 설정하여 업데이트를 자동으로 승인하고 배포할 수 있다. |
| •	방안 3, Windows Server Update Services (WSUS) 서버 구성 | WSUS를 통해 Microsoft Defender의 보안 인텔리전스 및 플랫폼 업데이트를 중앙에서 관리할 수 있다. <br> 업데이트는 KB2267602 (보안 인텔리전스) 및 KB4052623 (플랫폼 업데이트)로 제공 |
| •	방안4. Microsoft Update 또는 네트워크 파일 공유 | 엔드포인트가 직접 Microsoft Update에서 업데이트를 받도록 설정하거나, 내부 네트워크 파일 공유를 통해 업데이트 파일을 배포하는 방법 |

<br><br>
---
<br><br>

Defender 에이전트는 기본적으로 Windows Update 또는 Microsoft Update를 통해 자동으로 최신 버전으로 유지되며, 리눅스, 맥 버전도 동일하게 자동으로 최신 버전으로 유지된다. 

#### Intune 정책 확인
- Microsoft Intune 을 활용하는 자동 업데이트구성은 다음과 같다.

<img width="900" height="506" alt="image" src="https://github.com/user-attachments/assets/3fdbfe14-f532-4d40-8d06-99bc7abe0b71" />

참고 URL > 아래 가이드 링크에서 상세한  설명을 확인할 수 있다.
- Intune 사용하여 Intune 등록되지 않은 디바이스에서 Microsoft Defender 설정을 관리하는 방법에 대해 알아봅니다. 
- https://learn.microsoft.com/ko-kr/intune/intune-service/protect/mde-security-integration
 
다음은 Intune 이 연결되었다고 가정하고 업데이트 방법을 설명한다.
-	자동으로 업데이트 하기 위해 Microsoft Intune 에 정책 (즉, 프로필)을 만든다.
-	Microsoft Intune > 엔드포인트 보안 > 바이러스 백신 > 프로필 만들기

<img width="836" height="529" alt="image" src="https://github.com/user-attachments/assets/d195fcab-1170-4884-8f06-64d2fa5b2774" />

정책을 자동으로 업데이트 하기 위한 방법(채널)을 각각 구성한다.
- 엔진 업데이트, 플랫폼 업데이트, 보안 인텔리전스 업데이트
- 기본적으로 현재 채널(광범위)로 선택한다.

<img width="829" height="542" alt="image" src="https://github.com/user-attachments/assets/0e89ef86-8e46-4246-976a-bb411b3bf72d" />


- 업데이트가 적용되는 대상 디바이스 그룹을 할당한다.
- 검토 + 만들기 메뉴에서 구성한 에이전트 업데이트 구성 정책을 확인하고 저장한다.

<img width="900" height="572" alt="image" src="https://github.com/user-attachments/assets/23f8464f-9bd5-45e3-9dc4-e95c0573a4e8" />

정책이 만들어진 것을 메뉴에서 확인할 수 있다
- 아래 화면의 예시는 윈도우 PC + 서버를 대상으로 만들었으며
- 리눅스, 맥에 대해서도 동일하게 구성한다.

<img width="900" height="571" alt="image" src="https://github.com/user-attachments/assets/2ba80cbd-3b01-4871-a7f3-7070d38fb1fb" />

- 프로필 만들기에서 플랫폼 선택하기 화면이다.

<img width="900" height="570" alt="image" src="https://github.com/user-attachments/assets/ea92a6ad-2bdc-4b32-af0e-058557194957" />

각 디바이스에서 자동 업데이트가 정상적으로 작동하는지 확인하려면 다음을 수행한다. 
- Windows 보안 > 바이러스 및 위협 방지 > 업데이트 확인

<img width="716" height="417" alt="image" src="https://github.com/user-attachments/assets/15767214-35d2-47db-a1bb-f412a181c5d4" />

- Powershell 명령어

<img width="871" height="709" alt="image" src="https://github.com/user-attachments/assets/d0ca3a42-fe44-4986-a717-e331fe3909a4" />


### 3.4 윈도우 에이전트 수동 업데이트 방법
Microsoft Defender윈도우 에이전트(플랫폼/클라이언트)를 중앙에서 수동으로 업데이트하려면 아래와 같은 방법을 사용할 수 있다.

Microsoft 업데이트 카탈로그에서 수동 설치
>	최신 Defender 에이전트 패키지(KB 5005292 등)를 Microsoft 업데이트 카탈로그에서 다운로드
>>	웹 브라우저에서 security.microsoft.com 접속
>> 	좌측 메뉴에서 Settings(설정) → Endpoints(엔드포인트) → Onboarding(온보딩) 경로로 이동
>	다운로드한 설치 파일을 엔드포인트 서버에 배포(예: 파일 공유, 스크립트, 원격 푸시 등)하고 실행하여 수동으로 업그레이드 수행
>	이 방식은 중앙 배포 도구(예: Configuration Manager, WSUS) 없이도 적용할 수 있습니다

<img width="794" height="604" alt="image" src="https://github.com/user-attachments/assets/e31ae6ff-c622-4313-a12e-c9e057eb866d" />

#### 추가적인 방법으로 Microsoft 업데이트 카탈로그에서 다운로드
- Microsoft Update Catalog (https://www.catalog.update.microsoft.com/Home.aspx) 사이트에서 KB5005292 검색
- 검색 결과에서 운영체제(Windows Server 2012 R2, 2016)에 맞는 패키지를 선택해 다운로드
-	다운로드한 msu 또는 msi 파일을 엔드포인트에 배포 및 설치

업데이트 카탈로그의 패키지는 WSUS 등 중앙 관리 도구로도 배포할 수 있다.

<img width="900" height="308" alt="image" src="https://github.com/user-attachments/assets/afaa5b5c-70ef-4317-b6e1-548cc47fa67f" />

단말에서 수동 업데이트 방법이다

<img width="900" height="398" alt="image" src="https://github.com/user-attachments/assets/32e527d1-7d3f-4c9f-b44b-9540c7fd4b42" />

<br><br>
---
<br><br>


## 4 탐지 룰 업데이트 방안 (주기적, 비주기적, 수동)

### 4.1 리눅스 용 탐지룰 업데이트 설정 방법 

#### 리눅스 탐지룰 자동 업데이트

기본으로 리눅스용 탐지룰은 자동 업데이트 되도록 설정되어 있다. 
자동 업데이트 되도록 설정하기 위해서는 엔드포인트 보안 정책을 설정한다.

<img width="900" height="384" alt="image" src="https://github.com/user-attachments/assets/c995274f-5d1e-4da8-99f4-73357493f9af" />

기본값으로 Automatic Security Intelligence Updates 가 활성화되어 있다. 

<img width="824" height="527" alt="image" src="https://github.com/user-attachments/assets/d9ba7795-379c-4194-9042-327265e47c7a" />

이렇게 지정한 설정을 대상 디바이스에 지정하면 된다. 
기본값이 활성화(enabled) 이기 때문에 새롭게 추가할 필요는 없다. 

<img width="900" height="479" alt="image" src="https://github.com/user-attachments/assets/5b9b4109-58d5-485b-a0b0-c2953ad9085c" />

Command Line 으로 다음 명령어로 각 서버에서 활성화 시킬수 있다. 

<img width="768" height="135" alt="image" src="https://github.com/user-attachments/assets/06cc22ab-80b7-44de-a47a-f9729b3dded5" />

아래와 같은 명령어로 리눅스 탐지 룰 자동업데이트가 활성화 되어있는지도 확인할 수있다.

<img width="831" height="446" alt="image" src="https://github.com/user-attachments/assets/14e1738c-6a97-482a-9d2a-90ad656bb675" />


#### 리눅스 탐지룰 수동 업데이트
수동으로 탐지룰 수동 업데이트는 다음 명령어로 수행할 수있다.

\# mdatp definitions update

<img width="900" height="259" alt="image" src="https://github.com/user-attachments/assets/79141ac1-4539-498d-86fb-73b2f7b3672f" />

다음 2가지 명령어중 한가지로 현재 탐지룰 버전을 확인할 수 있다.
<img width="900" height="398" alt="image" src="https://github.com/user-attachments/assets/6270a332-6122-415e-a781-8fb225ccc0ce" />

<img width="900" height="229" alt="image" src="https://github.com/user-attachments/assets/0933acb9-57a2-4582-aa71-41495cccfd07" />

### 4.2 윈도우 용 탐지룰 업데이트 설정 방법 

#### 윈도우 탐지룰 자동 업데이트

#### Microsoft Defender for Endpoint와 Intune 활용 방법
Microsoft Defender 관리 센터 접속한다.
-	→ 설정 > 엔드포인트 > 구성 관리 → **MDE를 사용하여 Intune의 보안 구성 설정 적용** 옵션을 활성화하여 Intune 에서 업데이트 정책을 구성할 수 있도록 한다.

<img width="893" height="460" alt="image" src="https://github.com/user-attachments/assets/f2d47979-01e2-4286-9775-35d66f2b2e5b" />

-	적용 범위 선택
>>	모든 장치에 적용하거나 특정 태그(MDE-Management)가 지정된 장치에만 적용 가능하도록 할수 있다.
>>	장치가 MDE에 등록되면 Intune과 자동 연동된다.

<img width="900" height="447" alt="image" src="https://github.com/user-attachments/assets/09ede580-81b7-49aa-a0ce-076568d889aa" />

#### Windows 용 자동 업데이트 방법 - Defender 포털에서 등록상태 확인 

등록 상태는 Defender 포털(https://security.microsoft.com) 에서 확인 가능하다.
- 상태가 업데이트 되기 까지 최대 24시간 소요될 수 있다.

<img width="900" height="291" alt="image" src="https://github.com/user-attachments/assets/917d3b34-92ea-410f-aa1b-39349a2b58f2" />

장치(디바이스) 마다 태그를 지정하여 그룹화 관리할 수 있다.
- 아래에 예시는 MDE-Management 라는 태그를 지정하여 정책 설정시, 적용 범위로 활용할 수 있다.

<img width="900" height="289" alt="image" src="https://github.com/user-attachments/assets/86b22c8e-6369-4455-a7e6-d5d547d3bdcf" />

- 디바이스 에서 수동 태그 편집을 지정한다.

<img width="900" height="331" alt="image" src="https://github.com/user-attachments/assets/83152116-237b-4931-8b91-5375ebc87b26" />

- 목록에 지정한 태그가 설정된 것을 확인 할 수 있다.

<img width="900" height="182" alt="image" src="https://github.com/user-attachments/assets/89dc8a8d-bbdb-4839-b1ca-6966db1e2f68" />


####  Windows 용 자동 업데이트 방법 - Intune 관리 포털에서 탐지룰  업데이트(보안프로필)설정
Intune 의 엔드포인트 보안 관리화면에서 프로필을 설정하면, 장치(디바이스) 마다 태그를 지정하여 그룹화 관리할 수 있다.
-	아래에 예시는 MDE-Management 라는 태그를 지정하여 정책 설정시, 적용 범위로 활용할 수 있다. 

<img width="900" height="511" alt="image" src="https://github.com/user-attachments/assets/328b650f-6010-4895-81b0-2ee9436e372a" />

등록 상태는 Defender 포털에서 확인할수 있다.
-	Microsoft Intune (https://intune.microsoft.com) > 엔드포인트 보안 > 모든 디바이스 

이후 주기적인 탐지룰 업데이트에 대해서는 앞 2.2 항목에서 설명한 가이드와 동일하다.
다음 화면은 그룹을 동적으로 관리할 때 추가적인 기능을 활용하여 Advanced 한 기능을 활용할수 있어서 추가로 설명한다. 

<img width="900" height="419" alt="image" src="https://github.com/user-attachments/assets/85877447-2382-4616-baff-b42596b29322" />

등록 상태는 Defender 포털에서 확인할 수 있다.
- Microsoft Intune (https://intune.microsoft.com) > 엔드포인트 보안 > 모든 디바이스 
-	각 디바이스에 대한 상세 설명을 확인할수 있고,  MDE(Microsoft Defender for Endpoint) 가 설정된 내용을 확인할수 있다.

<img width="900" height="263" alt="image" src="https://github.com/user-attachments/assets/bd1a24f3-cff6-41e9-92b8-dd33e31f4d67" />

#### 참고로, Entra 에서 동적 구성원 규칙을 설정하여, 향후 프로파일(정책)이 적용되는 대상을 유연하게 설정하여 지정할수 있도록 하는 방법이다 .
-	Entra 화면 (https://entra.microsoft.com) 에서 그룹 > 모든 그룹 > 동적 구성원 규칙

<img width="900" height="432" alt="image" src="https://github.com/user-attachments/assets/a44a2db9-02ca-4dd2-a57e-05149d2df1f6" />

#### Windows 용 자동 업데이트 방법 -  Intune/Defender 포털에서 탐지룰 업데이트(보안프로필)설정

다음은 탐지룰 업데이트를 위해 보안프로필(정책)을 정의하는 부분이며,탐지룰 업데이트에 대해서는 앞 항목에서 설명한 가이드와 동일하다.

<img width="900" height="413" alt="image" src="https://github.com/user-attachments/assets/972b31a7-5b8f-48a5-9374-f9de1fff6830" />

Defender 포털에서도 생성할 수 있다.

<img width="900" height="332" alt="image" src="https://github.com/user-attachments/assets/b04ac73c-2c4e-4f22-9b79-10c0cda8ef1a" />

#### 윈도우 수동 업데이트 방법

1. Windows 보안 설정에서 수동 업데이트
-가장 간단한 방법은 Windows 보안 앱을 통해 직접 업데이트를 확인하는 것이다.
-시작 메뉴 > 설정 > 업데이트 및 보안 > Windows 보안
-Windows 보안 열기 > 바이러스 및 위협 방지 클릭
-아래로 스크롤하여 "보호 업데이트" > 업데이트 확인 클릭
- → 최신 보안 인텔리전스가 수동으로 다운로드 및 설치된다.
- 이항목도 앞 절의항목과 동일하다.
________________________________________
2. Microsoft 업데이트 카탈로그에서 수동 다운로드
보안 인텔리전스 또는 플랫폼 업데이트를 직접 다운로드하여 설치할 수 있다.
-	Microsoft 업데이트 카탈로그 접속
-다음 키워드로 검색:
-보안 인텔리전스: KB2267602
-플랫폼 업데이트: KB4052623
-운영체제에 맞는 버전 선택 후 .exe 또는 .cab 파일 다운로드
-	다운로드한 파일을 실행하여 수동 설치
________________________________________
3. PowerShell 명령어로 수동 업데이트
고급 사용자는 PowerShell을 통해 Defender 업데이트를 수동으로 실행할 수 있다.
-	이 명령은 최신 보안 인텔리전스를 다운로드하고 적용합니다.
-	관리자 권한 PowerShell에서 실행해야 합니다.

## 5 수동 탐지룰 생성 방법 

### 5.1 수동 탐지룰 확인 방법 
Microsoft Defender for Endpoint(MDE)에서 **수동 탐지 룰(탐지 규칙)**을 생성하려면, 일반적으로 고급 헌팅(Advanced Hunting) 또는 사용자 지정 감지(Custom Detection Rules) 기능을 사용합니다. <br> 이 기능은 Microsoft Defender XDR 포털에서 제공되며, 다음과 같은 절차로 수동 탐지 룰을 만들 수 있다.

Microsoft Defender XDR 포털 접속
-	URL: https://security.microsoft.com
-	관리자 권한 필요

<img width="900" height="641" alt="image" src="https://github.com/user-attachments/assets/55f9b1a7-f3f3-4702-b2ad-8d6e3f4b2f51" />

고급 헌팅 쿼리 작성
-	메뉴: "헌팅 > 고급 헌팅"
-	Kusto Query Language (KQL)를 사용하여 탐지 쿼리를 작성함
-	예시: 특정 프로세스 실행 탐지

<img width="900" height="721" alt="image" src="https://github.com/user-attachments/assets/84df1f49-b520-405d-9727-676c11f370e5" />

사용자 지정 탐지 규칙 생성
-	메뉴: "헌팅 > 사용자 지정 감지(Custom detection rules)"
-	**규칙 만들기(Create rule)** 클릭
-	앞서 작성한 고급 헌팅 쿼리를 기반으로 규칙 생성

<img width="900" height="319" alt="image" src="https://github.com/user-attachments/assets/f93bb55c-0ef6-4659-8b22-b3877d158c01" />

-	쿼리 실행 주기: 5분, 10분, 1시간 등
-	경고 심각도: 낮음, 보통, 높음
-	경고 제목 및 설명
- 조치: 이메일 알림, 티켓 생성, 자동 응답 등

<img width="900" height="749" alt="image" src="https://github.com/user-attachments/assets/2b9aac20-1e98-43c9-8878-5feeaf1f5a01" />

규칙 저장 및 활성화
- 규칙을 저장하고 활성화하면, 지정된 주기마다 쿼리가 실행되어 조건에 맞는 이벤트가 탐지된다.

<img width="900" height="406" alt="image" src="https://github.com/user-attachments/assets/cc67eb38-5f85-4223-970e-b84675c79010" />
