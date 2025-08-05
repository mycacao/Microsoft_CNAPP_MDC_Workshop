# Azure Security Policy 살펴 보기

<p><img width="137" height="161" alt="image" src="https://github.com/user-attachments/assets/2eabc4c2-b96a-407b-be9b-63a73b066254" /></p>

#### 🎓 레벨: 200 (중급)
#### ⌛ 이 랩의 예상 완료 시간: 60분

## 목표
이 연습에서는 현재 Microsoft Defender for Cloud의 보안 정책을 안내합니다. 이러한 보안 정책은 클라우드 보안 태세를 개선하는 데 도움이 되는 보안 표준과 권장 사항으로 구성되어 있습니다. 보안 표준은 [Microsoft 클라우드 보안 벤치마크(MCSB)](https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-regulatory-compliance), 규정 준수 표준 및 사용자 지정 표준으로 구성됩니다.
이 연습을 마치면 예외, 정책 적용 및 사용자 지정 정책을 만드는 방법을 알게 됩니다.

#### 필수 구성 요소
Microsoft Defender for Cloud를 시작하려면 Microsoft Azure 구독이 필요합니다. 무료 구독을 시작하려면 [모듈 1](https://github.com/Azure/Microsoft-Defender-for-Cloud/blob/main/Labs/Modules/Module-1-Preparing-the-Environment.md)을 진행하세요.

### Azure Policy 란?

> Azure Security Policy는 Azure 리소스에 대한 거버넌스 및 규정 준수를 강화하기 위한 도구로, 정책 정의를 통해 리소스의 속성을 제어하고, 비즈니스 규칙을 적용하며, 규정 준수 상태를 평가합니다.
> 즉, 조직의 표준을 적용하고 리소스가 일관되게 구성되도록 보장하는 역할 수행

### Azure Security Policy의 주요 기능:
> 정책 정의:
- JSON 형식으로 정의된 규칙 집합으로, 리소스의 속성, 설정 및 동작을 정의합니다.
> 정책 할당:
- 특정 범위(관리 그룹, 구독, 리소스 그룹 등)에 정책을 할당하여 해당 범위 내의 모든 리소스에 적용합니다.
> 규정 준수 평가:
- 리소스가 정책을 준수하는지 주기적으로 평가합니다.
> 효과:
- 정책 위반 시 리소스에 대한 조치(예: 거부, 수정, 감사)를 정의합니다. 
### Azure Security Policy를 사용하는 이유:
- 규정 준수: 다양한 규제 및 산업 표준을 준수하도록 지원합니다. 
- 보안 강화: 조직의 보안 정책을 일관되게 적용하여 보안 위험을 줄입니다. 
- 비용 절감: 리소스 구성 오류 및 낭비를 방지하여 비용을 절감합니다. 
- 운영 효율성 향상: 일관된 구성을 통해 운영 및 관리 효율성을 높입니다.

https://learn.microsoft.com/ko-kr/azure/governance/policy/overview

---


