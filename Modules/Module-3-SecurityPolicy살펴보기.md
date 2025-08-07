# Azure Security Policy 살펴 보기

<p><img width="137" height="161" alt="image" src="https://github.com/user-attachments/assets/2eabc4c2-b96a-407b-be9b-63a73b066254" /></p>

#### 🎓 레벨: 200 (중급)
#### ⌛ 이 랩의 예상 완료 시간: 60분

## 목표
- 이번 랩은 현재 MDC (Microsoft Defender for Cloud)의 보안 정책(Security Policy)을 살펴봅니다.
- 보안 정책은 클라우드 보안 태세를 개선하는 데 도움이 되는 보안 표준(Standard)와 권장 사항(Recommendation)으로 구성됩니다.
- 보안 표준은 [[Microsoft 클라우드 보안 벤치마크(MCSB)](https://learn.microsoft.com/ko-kr/azure/defender-for-cloud/concept-regulatory-compliance)], 규정 준수 표준(Regulatory compliance standards) 및 사용자 지정 표준(custom standards)으로 구성됩니다.
- 이번 랩을 완료하면 예외, 정책 적용 및 사용자 지정 정책을 만드는 방법을 이해할수 있습니다.

#### 필수 구성 요소
Microsoft Defender for Cloud를 시작하려면 Microsoft Azure 구독이 필요합니다. 무료 구독을 시작하려면 [모듈 1](https://github.com/mycacao/Microsoft_CNAPP_MDC_Workshop/blob/main/Modules/Module-1-MDC%ED%99%98%EA%B2%BD%EA%B5%AC%EC%84%B1%ED%95%98%EA%B8%B0.md)을 진행하세요.  

<br><br>
---
<br><br>
#### Azure Policy 란 무엇인가?
- Azure Policy는 Azure 환경에서 리소스가 조직 표준 및 규정 준수 요구사항을 충족하는지 감사하고 강제하는 서비스입니다.
- 즉, Azure 리소스에 대한 규칙을 정의하고, 해당 규칙을 기반으로 리소스가 생성되거나 수정될 때 자동으로 평가하여 규정 준수 여부를 확인하고, 필요에 따라 조치를 취할 수 있도록 합니다
- 조직의 표준을 적용하고 리소스가 일관되게 구성되도록 보장하는 역할 수행
- https://learn.microsoft.com/ko-kr/azure/governance/policy/overview

### Azure Policy의 주요 기능
> 정책 정의: JSON 형식으로 정의된 규칙 집합으로, 리소스의 속성, 설정 및 동작을 정의합니다. </br>
> 정책 할당: 특정 범위(관리 그룹, 구독, 리소스 그룹 등)에 정책을 할당하여 해당 범위 내의 모든 리소스에 적용합니다. </br>
> 규정 준수 평가: 리소스가 정책을 준수하는지 주기적으로 평가합니다. </br>
> 효과: 정책 위반 시 리소스에 대한 조치(예: 거부, 수정, 감사)를 정의합니다.  </br>
  
<br><br>
---
<br><br>
  
### 연습 1: MDC 정책(Policy) 개요

1. Microsoft Defender for Cloud 블레이드의 왼쪽 탐색 창에서 **환경 설정**을 클릭합니다.
2. **구독 Subscription**을 선택하고 왼쪽 탐색 창에서 **보안 정책 Security Policy**을 선택합니다.

<img width="1270" height="872" alt="image" src="https://github.com/user-attachments/assets/c6a34b94-c4f4-4129-bc8b-19c709e5bb3e" />

3. **표준** 탭에 MCSB ( 현재 228개 ) 권장 사항(Recommendations) 이 표시됩니다. **유형**은 **기본값**입니다.</br>
   이는 관리 그룹 또는 구독이 Defender for Cloud에 온보딩될 때 MCSB가 기본적으로 할당되기 때문입니다.

> 참고: 앞서 언급했듯이 이는 기본값이며 Microsoft Defender for Cloud 온보딩의 일부로 자동으로 할당되었습니다.</br>
> 기본 할당에는 감사 정책(audit policies)만 포함됩니다.</br>
> 자세한 내용은 https://learn.microsoft.com/ko-kr/azure/defender-for-cloud/concept-regulatory-compliance 에서 확인 </br>
> MCSB는 Azure뿐만 아니라 다중 클라우드 환경의 보안 권장 사항과 모범 사례를 모두 모아놓은 종합적인 모음입니다.</br>

<img width="1605" height="546" alt="image" src="https://github.com/user-attachments/assets/0f38f09f-7963-435e-8bcf-f71796646d57" />

4. Assignment 할당을 클릭합니다: **Microsoft Cloud Security Benchmark**. **효과 Effect**는 **감사 Audit**입니다. </br>
   Microsoft Defender for Cloud는 사용자 환경을 평가하고 데이터를 감사합니다. 사용자의 승인 없이는 이를 시행하지 않습니다. </br>
5. **보안 정책** 페이지로 돌아갑니다. **권장 사항** 탭을 클릭합니다. **Defender for Cloud** 및 **Azure Policy**의 **소스** 변경 사항을 확인합니다. **표준** 열도 기록해 둡니다.
<img width="1663" height="745" alt="image" src="https://github.com/user-attachments/assets/ff3e8577-ec0d-454b-b8c6-3c03ab1803b9" />

📌📌📌 알아두면 좋은 정보 <br>
<img width="1058" height="550" alt="image" src="https://github.com/user-attachments/assets/25f86ae6-4d19-47a7-95fb-6fbc82ad29fa" />
  
<br><br>
---
<br><br>
    
### 연습 2: Azure 정책(Policy) 살펴보기  
1. Azure Portal에서 **정책 블레이드**로 이동합니다. 상단의 검색 상자에서 "정책"을 검색하거나 [정책](https://portal.azure.com/#view/Microsoft_Azure_Policy/PolicyMenuBlade/~/Overview) 로 이동할 수 있습니다.     
2. 왼쪽 탐색 창의 **작성 또는 제작, Authoring** 섹션에서 **정의**를 클릭하여 기본 제공 정책 정의 및 이니셔티브를 살펴보세요.     

<img width="1672" height="775" alt="image" src="https://github.com/user-attachments/assets/b20aed01-6c24-42e8-881b-8997770d5ff3" />

✨✨✨ 참고, 정책(Policy) 과 이니셔티브(Initiative) 차이점은? AI 가 잘 알려주네요 <br>
>> MDC에서 사용하는 Policy와 Initiative는 모두 Azure Policy의 개념에 기반을 두고 있으며, 보안 평가 및 규정 준수 준수를 위한 핵심 구성요소입니다.
  
| 개념                        | 설명                                                                                                                     |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| **Policy (정책)**           | 하나의 **보안 조건이나 규칙**을 정의하는 단일 정책입니다. 특정 조건을 준수하지 않을 경우 **비정상(Non-compliant)** 상태로 표시됩니다.                                 |
| **Initiative (정책 이니셔티브)** | 여러 개의 Policy를 **묶은 집합 Policy Set**입니다. 일반적으로 하나의 보안 기준(예: ISO 27001, NIST 등)을 구현하기 위해 수십\~수백 개의 Policy를 묶어 사용합니다. |

>> 다시한번 구체적으로 비교하면 다음과 같습니다.
  
| 항목    | **Policy**             | **Initiative**                               |
| ----- | ---------------------- | -------------------------------------------- |
| 구성 단위 | 하나의 규칙(예: 스토리지 암호화 필요) | 여러 규칙을 묶은 세트                                 |
| 목적    | 특정한 하나의 조건을 강제 또는 평가   | 특정 보안 기준을 광범위하게 평가/강제                        |
| 예시    | "공용 IP가 허용되면 안 된다"     | "Azure Security Benchmark", "NIST SP 800-53" |
| 사용 위치 | 단독으로 또는 이니셔티브 내 포함     | 보통 Security Policy에 사용됨                      |
| 적용 방식 | 개별 리소스나 그룹에 직접 적용 가능   | 보안 벤치마크나 규정 준수 프레임워크로 적용됨                    |
3. 상단 메뉴에서 필터 버튼을 사용하여 범주를 **보안 센터\,Security Center**로 설정하고 **모두, All**의 선택을 취소합니다. **정의 유형**에서 **이니셔티브**를 선택하고 **모두**의 선택을 취소합니다.
4. 이제 Microsoft Defender for Cloud에서 사용되는 기본 제공 이니셔티브를 볼 수 있으며, 일부는 미리 보기 버전입니다.
5. 각 이니셔티브(정책 열)에 포함된 정책 수를 확인합니다.
6. 이제 종료합니다.

<img width="1835" height="701" alt="image" src="https://github.com/user-attachments/assets/8d9c60e0-f40b-493b-a119-dd8e5b71ff4f" />
  
<br><br>
---
<br><br>
  

### 연습 3: 권장 사항에 대한 리소스 예외(exemption) 만들기

리소스 면제(exemption)를 사용하면 특정 리소스를 평가에서 제외할 수 있으므로 권장 사항을 더욱 세부적으로 조정할 수 있습니다.
권장 사항을 사용할 때 오른쪽의 줄임표 메뉴를 클릭하고 '면제 만들기(exemption)'를 선택하여 면제를 만들 수 있습니다.

🔖🔖🔖 참고: 면제는 Microsoft Defender for Cloud 고객에게 추가 비용 없이 제공되는 프리미엄 Azure 정책 기능입니다. </br>
다른 사용자에게는 향후 요금이 부과될 수 있습니다.  😱 😱 😱 😱 😱  <- 정말로???????????

1. **Microsoft Defender for Cloud 블레이드**를 열고 왼쪽 탐색 창에서 **권장 사항**을 선택합니다.
2. **Management Port** 또는 **가상 머신** (제 테스트환경에서는 가상머신으로 검색) 를 입력합니다.
3. **가상 머신에서 관리 포트를 닫아야 합니다** 또는 유사한 권장 사항(아래 캡쳐 이미지 참고) 을 선택합니다.<br>

<img width="1606" height="910" alt="image" src="https://github.com/user-attachments/assets/40962690-1e64-4489-b44b-b730e0d599e0" />

<br>
4. **영향을 받는 리소스** 목록에서 현재 리소스인 *asclab-win* 및 *asclab-linux* 또는 아무거나 선택합니다.
5. **asclab-win** 리소스를 선택한 다음 **예외 --> exemption**를 클릭합니다.

<img width="1575" height="987" alt="image" src="https://github.com/user-attachments/assets/9459562f-8a8a-4b7e-a28b-ff690e67d951" />

6. **예외 또는 제외 또는 명제 생성** 창이 열립니다.
* 기본 이름을 유지합니다.
* 만료 버튼을 클릭하고 날짜/시간을 이틀 후 오전 12시로 설정합니다.
- 면제 범주로 **면제**를 선택합니다.
- 설명을 입력합니다: **예외 면제 기능 테스트 - 모듈 3**.
- **저장**을 선택합니다.

<img width="1801" height="1031" alt="image" src="https://github.com/user-attachments/assets/bd7a9e19-391a-4eb9-9149-13debe5a4505" />

📌 [참고] 완화 한다는것과 면제(또는 예외,제외로 번역) 한다는 것 의 차이점
> **완화** - 이 문제는 제안된 것과 다른 도구 또는 프로세스로 처리되었으므로 해당 리소스와 관련이 없습니다.
> **면제** - 이 리소스에 대한 위험 감수

7. 면제가 적용되는 데 최대 **30분**이 소요될 수 있습니다. 면제 적용 후:
- 리소스는 보안 점수에 영향을 미치지 않습니다.
- 리소스는 권장 사항 세부 정보 페이지의 '해당 없음' 탭에 나열됩니다.
- 권장 사항 세부 정보 페이지 상단의 정보 스트립에 면제된 리소스 수가 **1**로 표시됩니다.

<img width="1807" height="699" alt="image" src="https://github.com/user-attachments/assets/6543c12f-32cd-4c32-8d09-b33f14bf8091" />

8. **해당 없음** 탭을 열어 면제된 리소스를 검토합니다. 리소스와 사유/설명 값을 확인할 수 있습니다.
9. 면제 규칙은 Azure Policy 기능을 기반으로 합니다. 따라서 Azure Policy 블레이드에서도 모든 면제를 추적할 수 있습니다.
10. **Azure Policy 블레이드**로 이동하여 왼쪽 탐색 창에서 **면제**를 선택합니다. 새로 만든 면제 항목이 거기에 나열되어 있는지 확인하세요.

📌 [참고] 여러개를 한번에 예외 적용할 수 있습니다.
<img width="1852" height="885" alt="image" src="https://github.com/user-attachments/assets/5fd80cc2-5fdf-4531-95c1-958bcd646340" />

<br><br>
---
<br><br>
  
### 연습 4: 정책 적용 및 거부 만들기

1. **Microsoft Defender for Cloud 사이드바**에서 **권장 사항**을 선택합니다.
2. **저장소 계정으로의 보안 전송을 활성화해야 합니다**를 검색합니다.
   
<img width="1622" height="748" alt="image" src="https://github.com/user-attachments/assets/b1b80961-67a5-4471-83ba-c4e51ed02000" />

3. 상단 메뉴 모음에서 **거부** 버튼을 클릭합니다. *적용 및 거부 옵션은 보안 구성 오류를 방지하여 점수를 높이는 또 다른 방법입니다*.

> ❗ [중요] 
> 보안 구성 오류는 보안 사고의 주요 원인입니다.

4. **거부 - 리소스 생성 방지**에서 **Azure 구독 1**(현재 감사 모드로 설정됨)을 선택합니다. 이렇게 하면 지금부터 보안 전송 기능이 활성화되지 않은 저장소 계정은 거부됩니다.

<img width="1647" height="1026" alt="image" src="https://github.com/user-attachments/assets/d85d3499-48f9-4b92-adf6-5f77d23e9b85" />


다시 감사로 변경하려면 아래와 같이 합니다.
<img width="1819" height="1028" alt="image" src="https://github.com/user-attachments/assets/00a605c8-e5a0-475d-9e71-948ff41d2c58" />

5. **권장 사항** 보기로 돌아가서 거부 전용 필터를 제거합니다. 검색 영역에 **감사**를 입력합니다. **SQL 서버에서 감사를 활성화해야 합니다**라는 권장 사항을 클릭합니다.
6. 
![Auditing on SQL server should be enabled](../Images/asc-auditing-sql.gif?raw=true)

7. 권장 사항 페이지의 상단 메뉴 모음에서 **적용** 버튼을 클릭합니다. 이 옵션을 사용하면 Azure 정책의 DeployIfNotExist 효과를 활용하여 비준수 리소스가 생성되는 즉시 자동으로 수정할 수 있습니다.

<img width="1830" height="1044" alt="image" src="https://github.com/user-attachments/assets/c1309efd-a7be-4e8c-a141-b69cd54052a2" />

8. 모든 정책 구성 옵션이 포함된 구성 창이 열리면 다음 구성 설정을 선택합니다.

* 범위에서 구독을 선택합니다. **선택**을 클릭합니다.
* **다음**을 클릭합니다.
* 보존 기간을 그대로 유지하고 리소스 그룹 **asclab**을 선택합니다.
****검토 및 만들기**를 선택하여 구독에 정책을 할당합니다.
* **만들기**를 클릭합니다.

9. 권장 사항 페이지에서 **비정상 리소스** 탭(asclab-sql-xxx)에 있는 SQL Server 리소스를 **선택**하고 **수정**을 클릭합니다. **리소스 1개 수정**을 클릭합니다. 두 작업을 모두 수행하면 기존 리소스와 새 리소스 모두 감사 대상에 포함될 수 있습니다. SQL Server 감사 기능을 사용하면 서버의 모든 데이터베이스에서 데이터베이스 활동을 추적하고 감사 로그에 저장할 수 있습니다.
10. 보안 점수 보안 제어 및 권장 사항 목록을 검토하려면 🔔 [여기를 클릭하세요](https://learn.microsoft.com/ko-kr/azure/defender-for-cloud/secure-score-security-controls) 🔔
  
<br><br>
---
<br><br>
  
### 연습 5: 사용자 지정 권장 사항(Custom Recommendation) 만들기

***KQL 쿼리를 사용하여 사용자 지정 이니셔티브 만들기***
이 연습에서는 기존 권장 사항([미리 보기]: 저장소 계정의 공용 액세스를 허용하지 않아야 함)을 사용하여 사용자 지정 권장 사항을 만듭니다.
1. 구독의 **보안 정책**으로 이동합니다.
2. 상단의 **+만들기** 드롭다운에서 **권장 사항 만들기**를 선택합니다.
<img width="1728" height="714" alt="image" src="https://github.com/user-attachments/assets/34d4df0f-266b-4b20-8b46-cd14cf14e044" />

3. **새 권장 사항 만들기** 페이지에서 다음을 입력합니다.
- 이름: customrecommendation_module3
- 설명: [미리 보기]: 저장소 계정의 공용 액세스를 허용하지 않아야 함
- 수정 설명: Azure Storage의 컨테이너 및 BLOB에 대한 익명의 공용 읽기 액세스는 데이터를 공유하는 편리한 방법이지만 보안 위험을 초래할 수 있습니다. 원치 않는 익명 액세스로 인한 데이터 침해를 방지하기 위해 Microsoft는 상황에 따라 필요하지 않은 경우 저장소 계정에 대한 공용 액세스를 차단할 것을 권장합니다.
- 심각도: 높음
- 보안 문제: 익명 액세스

<img width="952" height="590" alt="image" src="https://github.com/user-attachments/assets/ce0de5a2-93ab-4d10-87f5-e84ea8a34d6b" />

4. 쿼리 편집기를 사용하여 KQL 쿼리를 작성하거나 테스트합니다. 완료되면 **권장 사항 쿼리**에 쿼리를 추가합니다.

<img width="1645" height="953" alt="image" src="https://github.com/user-attachments/assets/7465a05e-e41e-4a61-b5a7-c8fcfb319fb0" />

5. **다음**을 선택합니다. **저장**을 클릭합니다.
<img width="950" height="506" alt="image" src="https://github.com/user-attachments/assets/0f1c11ad-8b78-4ff3-be82-de72972b4283" />

6. 몇 분 후 구독 아래의 **보안 정책**으로 돌아갑니다.
7. **권장 사항** 탭을 클릭하면 방금 만든 사용자 지정 정책이 표시됩니다.

<img width="1406" height="571" alt="image" src="https://github.com/user-attachments/assets/d7396ad8-a6a6-4080-b21d-c1ed8601432b" />

이 [페이지](https://learn.microsoft.com/en-us/azure/defender-for-cloud/create-custom-recommendations)를 방문하여 사용자 지정 권장 사항 및 표준에 대해 자세히 알아보세요.
  
<br><br>
---
<br><br>

### 다음 랩을 계속 진행하세요: [모듈 4 - 규정 준수](../Modules/Module-4-Regulatory-Compliance.md)
