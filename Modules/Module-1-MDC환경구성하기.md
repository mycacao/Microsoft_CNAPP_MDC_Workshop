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
SecurityCenterFree | Solution | Default workspace solution used for Microsoft Defender for Cloud free tier

템플릿 배포 후, 생성된 리소스 그룹 세부 정보를 클릭한 다음 배포(1개 배포)를 클릭하면 배포 진행 상황을 확인할 수 있습니다.
배포가 완료될 때까지 아래 Exercise를 계속하세요.
<br><br>

<img width="1292" height="715" alt="image" src="https://github.com/user-attachments/assets/527128a1-8750-440d-ad2b-72f8ce2c06bb" />
<br>

1. 아래의 파란색 **Deploy to Azure** 버튼을 클릭하여 랩 환경을 준비하세요.:

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2FAzure-Security-Center%2Fmaster%2FLabs%2FFiles%2Flabdeploy.json" target="_blank"><img src="https://aka.ms/deploytoazurebutton"/></a>

2.	배포를 위한 필수 필드를 지정해야 하는 Azure Portal > 사용자 지정 배포 페이지로 리디렉션됩니다.
3.	구독 필드에서 **Azure Subscription 1**을 선택하세요..
4.	소스 그룹 필드에서 **새로 만들기**를 클릭하고 이름을 **asclab**으로 지정합니다(원하는 이름을 선택하거나 기본값을 유지할 수 있음).
5.	매개변수 섹션에서 현재 위치에 가장 가까운 데이터 센터 **region**을 선택합니다(모든 다운스트림 리소스는 리소스 그룹과 동일한 지역에 생성됩니다).
6. 서비스 전반에서 사용될 암호(예: 가상 머신 및 SQL 데이터베이스의 자격 증명)를 선택하세요.
> ❗ 중요: <br>
> 비밀번호는 12자에서 72자 사이여야 하며, 소문자 1개, 대문자 1개, 숫자 1개, 특수문자 1개 중 3가지를 포함해야 합니다. 이를 준수하지 않으면 배포가 실패합니다.  
7.	**Review + create**을 클릭하여 유효성 검사 프로세스를 시작합니다. 유효성 검사가 통과되면 **Create** 을 클릭하여 구독에서 ARM 배포를 시작합니다.
8.	배포가 완료되는 데는 약 **10분**이 걸립니다.<br>

> *배포 진행 중* 페이지는 계속 업데이트되며 배포가 성공적이라고 가정하고 리소스가 환경에 업로드되는 모습을 보여줍니다.  
> 배포 중에 Kubernetes 리소스에 대해 "asclab-aks"라는 이름의 추가 리소스 그룹이 자동으로 생성됩니다.<br>

<img width="600" height="600" alt="image" src="https://github.com/Azure/Microsoft-Defender-for-Cloud/blob/main/Labs/Images/deploy-to-azure.gif?raw=true"  /> 

생성된 리소스 그룹 세부 정보를 클릭한 다음 **Deployments**를 클릭하면 배포 진행 상황을 확인할 수도 있습니다(*1 배포*). <br>

<img width="600" height="600" alt="image" src="https://github.com/Azure/Microsoft-Defender-for-Cloud/blob/main/Labs/Images/asc-deployment-in-progress.gif?raw=true"  />

배포가 완료되면 다음이 표시됩니다.:

<img width="600" height="600" alt="image" src="https://github.com/Azure/Microsoft-Defender-for-Cloud/blob/main/Labs/Images/asc-deployment-completed.gif?raw=true"  />

### Exercise 3: 클라우드용 Microsoft Defender 활성화

#### 구독 업그레이드 및 에이전트 설치
1. **Azure Portal**을 열고 **Microsoft Defender for Cloud** 블레이드로 이동합니다.
2. 왼쪽 창에서 **시작하기** 페이지를 클릭하고, **업그레이드** 탭에서 구독(Azure 구독 1)을 선택하고 **활성화**를 누릅니다.
   >참고: 업그레이드가 완료될 때까지 몇 분 정도 기다려야 할 수 있습니다.
3. **Azure 구독 1**과 그 아래의 **workspace name**을 모두 선택하세요. **upgrade**를 클릭하여 업그레이드하세요.
<img width="600" height="600" alt="image" src="https://github.com/Azure/Microsoft-Defender-for-Cloud/blob/main/Labs/Images/mdfc-gettingstarted.png?raw=true"  />

#### 구독 및 Workspace 에서 Defender 적용 범위 상태를 확인하세요.
1. Microsoft Defender for Cloud 블레이드로 돌아가서 **환경 설정**을 클릭합니다. **Azure**의 아래쪽 화살표를 클릭하여 구독을 표시한 다음, **Azure 구독 1**의 아래쪽 화살표를 클릭하여 작업 영역을 표시합니다. 해당 구독의 Defender 적용 범위는 12/12 플랜입니다..
> 이전에는 Defender for Server와 Defender for SQL on Machines의 경우 Log Analytics 작업 영역에서 Defender 플랜을 활성화해야 했습니다. 기본적으로 두 플랜 모두 더 이상 Log Analytics 작업 영역을 사용할 필요가 없습니다. (Defender for SQL on Machines는 DCR 요구 사항으로 인해 작업 영역을 생성합니다.)   

2. **Azure 구독 1**을 클릭하고 모든 Microsoft Defender for Cloud 플랜이 활성화되어 있는지 확인하세요.

> 개별 plan을 활성화해야 하는 경우 먼저 오른쪽에 있는 Microsoft Defender for Cloud plan 파란색 상자가 선택되어 있는지 확인한 다음, 아래에서 특정 Defender plan을 선택할 수 있습니다.

<br>

> 주의해주세요:
> * 업그레이드 버튼을 클릭하기 전에 Microsoft Defender for Cloud를 활성화할 총 리소스 수를 검토할 수 있습니다.
> * 이전에 사용하지 않은 경우에만 구독에 대해 30일 동안 Microsoft Defender for Cloud 평가판을 활성화할 수 있습니다.
> * 구독에서 Microsoft Defender for Cloud를 활성화하려면 구독 소유자, 구독 기여자 또는 보안 관리자 역할이 할당되어야 합니다 (Subscription Owner, Subscription Contributor, or Security Admin).

### 다음 랩을 계속하세요: [Module 2 - Exploring Microsoft Defender for Cloud](../Modules/Module-2-Exploring-Azure-Security-Center.md)
