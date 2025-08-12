# 탐지 이벤트 처리 프로세스 

## 1. 탐지 이벤트 확인 방법
📌 엔드포인트용 Defender에 대한 보안 운영 가이드 참고 링크 : https://learn.microsoft.com/ko-kr/defender-endpoint/mde-sec-ops-guide

Microsoft Defender for Endpoint(MDE)의 **탐지 이벤트 처리 프로세스**는 위협이 탐지된 후 자동화된 분석, 대응, 수동 검토까지 이어지는 **다단계 보안 운영 흐름**으로 구성된다. 
<br> 아래는 그 상세한 단계별 설명이며 위 링크를 참고한다.

### 📚 📑 Microsoft Defender for Endpoint 탐지 이벤트 처리 프로세스
#### 1.1 데이터 수집 및 센서 감지

각 엔드포인트에 설치된 Defender 센서가 다음과 같은 데이터를 수집
- 프로세스 실행 정보
- 네트워크 연결
- 파일 및 레지스트리 변경
- 사용자 활동

이 데이터는 **Microsoft Defender XDR** 클라우드로 전송

#### 1.2 실시간 위협 탐지
수집된 데이터를 기반으로 다음 탐지 기술이 작동함
-	시그니처 기반 탐지 (정적 분석)
-	행위 기반 탐지 (동적 분석)
-	기계 학습 기반 탐지
-	IOC/IOA 기반 탐지 (지표 기반)
  
#### 1.3 경고(Alert) 생성
위협이 탐지되면 **경고(Alert)**가 생성됨
경고는 다음 정보를 포함
- 탐지된 위협 유형
- 영향을 받은 디바이스 및 사용자
- 관련된 파일, 프로세스, IP 등

#### 1.4. 인시던트(Incident)로 그룹화
여러 개의 관련 경고는 **하나의 인시던트**로 자동 그룹화됨
- 예: 동일한 공격자가 여러 디바이스에서 활동한 경우
  
#### 1.5. 자동 조사 및 대응 (AIR)
Defender는 자동으로 다음 작업을 수행할 수 있다.
- 의심 파일 분석 (sandbox)
- 프로세스 종료
- 파일 격리
- 레지스트리 롤백
이 과정은 자동화 규칙에 따라 실행되며, 수동 승인도 설정 가능

#### 1.6. 보안 운영 센터(SOC)의 수동 검토
보안 분석가는 Defender 포털에서 인시던트를 검토하고 다음을 수행한다.
- 고급 헌팅(KQL)으로 추가 분석
- 사용자 지정 감지 규칙 생성
- 경고의 진위 여부 판단 (True Positive / False Positive)
- 대응 조치 승인 또는 거부

#### 1.7. 외부 시스템 연동
Defender는 다음과 같은 외부 시스템과 연동됩니다:
- SIEM (예: Microsoft Sentinel): 로그 통합 및 상관 분석
- SOAR: 자동화된 대응 워크플로우 실행
- ServiceNow 등 티켓 시스템과 연동

#### 1.8. 사후 분석 및 보고
인시던트 해결 후 다음 보고서가 생성됩니다:
- 위협 분석 보고서
- 디바이스 상태 보고서
- 사용자 활동 보고서
이 정보는 향후 탐지 룰 개선 및 정책 수립에 활용됨

<br><br>

## 📑 2. 주간 활동

📍 메시지 센터 확인
* Microsoft Defender XDR Microsoft 365 메시지 센터를 사용하여 새로운 기능 및 변경된 기능, 계획된 유지 관리 또는 기타 중요한 공지 사항과 같은 향후 변경 사항을 알려줌. 내용을 검토함
* 메시지 센터 메시지를 검토하여 환경에 영향을 주는 향후 변경 내용을 이해함
* 상태 탭의 Microsoft 365 관리 센터 액세스할 수 있음
* Microsoft 365 서비스 상태를 검사 방법을 참조
  + https://learn.microsoft.com/ko-kr/microsoft-365/enterprise/view-service-health?view=o365-worldwide

📍보안 운영 팀
 위협 보고 검토
  + 상태 보고서를 검토하여 해결해야 하는 디바이스 위협 추세를 식별합니다.
  + 위협 방지 보고서를 참조
  + https://learn.microsoft.com/ko-kr/defender-endpoint/threat-protection-reports  

* 위협 분석 검토
  + 위협 분석을 검토하여 환경에 영향을 주는 캠페인을 식별합니다.
  + 위협 분석을 통해 새로운 위협 추적 및 대응을 참조하세요
  + https://learn.microsoft.com/ko-kr/defender-xdr/threat-analytics  

📍보안 관리 팀
* TVM(위협 및 취약성) 상태 검토
  + TVM을 검토하여 조치가 필요한 새로운 취약성 및 권장 사항을 식별합니다.
  + 취약성 관리 dashboard 참조하세요
  + https://learn.microsoft.com/ko-kr/defender-vulnerability-management/tvm-dashboard-insights  

* 공격 표면 감소 보고 검토
  + ASR 보고서를 검토하여 환경에 영향을 주는 파일을 식별합니다.
  + 공격 표면 감소 규칙 보고서를 참조하세요
  + https://learn.microsoft.com/ko-kr/defender-endpoint/attack-surface-reduction-rules-report  

* 웹 보호 이벤트 검토
  + 웹 방어 보고서를 검토하여 차단된 IP 주소 또는 URL을 식별합니다.
  + 웹 보호를 참조하세요
  + https://learn.microsoft.com/ko-kr/defender-endpoint/web-protection-overview  

<br><br>

## 📑 3. 월별 활동

📍 최근 릴리스된 업데이트를 이해하려면 다음 문서를 검토함
* 엔드포인트용 Microsoft Defender의 새로운 기능
  + https://learn.microsoft.com/ko-kr/defender-endpoint/whats-new-in-microsoft-defender-endpoint
* Windows의 엔드포인트용 Microsoft Defender 새로운 기능
  + https://learn.microsoft.com/ko-kr/defender-endpoint/windows-whatsnew
* Mac의 엔드포인트용 Microsoft Defender 새로운 기능
  + https://learn.microsoft.com/ko-kr/defender-endpoint/mac-whatsnew
* Linux의 엔드포인트용 Microsoft Defender 새로운 기능
  + https://learn.microsoft.com/ko-kr/defender-endpoint/linux-whatsnew
* iOS의 엔드포인트용 Microsoft Defender 새로운 기능
  + https://learn.microsoft.com/ko-kr/defender-endpoint/ios-whatsnew
* Android의 엔드포인트용 Microsoft Defender 새로운 기능
  + https://learn.microsoft.com/ko-kr/defender-endpoint/android-whatsnew

📍 보안 관리 팀
* 정책에서 제외된 디바이스 검토
* 엔드포인트용 Defender 정책에서 제외된 디바이스가 있는 경우 해당 디바이스를 정책에서 제외해야 하는지 여부를 검토하고 확인함

<br><br>

## 🕒 4. 정기 활동

이러한 작업은 보안 상태에 대한 유지 관리로 간주되며 지속적인 보호에 중요하다. <br> 그러나 시간과 노력이 필요할 수 있으므로 이러한 작업을 수행하기 위해 유지할 수 있는 표준 일정을 설정하는 것이 좋다.

📍예외 항목 검토
* 사용자 환경에서 설정된 제외를 검토하여 더 이상 제외할 필요가 없는 항목을 제외하여 보호 격차를 만들지 않았는지 확인
* **Defender 정책 구성 검토**
  +	Defender 구성 설정을 주기적으로 검토하여 필요에 따라 설정되었는지 확인
* 자동화 수준 검토
  + 자동화된 조사 및 수정 기능에서 자동화 수준을 검토. 자동화된 조사 및 수정의 자동화 수준을 참조하세요.
  + https://learn.microsoft.com/ko-kr/defender-endpoint/automation-levels
* 사용자 지정 검색 검토
  + 생성된 사용자 지정 검색이 여전히 유효하고 효과적인지 주기적으로 검토. 사용자 지정 검색 검토를 참조하세요.
  + https://learn.microsoft.com/ko-kr/defender-xdr/custom-detection-rules
* 경고 표시 안 함 검토
  + 생성된 경고 제거 규칙을 주기적으로 검토하여 여전히 필요하고 유효한지 디바이스를 정책에서 제외해야 하는지 여부를 검토하고 확인함

<br><br>

## 💪 5. 에이전트 설치율/ 최신 업데이트 적용률 / 이벤트 탐지율 모니터링
Microsoft Defender 포털(https://security.microsoft.com) 의 Report > Device Health > Microsoft Defender Antivirus Health 메뉴를 통해 현황을 파악할 수 있다. 

에이전트 유형(윈도우, 리눅스, 맥) 의 설치 버전별 통계를 볼수 있다. 

<img width="900" height="618" alt="image" src="https://github.com/user-attachments/assets/7a2456ab-3d61-49d0-a12b-fc0187a24a2e" />
<br>



 


해당 항목을 클릭하면, 세부 목록을 볼수 있다. 리눅스 특정 버전을 클릭하면 다음과 같은 화면이 보인다.
 
<img width="900" height="605" alt="image" src="https://github.com/user-attachments/assets/a09f9116-5af3-4d20-abfe-286007c1e881" />
<br>

이외에도 검색명령어를 활용하여 각종 통계정보를 확인할 수 있다.

 <img width="900" height="427" alt="image" src="https://github.com/user-attachments/assets/26db18ab-0374-4f8a-b6af-4c3ae9ee80cf" />
<br>


```
DeviceTvmSecureConfigurationAssessment
| where ConfigurationId in ('scid-90', 'scid-91', 'scid-2003', 'scid-2010', 'scid-2011', 'scid-2012', 'scid-2013', 'scid-2016', 'scid-5095', 'scid-6095', 
                            'scid-5090', 'scid-6090', 'scid-5091', 'scid-6091', 'scid-5094', 'scid-6094')
| extend Test = case(
    ConfigurationId == 'scid-2003' and OSPlatform startswith 'Windows', 'TamperProtection',
    ConfigurationId == 'scid-2010' and OSPlatform startswith 'Windows', 'AntivirusEnabled',
    ConfigurationId == 'scid-90'   and OSPlatform startswith 'Windows', 'EmailScanning', 
   ConfigurationId == 'scid-2011' and OSPlatform startswith 'Windows', 'AntivirusSignatureVersion',
    ConfigurationId == 'scid-5095' and OSPlatform == 'macOS', 'AntivirusSignatureVersion',
    ConfigurationId == 'scid-6095' and OSPlatform == 'Linux', 'AntivirusSignatureVersion',
    ConfigurationId == 'scid-2012' and OSPlatform startswith 'Windows','RealtimeProtection',
    ConfigurationId == 'scid-5090' and OSPlatform == 'macOS', 'RealtimeProtection',
    ConfigurationId == 'scid-6090' and OSPlatform == 'Linux', 'RealtimeProtection',
    'NA'),
        Result = case(IsCompliant == 1, 'GOOD', 'BAD'),
        SignVer = case(ConfigurationId == 'scid-2011' and OSPlatform startswith 'Windows', parse_json(Context)[0], 
                       ConfigurationId == 'scid-5095' and OSPlatform == 'macOS', parse_json(Context)[0], 
                       ConfigurationId == 'scid-6095' and OSPlatform == 'Linux', parse_json(Context)[0], 
        ''),
        DeviceName = toupper(tostring(split(DeviceName, '.')[0]))
| extend packed = pack(Test, Result)
| summarize Tests = make_bag(packed), SignatureData = max(SignVer), DeviceName = any(DeviceName), OSPlatform = any(OSPlatform) by DeviceId
| evaluate bag_unpack(Tests)
| extend AVSignatureVersion = tostring(parse_json(SignatureData)[0]), Date = todatetime(parse_json(SignatureData)[2]), ProductVersion = tostring(parse_json(SignatureData)[3]), EngineVersion = tostring(parse_json(SignatureData)[1])
| join kind=leftouter (DeviceInfo
| distinct DeviceId, MachineGroup, OnboardingStatus) on DeviceId
| where OnboardingStatus == "Onboarded"
| project-away SignatureData, NA, DeviceId1, EmailScanning, TamperProtection
```
<br>
참고 : https://jeffreyappel.nl/how-to-check-for-a-healthy-defender-for-endpoint-environment/

 <img width="900" height="632" alt="image" src="https://github.com/user-attachments/assets/2aee2c61-9de9-41f0-b48a-2e0ed078a52f" />
<br>

추가적으로 다음 화면에서도 만들어져 있는 대시보드들을 활용할 수 있다.
* Microsoft Defender 보안 포털(Defender XDR) 활용
  + Defender 보안 포털(https://security.microsoft.com)에서 디바이스 인벤토리 또는 보고서 메뉴를 통해조직 내 온보딩된 디바이스 현황과 에이전트 설치/미설치 상태를 확인할 수 있음
  + 설치율은 전체 디바이스 대비 온보딩(에이전트 설치 및 연결)된 디바이스의 비율로 확인 가능
* Intune 관리 콘솔 디바이스 > 모니터링 > 엔드포인트 보안 메뉴에서 Defender 에이전트가 설치된 디바이스와 그렇지 않은 디바이스를 한눈에 파악할 수 있다. 

<img width="778" height="554" alt="image" src="https://github.com/user-attachments/assets/ea03085e-b994-4fba-830d-5ed3c24b785e" />
<br>

이외 최신 업데이트 적용률, 이벤트 탐지율도 검색하여 확인할수 있다.

* Microsoft Defender for Endpoint 환경에서 에이전트가 최신 버전으로 업데이트된 디바이스의 비율을 확인하려면, Microsoft Defender XDR 포털의 고급 헌팅(Advanced Hunting) 기능에서 KQL 쿼리를 사용할 수 있음
  + 최신 에이전트 버전 기준 확인
  + 조직에서 "최신"으로 간주하는 에이전트 버전(예: MsSense.exe의 ProductVersion)을 먼저 확인
  + 최신 버전 기준은 Microsoft 공식 릴리스 정보 또는 조직의 보안 정책에 따라 다를 수 있음

* 고급 헌팅 쿼리 예시
  + 아래는 DeviceTvmSecureConfigurationAssessment 또는 DeviceInfo 테이블을 활용해 각 디바이스의 에이전트 버전을 집계하고, 최신 버전 적용 비율을 산출하는 KQL 쿼리 예시입니다.

```
let LatestVersion = "10.8760.12345.0"; // 조직에서 최신으로 인정하는 버전 입력
DeviceInfo
| summarize
    최신_버전_디바이스 = countif(Version == LatestVersion),
    전체_디바이스 = count()
| extend
    최신_업데이트_적용_비율 = todouble(최신_버전_디바이스) / todouble(전체_디바이스) * 100
```

**Version** 필드는 MsSense.exe 또는 Defender Agent의 버전 정보이며 **LatestVersion**에 최신 버전 번호로 확인하다. 

이부분에 대해서는 추가로 업데이트 예정이다.

<br><br>
 
## 🚨 6 오탐 차단시, 프로세스 차단 긴급 조치 방법 
### 💣 6.1 프로세스 차단 긴급 조치 방법
차단 해제 및 예외 처리
- Microsoft Defender XDR 포털 접속: https://security.microsoft.com
- **조치된 항목(Action Center)** 또는 **인시던트** 메뉴 이동
- 차단된 항목 선택 → **허용(Allow)** 클릭
- 허용 범위 선택
  + 파일 해시 기반
  + 경로 기반
  + 서명 기반 (신뢰할 수 있는 게시자)
- 허용 처리는 모든 디바이스에 적용되므로 신중하게 판단 필요

또는 다음 파워쉘 스크립트로 허용 처리
- (예시) Add-MpPreference -ExclusionPath "C:\Program Files\MyApp"

### 🔍 6.2 탐지 이벤트 예외 처리 방법 
Microsoft Defender for Endpoint(MDE)에서 탐지 이벤트에 대한 예외 처리는 특정 파일, 프로세스, 경로, 해시 등에 대해 탐지 또는 차단을 하지 않도록 설정한다.
* 이 작업은 오탐지 대응, 내부 도구 허용, 테스트 환경 구성 등에 사용
Defender 포털에서 직접 허용 처리 (Allow List 등록)
* Microsoft Defender XDR 포털 접속
* **인시던트** 또는 **조치된 항목(Action Center)** 메뉴 이동
*	차단된 항목 선택 → **허용(Allow)** 클릭
* 허용 기준 선택
  +	파일 해시 기반
  +	경로 기반
  +	서명 기반 (신뢰할 수 있는 게시자)

추가로 Intune 에서 예외처리를 정책 템플릿으로 추가할 수 있다.
* 경로: Endpoint security > Antivirus > Microsoft Defender Antivirus
  + 정책 템플릿에서 예외 항목 추가
    + Microsoft Defender for Endpoint 설정에서 제외 정책 구성
* Defender 설정에서 다음 항목을 예외로 지정 가능:
  + 파일 및 폴더
  + 프로세스
  + 파일 확장자
  + 네트워크 위치

<br><br>

## 🔍 7. 탐지 이벤트 로그 분석 상세 방법
#### 7.1 탐지 이벤트 상세 분석 방법
1. 탐지 이벤트 확인
* 포털 접속: https://security.microsoft.com
* 메뉴: 인시던트(Incidents) 또는 경고(Alerts)
* 각 이벤트는 다음 정보를 포함
  + 탐지된 위협 이름 
  +	탐지된 시간, 디바이스, 사용자
  +	관련된 파일, 프로세스, IP, URL 등

2. 인시던트 타임라인 분석
* 인시던트 페이지에서 타임라인을 통해 공격 흐름 확인
  + 예: 이메일 수신 → 링크 클릭 → 악성 프로세스 실행 → lateral movement
*	주요 항목:
  + 프로세스 트리 (Process Tree)
  + 파일 생성/삭제
  + 네트워크 연결
  + 사용자 로그인/세션 정보

3. 고급 헌팅(Advanced Hunting)으로 심층 분석
* 메뉴: 헌팅 > 고급 헌팅
  + KQL(Kusto Query Language)을 사용하여 관련 이벤트 추적
    * 예시: 특정 해시로 실행된 프로세스 추적
    * 예시: 동일 사용자로 실행된 모든 프로세스

4. 자동 조사 결과 확인 (Automated Investigation)
* MDE는 자동으로 다음을 조사
  + 관련 파일의 평판
  + 프로세스의 행위 분석
  + 네트워크 연결지
  + 결과는 **자동 조사** 탭에서 확인 가능

5. 샘플 분석 및 제출
* 의심 파일을 수동으로 다운로드하여 분석하거나,
  + Microsoft에 샘플 제출: https://www.microsoft.com/wdsi/filesubmission

6. 외부 위협 인텔리전스 연계
* VirusTotal, Any.run, Hybrid Analysis 등에서 해시/IP/도메인 분석
  + MDE는 Threat Intelligence와 연동되어 자동으로 평판을 제공

7. 대응 조치 및 예외 처리
* 차단, 격리, 프로세스 종료, 사용자 로그오프 등
  + 오탐일 경우 예외 처리 (허용 등록)

* 분석 시 유용한 KQL 테이블

|  테이블 이름	 |  설명  |
| --- | --- |
| DeviceProcessEvents |	프로세스 실행 정보 |
| DeviceFileEvents |	파일 생성/삭제/수정 |
| DeviceNetworkEvents |	네트워크 연결 정보 |
| AlertEvidence |	경고에 포함된 증거 항목 |
| DeviceLogonEvents |	사용자 로그인 정보 |

<br><br>

## 🧑‍🔧 8. 에이전트 장애가 발생 시 문제 해결
#### 8.1 센서 상태 문제 해결
리눅스 버전의 경우, 아래 트러블 슈팅 가이드 참고 
* 에이전트 상태 문제 조사
  + https://learn.microsoft.com/ko-kr/defender-endpoint/health-status

윈도우 버전의 경우, 아래 트러블 슈팅 가이드 참고 

*	엔드포인트용 Microsoft Defender 디바이스 상태 확인
  + https://learn.microsoft.com/ko-kr/defender-endpoint/check-sensor-status
* 엔드포인트용 Microsoft Defender 비정상 센서 수정
  + https://learn.microsoft.com/ko-kr/defender-endpoint/fix-unhealthy-sensors
*	Microsoft Defender 바이러스 백신 검사 문제 해결
  + https://learn.microsoft.com/ko-kr/defender-endpoint/troubleshoot-mdav-scan-issues

<br><br>

## 9. 에이전트 긴급 삭제 혹은 프로세스 중지 방안
#### 9.1 에이전트 중지 및 삭제 방법
1. 설정 화면에서 중지
 <img width="900" height="574" alt="image" src="https://github.com/user-attachments/assets/eff70a10-4f23-406b-b028-f39e666722dc" />




2. 이외 방법으로 -  오프보딩 패키지 다운로드
  * Microsoft 365 Defender 포털(security.microsoft.com)에 관리자 계정으로 로그인
  * 설정 > 엔드포인트 > 디바이스 관리 > 오프보딩 메뉴로 이동
  * 오프보딩할 디바이스의 운영 체제(예: 리눅스/Windows Server 등)를 선택
  * 오프보딩 패키지를 다운로드

3. 오프보딩 패키지 실행
  * 다운로드한 오프보딩 패키지를 오프보딩 대상 디바이스에 복사
  * 로컬 스크립트 실행:
    + 오프보딩 패키지 안의 스크립트(.cmd 또는 .ps1)를 관리자 권한으로 실행
  * [참고] 여러 대의 디바이스를 오프보딩할 경우, 그룹 정책(GPO), Microsoft Endpoint Configuration Manager(SCCM), Intune 등 조직의 배포 도구를 활용할 수도 있음

4. 오프보딩 결과 확인
  * 서비스 상태 확인:
    + 오프보딩이 완료되면 서비스가 중지됨

5. 에이전트 삭제 
  * 중지된 이후 제어판에서 직접 제거
    +	제어판 > 프로그램 및 기능에서
        + **Microsoft Defender for Endpoint** 또는 **Windows Defender Advanced Threat Protection**을 찾아 제거를 클릭
  *	명령줄(MSI)로 제거 (MMA 기반 환경)
    + Microsoft Monitoring Agent(MMA) 기반 환경에서는 명령 프롬프트(관리자 권한)에서 다음과 같이 입력합니다:
    +	%WinDir%\System32\msiexec.exe /x <MOMAgent.msi 경로> /qb
    +	또는, 제어판에서 *Microsoft Monitoring Agent* 선택 후 제거

이외에, 중앙 관리(SCCM/Intune)에서 정책 배포로 일괄 오프보딩 및 삭제

#### 9.2 에이전트 프로세스 중지 방법

Microsoft Defender for Server 는 화면에서 Off 로 설정하면 중지됩니다. 
<img width="900" height="574" alt="image" src="https://github.com/user-attachments/assets/1e2c1a32-c75e-4cf6-bc83-9aed559da58f" />

 


리눅스 버전 에이전트 즉시 중지는 다음과 같이 서비스 중지 명령을 활용한다. 
```
# systemctl stop mdatp
```
<img width="894" height="490" alt="image" src="https://github.com/user-attachments/assets/68634063-7822-4dbd-a76b-ffffcddd11ab" />

 


