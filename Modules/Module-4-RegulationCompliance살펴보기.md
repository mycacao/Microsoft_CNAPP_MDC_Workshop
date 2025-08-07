# Module 4 - 규정 준수 (Regulatory Compliance) 관리 

<p align="left"><img width="137" height="161" alt="image" src="https://github.com/user-attachments/assets/27ca622c-6128-4310-be1b-50a8a3f93d9f" /></p>

#### 🎓 레벨: 200 (중급)
#### ⌛ 이 랩의 예상 완료 시간: 60분

## 목표
이 랩에서는 MDC 의 현재 제공하는 규정 준수 기능을 안내합니다. MDC는 규정 준수 대시보드를 통해 특정 표준(Standard)에 따라 리소스의 상태를 평가하여 고객이 이러한 요구 사항을 충족할 수 있도록 지원합니다. <br>
이 랩은 기능 위주로 안내하지만, 공식 문서는 이 [페이지](https://learn.microsoft.com/ko-kr/azure/defender-for-cloud/regulatory-compliance-dashboard) 를 참고하세요

<br><br>
---
<br><br>

### 연습 1: 규정 준수 대시보드 이해

1. **MDC 기본 대시보드**에서 **규정 준수** 타일을 선택합니다 (이 타일은 클라우드 보안 아래의 사이드바에서도 사용할 수 있습니다).
2. 규정 준수 대시보드가 열립니다. 이 페이지에서 현재 구독에 할당된 규정 준수 표준을 확인할 수 있습니다.
3. 상단 스트립에서 Microsoft 클라우드 보안 벤치마크에 대한 **통과된 컨트롤**의 수를 확인하세요.
   
<img width="1707" height="980" alt="image" src="https://github.com/user-attachments/assets/3d3949cc-d12f-440e-a2f3-032835ebd302" />
<br><br>
<img width="1275" height="945" alt="image" src="https://github.com/user-attachments/assets/21e5be9a-18fb-43b9-ae1e-72978d6a3402" />

<br><br>
---
<br><br>

### 연습 2: Azure 및 멀티클라우드에 새로운 표준 추가

IST SP 800-53 R4, SWIFT CSP CSCF-v2020, 영국 공식 표준 등과 같은 추가 산업 표준(규정 준수 패키지로 표시됨)을 추가할 수 있습니다.

1. 규정 준수의 상단 메뉴 모음에서 **규정 준수 정책 관리**를 선택합니다.


<img width="1787" height="766" alt="image" src="https://github.com/user-attachments/assets/16f8921a-9bc4-4b22-b1f7-061bf9bae661" />

2. 구독을 선택합니다.
<br> 참고: <br>
AWS 또는 GCP에서 표준을 할당하려면 AWS 또는 GCP 연결을 선택한 다음 왼쪽의 **보안 정책**으로 바로 이동합니다. 세 클라우드 모두에서 사용 가능한 규정 준수 표준은 [여기](https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-regulatory-compliance-standards#available-compliance-standards)에 문서화되어 있습니다.
<br> 추가 참고 사항: <br>
모듈 [10](https://github.com/Azure/Microsoft-Defender-for-Cloud/blob/main/Labs/Modules/Module-10-GCP.md) 및 [11](https://github.com/Azure/Microsoft-Defender-for-Cloud/blob/main/Labs/Modules/Module-11-AWS.md)에서 이러한 멀티클라우드 커넥터를 생성하는 방법을 안내합니다. 해당 모듈로 이동한 후 다시 돌아와도 됩니다.
3. **보안 정책**을 선택합니다.
4. **표준** 탭에서 *CIS Microsoft Azure Foundations Benchmark v2.0.0*을 찾습니다.
5. 표준을 선택합니다.
6. **감사** 및 **수동** 정책 정의의 개수를 확인하세요. 
<img width="1656" height="745" alt="image" src="https://github.com/user-attachments/assets/617ca0ff-a36f-45e3-b24a-906719988883" />
<br><br><br>
> **감사 효과**: 리소스가 특정 정책 정의를 준수하지 않으면 정책은 해당 리소스를 **비준수**로 표시하고 활동 로그에 경고를 생성하지만 실제 리소스에 대한 조치는 취하지 않습니다. 
>> 감사 효과에 대한 자세한 내용은 이 [페이지](https://learn.microsoft.com/en-us/azure/governance/policy/concepts/effect-audit)를 참조하세요.
>**수동 효과**: 일부 작업이나 작업을 자동화할 수 없거나 리소스의 규정 준수 상태 업데이트가 필요한 경우 수동 증명이 필요합니다. 
>> 자세한 내용은 이 [페이지](https://learn.microsoft.com/en-us/azure/governance/policy/concepts/effect-manual)를 참조하세요.  

7. **감사** 및 **수동** 정책 정의의 개수를 확인하세요.<br> 검색 상자에서 **순환 또는 rotation **을 검색합니다. **키에는 생성 후 지정된 일수 내에 순환이 예약되도록 하는 순환 정책이 있어야 합니다.**라는 메시지가 표시됩니다. **추가 매개변수**가 **구성됨**으로 설정되어 있습니다.
8. 줄임표를 클릭하여 **정책 정의 보기**를 클릭합니다.
<p align="left"><img width="1821" height="478" alt="image" src="https://github.com/user-attachments/assets/fa0a3463-e05c-4576-9ed3-25c34c5e6919" /></p>
<p align="left"><img width="1533" height="978" alt="image" src="https://github.com/user-attachments/assets/479f8d7c-be7e-4e5a-9c45-74c8ae6a6cac" /></p>

이 표준을 범위(구독 또는 관리 그룹)에 할당하면 이 정책 정의에 따라 키 순환 최대 일 수 값을 입력하라는 메시지가 표시됩니다.

9. **표준** 페이지로 돌아가서 *CIS Microsoft Azure Foundations Benchmark v2.0.0*에 대해 **켜짐** 토글을 클릭합니다.

10. 조직의 정책을 준수하는 값을 입력하거나, 이 랩 목적으로만 **30**을 입력합니다.
11. 몇 시간 후, 이 새 표준이 기본 MCSB 옆의 **규정 준수** 대시보드에 표시됩니다.  

<p align="left"><img width="1632" height="725" alt="image" src="https://github.com/user-attachments/assets/55973eb2-05fb-4553-b22d-c3b425536456" /></p>

> ⏰ 중요: <br>
> 변경 사항이 적용되기까지 시간이 다소 소요됩니다(2~3시간)
  
<br><br>
---
<br><br>

### 연습 3: 벤치마크 살펴보기
1. 연습 2에서 선택한 표준으로 이동합니다. 이 랩에서는 *CIS Microsoft Azure Foundations Benchmark v2.0.0*을 선택했습니다. 평가에 매핑된 다양한 규정 준수 제어를 확인하세요.
2. **저장소 계정으로의 보안 전송을 활성화해야 합니다.**를 검색합니다.
3. **저장소 계정으로의 보안 전송을 활성화해야 합니다.**를 클릭하여 엽니다.
4. 새 창에서 asclabXXXXXX라는 비정상 리소스의 확인란을 선택하고 페이지 하단의 **수정**을 선택합니다.
5. 팝업 탭에서 리소스 1개 수정을 클릭합니다. 이제 저장소 계정의 보안 전송이 활성화되었습니다.

==> 현재 내 테스트 환경에서 미준수로 되어 있는게 1가지 밖에 없어서 이 화면으로 캡쳐합니다.\" SQL 서버의 감사 보존 기간을 90일 이상으로 설정해야 합니다.\"
<img width="1621" height="857" alt="image" src="https://github.com/user-attachments/assets/ff980a46-e5bf-4992-a632-728014d7f846" />  
<img width="1323" height="936" alt="image" src="https://github.com/user-attachments/assets/5a6edfc9-3b62-41cb-bb4e-db8c7259242c" />

6. 대시보드로 돌아갑니다. 규정 표준 준수 상태를 PDF 보고서 또는 CSV 파일로 내보낼 수 있습니다. 상단 메뉴 모음에서 **보고서 다운로드**를 선택합니다.
<img width="1826" height="892" alt="image" src="https://github.com/user-attachments/assets/00700bd7-481e-4943-a726-b640270d1a12" />

7. 보고서 표준 드롭다운 메뉴에서 *CIS Microsoft Azure Foundations Benchmark v2.0.0* 및 **PDF**를 선택합니다. **다운로드**를 클릭하세요.
8. 로컬 PDF 파일이 컴퓨터에 저장되었습니다. **CIS Microsoft Azure Foundations Benchmark v2.0.0**을 열고 규정 준수 보고서를 살펴보세요. 이 보고서는 사용자 환경에서의 평가 상태를 요약하며, 관련 제어와 매핑됩니다.

<br><br>
---
<br><br>

### 연습 4: 나만의 벤치마크 만들기!
간단하게 설명하기 위해, 직접 "벤치마크"를 만들 수도 있지만, 이 연습에서는 "표준"이라는 용어를 사용합니다. 표준은 하나 이상의 권장 사항으로 구성될 수 있습니다.
사용자 지정 표준을 만들면 Defender for Cloud에서 보안 정책으로 추가할 수 있으며, 이는 두 가지 주요 이점을 제공합니다.
* 보안 요구 사항을 권장 사항 목록에 사용자 지정 권장 사항으로 표시합니다.
* 규정 준수 대시보드를 사용하여 규정 준수 상태를 추적할 수 있습니다.
1. Defender for Cloud에서 규정 준수로 이동합니다.
2. 상단 메뉴에서 **규정 준수 표준 관리**를 선택하여 사용자 지정 표준을 만듭니다.
3. 새 정의의 위치로 범위를 선택합니다. 할당된 관리 그룹이 있는 경우 해당 그룹을 선택하는 것이 좋지만, 이 시나리오에서는 구독을 범위로 선택합니다.
4. **보안 정책**을 선택합니다.
5. 상단의 **+만들기** 드롭다운에서 **+사용자 지정 표준**을 클릭합니다.

<img width="1352" height="427" alt="image" src="https://github.com/user-attachments/assets/2cb85142-5046-42b9-9929-30f321d54ecb" />


6. "사용자 정의 보안 표준 - 그룹 보안"과 같은 이름을 입력하세요.
<img width="756" height="326" alt="image" src="https://github.com/user-attachments/assets/e30d9d0a-d2e4-4773-8d7c-a920b5458347" />

7. 설명을 추가하세요.
8. 이제 이 표준에 포함할 다양한 권장 사항을 선택할 수 있습니다.
9. **만들기**를 클릭하세요.
10. **보안 정책** 페이지로 리디렉션됩니다. **상태**별로 정렬하여 새로 생성된 표준이 구독에 적용된 것을 확인하세요.
<img width="1272" height="375" alt="image" src="https://github.com/user-attachments/assets/0bafa569-44bf-4ca6-ab29-c173f31994bb" />



<br><br>
---
<br><br>

### 연습 5 Azure 감사 보고서

이제 Microsoft Defender for Cloud에서 규정 준수 표준에 대한 감사 보고서를 쉽게 만들고 다운로드할 수 있습니다.
1. Microsoft Defender for Cloud의 사이드바에서 규정 준수를 선택합니다.
2. 페이지 상단의 감사 보고서를 클릭합니다.
<img width="1492" height="868" alt="image" src="https://github.com/user-attachments/assets/9622b023-2af8-4d7e-bedb-9389cd7b80d5" />
3. 탭에서 PCI를 선택하고 2021 - Azure PCI 3DS 1.0 패키지를 다운로드한 후 다운로드를 클릭합니다.
<img width="1721" height="643" alt="image" src="https://github.com/user-attachments/assets/70cb840b-1601-4dfc-a8e7-7553f9cc0dc3" />
4. 나타나는 개인정보처리방침 팝업에서 다운로드를 클릭합니다.
이제 감사 보고서가 다운로드되었습니다.


<br><br>
---
<br><br>

### 연습 6 연속 내보내기 및 시간 경과에 따른 규정 준수 통합 문서

시간 경과에 따른 규정 준수 대시보드는 Microsoft Defender for Cloud의 통합 문서로, 구독의 규정 준수 여부를 추적하는 데 사용됩니다. 자세한 내용은 [여기](https://learn.microsoft.com/en-us/azure/defender-for-cloud/custom-dashboards-azure-workbooks#compliance-over-time-workbook)를 참조하세요. 이 통합 문서를 활용하려면 먼저 Log Analytics 작업 영역으로 데이터를 내보내도록 연속 내보내기를 구성해야 합니다.
1. Microsoft Defender for Cloud의 사이드바에서 **환경 설정**을 선택합니다.
2. 데이터 내보내기를 구성할 구독을 선택합니다.
3. 해당 구독의 설정 페이지 사이드바에서 **연속 내보내기**를 선택합니다.
4. **Log Analytics 작업 영역**을 클릭합니다. 내보내기 사용을 **켜기**(이벤트 허브 옆 탭)로 설정합니다.
5. 설정을 그대로 둡니다. **규정 준수** 옆의 확인란을 선택하고 **모두 선택**을 선택합니다.
6. 내보내기 빈도 옵션에서 **스트리밍 업데이트**와 **스냅샷**을 모두 선택합니다.
7. 대상 작업 공간과 리소스 그룹을 이전에 생성한 리소스 그룹으로 선택합니다.
9. 저장을 선택합니다. Sentinel 알림 커넥터가 이미 활성화되었다는 메시지가 표시될 수 있습니다. **확인**을 클릭합니다.
10. 첫 번째 스냅샷이 생성될 때까지 기다립니다.
<img width="1753" height="1022" alt="image" src="https://github.com/user-attachments/assets/dffd3892-c2c8-4d5f-b028-6dc2534a6bf1" />

🎴[참고] Micrisoft Sentinel (SIEM) 에서 확인 

<img width="1647" height="997" alt="image" src="https://github.com/user-attachments/assets/997107ba-6b58-44a5-afc5-27fbcf5d9af7" />
<img width="1837" height="966" alt="image" src="https://github.com/user-attachments/assets/34c2cd82-c9ec-46a5-bee5-0b6f3b931c2f" />


시간 경과에 따른 규정 준수 대시보드
1. Microsoft Defender for Cloud로 이동하여 왼쪽 탐색 창의 **일반** 섹션에서 **통합 문서** 단추를 선택합니다.
2. **Defender for Cloud** 아래에 있는 **시간 경과에 따른 규정 준수** 통합 문서를 선택합니다.
<img width="1801" height="846" alt="image" src="https://github.com/user-attachments/assets/110eaa9a-6e63-4b6b-89fe-6b6412789e08" />


3. 작업 영역에서 **asclab-la-XXXXXXXXXX**를 선택합니다.
4. 구독에서 구독을 선택합니다.
5. 표준 이름에서 **모두**를 선택하면 통합 문서가 표시됩니다.
<img width="1815" height="1047" alt="image" src="https://github.com/user-attachments/assets/80c4f996-a0c9-4597-b7f1-fe2ee1b708b1" />


>참고 1: 시간 경과에 따른 규정 준수 통합 문서가 작동하려면 Log Analytics 작업 영역으로의 연속 내보내기 설정 연습을 완료해야 합니다.
>참고 2: 아래 오류가 표시되는 경우, 연속 내보내기를 통해 이 통합 문서에 데이터가 입력될 때까지 일주일 정도 기다려야 합니다.
<img width="1636" height="1050" alt="image" src="https://github.com/user-attachments/assets/3449a1ea-2aca-4800-a715-138127dd04d1" />
<img width="1553" height="1025" alt="image" src="https://github.com/user-attachments/assets/3816282c-0604-4ffa-860b-96a1a9a385ad" />

<br><br>
---
<br><br>

### 다음 랩을 계속 진행하세요: [모듈 5 - 보안 자세 개선](../Modules/Module-5-Improving-your-Secure-Posture.md)
