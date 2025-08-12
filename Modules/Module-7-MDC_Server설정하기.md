# MDC for Server 살펴 보기

<p><img width="137" height="161" alt="image" src="https://github.com/user-attachments/assets/2eabc4c2-b96a-407b-be9b-63a73b066254" /></p>

#### 🎓 레벨: 200 (중급)
#### ⌛ 이 랩의 예상 완료 시간: 60분

## 목표
- 이번 랩은 MDC 에서 Server (예, Azure VM) 구성 및 테스트를 목표로 한다.
- Azure VM 즉, 서버 워크로드에 대한 보호를 위한 구성, 정책 설정, 업데이트 설정 하는 방법을 이해할수 있다.
- 보안 분석 방법도 익힐수 있다.

#### 가이드 링크
Microsoft Defender for Cloud - Server

- 국문 https://learn.microsoft.com/ko-kr/azure/defender-for-cloud/defender-for-servers-overview
- 영문 https://learn.microsoft.com/en-us/azure/defender-for-cloud/defender-for-servers-overview

<br><br>
---
<br><br>

#### Server 용 MDC 의 2가지 Plan
- 서버용 Defender 플랜 1(P1) 은 초급 수준이며 엔드포인트용 Defender 통합에서 제공하는 EDR 기능에 중점을 둡니다.
- 서버용 Defender 플랜 2(P2) 는 계획 1 및 기타 기능과 동일한 기능을 제공합니다.


| 특징                                                 | 계획 1(P1) | 플랜 2(P2) | 클라우드 가용성                                                                                                        |
| ---------------------------------------------------- | ---------- | ---------- | ---------------------------------------------------------------------------------------------------------------------- |
| 다중 클라우드 및 하이브리드 지원                     | ✅     | ✅     | Azure, AWS 및 GCP VM 및 클라우드용 Microsoft Defender에 연결된 온-프레미스 머신에서 VM(Virtual Machines)을 보호합니다.<br>서버용 Defender 지원 및 요구 사항을 검토합니다.  |                                                                                                                   |
| 엔드포인트용 Defender 자동 온보딩                    | ✅     | ✅     |                                                                                                                        |
| 엔드포인트용 Defender EDR                            |✅     | ✅     | Azure, AWS 및 GCP                                                                                                      |
| 통합 경고 및 인시던트                                | ✅     | ✅     | Azure, AWS 및 GCP                                                                                                      |
| 소프트웨어 인벤토리 검색1                            | ✅     | ✅     | Azure, AWS 및 GCP                                                                                                      |
| 규정 준수 평가                                       | ✅     | ✅     | 다양한 환경에서 다양한 표준을 사용할 수 있습니다. 규정 준수 클라우드 가용성에 대해 자세히 알아봅니다.                  |
| 취약성 검사(에이전트 기반)                           | ✅     | ✅     | Azure, AWS 및 GCP                                                                                                      |
| 취약성 검사(에이전트 없는)                           | -          | ✅     | Azure, AWS 및 GCP                                                                                                      |
| 위협 감지(Azure 네트워크 계층)                       | -          | ✅     | 애저 (Azure)                                                                                                           |
| OS 시스템 업데이트                                   | -          | ✅     | Azure, AWS, GCP 및 온-프레미스 <br> Azure ARC를 사용하여 온보딩된 머신에만 적용됩니다. 자세히 알아보기.  |
| Defender for Vulnerability Management 프리미엄 기능3 | -          | ✅     | Azure, AWS, GCP                                                                                                        |
| 맬웨어 검사(에이전트 없는)                           | -          | ✅     | Azure, AWS 및 GCP                                                                                                      |
| 컴퓨터 비밀 검사(에이전트 없는)                      | -          | ✅     | Azure, AWS 및 GCP                                                                                                      |
| 파일 무결성 모니터링                                 | -          | ✅     | Azure, AWS 및 GCP <br>  Azure ARC를 사용하여 온보딩된 AWS 및 GCP 머신에만 적용됩니다.      |
| Just-In-Time 가상 머신 액세스                        | -          | ✅     | Azure 및 AWS                                                                                                           |
| 네트워크 맵                                          | -          | ✅     | 애저 (Azure)                                                                                                           |
| 무료 데이터 수집(500MB)                              | -          | ✅     |                                                                                                                        |

## 화면에서 설정 확인 
<img width="1377" height="900" alt="image" src="https://github.com/user-attachments/assets/c82e2050-5266-485a-847a-f77293fed08b" />

#### 화면에서 설정 확인 
<img width="1539" height="744" alt="image" src="https://github.com/user-attachments/assets/06a61ec3-9737-47cd-a5be-37ac78de8140" />

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
- 리눅스 서버 예시

<img width="900" height="489" alt="image" src="https://github.com/user-attachments/assets/06c208f6-3811-49ca-b2f0-aa43a3bf9984" />

- 윈도우 서버 예시

<img width="698" height="135" alt="image" src="https://github.com/user-attachments/assets/b9809fa6-9a27-4459-bd04-d19d2150462c" />





