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
8. 줄임표를 클릭하여 **정책 정의 보기**를 클릭합쳐 개선](Module-6-보안포스쳐개선하기.md)
