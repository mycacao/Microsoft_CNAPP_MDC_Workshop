# MDC 테스트를 위한 환경 구성
# Module 1 – Preparing the Environment

<img width="121" height="161" alt="image" src="https://github.com/user-attachments/assets/bc755e47-c2ed-467f-bdc1-bafefef05b37" />

#### 🎓 Level: 100 (Beginner)
#### ⌛ Estimated time to complete this lab: 30 minutes

## 목표
Azure 평가판 구독을 통해 새 Microsoft 계정을 만드세요.
이 섹션은 Azure 리소스를 자동화된 방식으로 배포하여 빠르게 시작하거나 환경을 다시 프로비저닝해야 하는 경우에 도움이 되도록 작성되었습니다.

#### Prerequisites
이 랩을 시작하기 전에 다음 전제 조건이 충족되었는지 확인하세요.:
- **지원되는 웹 브라우저** (Microsoft Edge, Google Chrome, Safari, Firefox Mozilla)
    - 이러한 랩을 사용하려면 컴퓨터에서 **시크릿 모드/비공개 브라우저 세션**을 열고 Azure Portal에 로그인하여 기존 Azure 구독/환경(이미 사용 중인 경우)과의 충돌을 방지하는 것이 좋습니다.
 - **Microsoft Account** - 기존 계정이 없으신 경우 무료 계정을 생성하기 위해 가입하세요: https://signup.live.com
  

### Exercise 1: Azure 평가판 구독 만들기

이러한 랩을 사용하려면 Azure 구독 평가판이 있어야 합니다. 이를 통해 다음을 수행할 수 있습니다.:
- **12개월 무료 상품** - 처음 30일 동안 가상 머신, 스토리지, 데이터베이스와 같은 인기 제품에 무료로 액세스할 수 있으며, 계정을 종량제 가격으로 업그레이드한 후 12개월 동안 무료로 액세스할 수 있습니다..
- £150 credit/$200 credit - 무료 제품 금액 외에도 최초 30일 동안 모든 Azure 서비스를 실험해 보려면 크레딧을 사용하세요.
- **자동 청구 없음** –등록 과정 중에 신원 확인 과정을 완료하기 위해 신용 카드 정보를 입력해야 합니다. 
> ⚠️ 경고:구독을 업그레이드하지 않는 한 요금이 청구되지 않습니다.
첫 30일이 끝나기 전에 알림을 받고 업그레이드하여 무료 용량을 초과하여 사용하는 리소스에 대해서만 비용을 지불할 수 있는 기회가 제공됩니다.

#### Instructions:
1. 웹 브라우저에서 **In-Private** 세션을 열고 다음으로 이동합니다. https://azure.microsoft.com/en-us/free
2. 이 페이지의 주요 부분에서 **무료로 시작**을 클릭하고 Microsoft 계정 자격 증명을 사용하여 Azure Portal에 로그인합니다.
중요 - 회사 사용자로 로그인하지 않았는지 확인하세요.
3. Microsoft 계정 이메일 주소를 입력한 후 **다음**을 클릭하세요.
4. **로그인 상태 유지** 메시지에서 **예**를 클릭합니다.
5. **Azure 무료 체험** 페이지에서 4단계(프로필, 전화 신원 확인, 카드 신원 확인, 계약)에 따라 정보를 입력하세요. 모든 단계를 완료한 후 **가입** 버튼을 클릭하여 구독 생성 절차를 완료하세요.
6. **Azure 시작 준비 완료** 페이지에서 **포털로 이동** 버튼을 클릭하세요. 이제 **Azure subscription 1**이라는 Azure 구독이 소유자 권한과 함께 생성되어야 합니다.

### Exercise 2: 리소스 프로비저닝

> ❗ 중요: <br>
> Microsoft Defender for Cloud 랩도 동일한 비공개 창에서 접속해야 합니다. 그렇지 않으면 랩 링크가 비공개가 아닌 다른 창에서 열립니다. 

이 랩 가이드에 언급된 연습의 일부로 ARM 템플릿을 기반으로 하는 자동화된 배포를 사용하여 환경을 생성합니다.
ARM 템플릿은 프로젝트의 인프라와 구성을 정의하는 JSON(JavaScript Object Notation) 파일입니다.
이 템플릿은 선언적 구문을 사용하므로, 프로그래밍 명령을 직접 작성하지 않고도 배포하려는 항목을 명시할 수 있습니다..
다음 리소스 목록은 프로비저닝 프로세스 중에 배포됩니다(디스크, 네트워크 인터페이스, 공용 IP 주소 등의 종속성 포함):

이름 | 리소스 유형 | 목적
-----| ------------- | -------
asclab-win | Virtual machine | Windows 서버
asclab-linux | Virtual machine | Linux 서버
asclab-as | Availability set | Availability set for the 2-VMs
asclab-aks | Kubernetes service | Testing container services capabilities
asclab-app-[uniqestring] | App Service | App service to be used for web app, function app
asclab-sql-[uniqestring] | SQL server | To be using for the sample database
asclab-as | SQL database | Sample database based on AdventureWorks template
asclab-kv-[uniqestring] | Key vault | Demonstrating Key Vault related recommendations and security alerts
asclab-fa-[uniqestring] | Function App | Demonstrating related built-in and custom security recommendations
asclab-la-[uniqestring]	| Log Analytics workspace | Log Analytics workspace used for data collection and analysis, storing logs and continuous export data
asclab-nsg | Network security group | Required for Just-in-Time access and security recommendations
asclab-splan | App Service plan | Demonstrating related security recommendations
asclab-vnet | Virtual network | Default virtual network for both Azure VM and for network related recommendations
asclabcr[uniqestring] | Container registry | Demonstrating related security recommendations
asclabsa[uniqestring] | Storage account | Demonstrating related security recommendations
SecurityCenterFree | Solution | Default workspace solution used for Microsoft Defender for Cloud free tie기](../Modules/Module-2-MDC메뉴 살펴보기.md)
