# Module 5 - 보안 태세(Secuirty Posture) 개선하기

<p align="left"><img width="128" height="161" alt="image" src="https://github.com/user-attachments/assets/975c25d1-fc20-4cb7-91c8-7990152606ce" /></p>

#### 🎓 레벨: 300 (고급)
#### ⌛ 이 랩의 예상 완료 시간: 60분

## 목표
이 연습에서는 가상 머신 및 컨테이너에 대한 취약성 평가와 자동화 및 데이터 쿼리를 사용하는 방법을 안내합니다.

### 연습 1: VM 취약성 평가

Microsoft Defender for Cloud for Servers를 사용하면 추가 구성이나 비용 없이 통합 취약성 평가 솔루션(Qualys 기반)을 빠르게 배포할 수 있습니다. 취약성 평가 스캐너가 배포되면 가상 머신에 설치된 모든 애플리케이션을 지속적으로 평가하여 취약성을 발견하고 그 결과를 Microsoft Defender for Cloud 콘솔에 표시합니다. *취약성* 평가 솔루션이 배포되지 않은 머신이 발견되면 Microsoft Defender for Cloud는 *머신에 취약성 평가 솔루션이 있어야 합니다*라는 권장 사항을 생성합니다. 리소스를 수정하려면 "빠른 수정" 버튼을 클릭하여 필요한 VM 확장 프로그램을 배포할 수 있습니다.

**취약성 평가 권장 사항 살펴보기:**

1. Microsoft Defender for Cloud 사이드바에서 **권장 사항**을 클릭합니다.
2. **취약성 해결** 보안 제어(보안 취약성과 관련된 모든 권장 사항 포함)를 실행합니다.
3. *시스템에 취약성 평가 솔루션이 있어야 함* 권장 사항이 있는지 확인합니다. 목록에 이 권장 사항이 없는 경우, 권장 사항이 평가와 함께 제공되기까지 24시간이 걸릴 수 있습니다.
4. **"시스템에 취약성 평가 솔루션이 있어야 함" 권장 사항**을 엽니다. 이 권장 사항은 원하는 VM에 VM 확장을 배포할 수 있는 빠른 수정 권장 사항입니다.
5. **수정 단계** 실행 - 빠른 수정 수정 옵션 외에도 **빠른 수정 로직 보기** 옵션을 사용하여 자동 수정 스크립트 콘텐츠(ARM 템플릿)를 표시할 수 있습니다. **이 창을 닫습니다.**
6. "비정상" 탭에서 *asclab-win* 및 *aslab-linux* 가상 머신을 모두 선택합니다. **수정**을 클릭합니다.
7. **취약성 평가 솔루션 선택**에서 **권장: Qualys 기반 ASC 통합 취약성 스캐너 배포(Microsoft Defender for Cloud 서버용 포함)**를 선택합니다. **진행**을 클릭합니다.
8. 창이 열리면 VM 목록을 검토하고 **리소스 2개 수정** 버튼을 클릭합니다.
9. 수정이 진행 중입니다. Microsoft Defender for Cloud가 선택한 VM에 Qualys VM 확장을 배포하므로 알림 영역이나 Azure 활동 로그를 사용하여 상태를 추적하세요. 프로세스가 완료될 때까지 5~10분 정도 기다리세요.

> Note: You can find a list of supported operating systems [here](https://docs.microsoft.com/en-us/azure/security-center/deploy-vulnerability-assessment-vm#deploy-the-integrated-scanner-to-your-azure-and-hybrid-machines).

10. VM 확장이 관련 머신에 배포되었는지 확인합니다.
- Azure Portal에서 **Virtual Machines**를 엽니다.
- **asclab-win**을 선택합니다.
- 사이드바에서 **확장**을 클릭합니다.
- `MDE.Windows` 확장이 설치되고 성공적으로 프로비저닝되었는지 확인합니다.
- **asclab-linux**에 대해서도 이 과정을 반복합니다. Linux 플랫폼에서는 확장의 이름이 `MDE.Linux`로 다르게 표시됩니다.

> Note: There are multiple ways you can automate the process where you need to achieve at scale deployment. More details are available on our [documentation](https://docs.microsoft.com/en-us/azure/security-center/deploy-vulnerability-assessment-vm#automate-at-scale-deployments) and on [blog](https://techcommunity.microsoft.com/t5/azure-security-center/built-in-vulnerability-assessment-for-vms-in-azure-security/ba-p/1577947).


1,105 / 5,000
11. VA 에이전트는 이제 필요한 모든 아티팩트를 수집하여 Qualys Cloud로 전송하고, 결과는 24시간 이내에 ASC 콘솔에 표시됩니다.

**취약성 평가 결과 확인 및 수정:**

1. Microsoft Defender for Cloud 사이드바에서 **권장 사항**을 클릭합니다.
2. **취약성 수정** 보안 제어(보안 취약성과 관련된 모든 권장 사항 포함)를 실행합니다.
3. **시스템에서 취약성 결과가 해결되어야 함**을 검색합니다.
4. 보안 검사에서 영향을 받은 리소스에서 발견된 취약성 목록이 표시됩니다.
5. 권장 사항에서 **영향을 받은 리소스**를 실행합니다. 두 개의 비정상 리소스(asclab-win 및 asclab-linux)와 해당 리소스가 없습니다.
6. **비정상 리소스**에서 **asclab-win** 리소스를 선택합니다. 여기에서 해당 리소스에 대한 모든 관련 권장 사항을 볼 수 있습니다.
7. 결과 목록에서 상단에 있는 가장 높은 취약점(ID 376813)을 클릭합니다.
8. 정보 창에서 취약점에 대한 설명, 영향, 심각도, 해결 단계 등을 포함한 세부 정보를 확인합니다.

<br><br>
---
<br><br>
### 연습 2: 컨테이너 취약성 평가

Microsoft Defender for Cloud는 ACR(Azure Container Registry)에서 레지스트리로 푸시되거나, 레지스트리로 가져오거나, 지난 30일 이내에 가져온 이미지를 검사합니다.
그런 다음 이미지별로 자세한 결과를 공개합니다. 모든 취약성은 다음 권장 사항에서 확인할 수 있습니다. Azure Container Registry 이미지의 취약성은 수정해야 합니다(Qualys 기반).

취약점이 있는 컨테이너 레지스트리 이미지를 시뮬레이션하기 위해 ACR 작업 명령과 샘플 이미지를 사용합니다.


1. Azure Portal에서 **컨테이너 레지스트리** 블레이드로 이동하거나 [여기](https://portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.ContainerRegistry%2Fregistries)를 클릭합니다.
2. 컨테이너 레지스트리의 이름을 복사합니다(예: *asclabcrktfvrxcne4kki*).
3. bash 환경을 사용하여 [Azure Cloud Shell](https://shell.azure.com/)을 엽니다.
4. Microsoft Container Registry에 호스팅된 hello-world 이미지에서 Linux 컨테이너 이미지를 빌드하고 구독의 기존 Azure Container Registry 인스턴스에 푸시합니다.

다음 두 스크립트 블록을 실행합니다.

```
echo FROM mcr.microsoft.com/azuredocs/aci-helloworld > Dockerfile
```

Modify the following script to include your container registry name:

```
az acr build --image sample/hello-world:v1 --registry <your container registry name> --file Dockerfile .
```

![Build Linux container in Cloud Shell](../Images/asc-build-linux-container-cloud-shell.gif?raw=true)

5. Wait for a successful execution message to appear. For example: Run ID: cb1 was successful after 23s
6.	The scan completes typically within few minutes, but it might take up to 15 minutes for the vulnerabilities/security findings to appear on the recommendation.
7.	From Microsoft Defender for Cloud sidebar, click on **Recommendations**.
8.	Expand **Remediate vulnerabilities** security control and select **Container registry images should have vulnerability findings resolved**.
9.	On the recommendation page, notice the following details at the upper section:
    - Unhealthy registries: *1/1*
    - Severity of recommendation: *High*
    - Total vulnerabilities: *expect to see 2 or more vulnerabilities*
10.	Expend the **Affected resources** section and notice the **Unhealthy registries** count which shows **1 container registry** (asclab-xxx).
11.	On the **Security Checks** section, notice the number of vulnerabilities.
12.	Click on the first security check to open the right pane. Notice the vulnerability description, general information, remediation, and the affected resources. **Close this window.**

![](../Images/Lab5vul2.gif?raw=true)

### Exercise 3: Automate recommendations with workflow automation

Every security program includes multiple workflows for incident response. These processes might include notifying relevant stakeholders, launching a change management process, and applying specific remediation steps.
Using workflow automation, you can trigger logic apps to automate processes in real-time with Microsoft Defender for Cloud events (security alerts or recommendations).
In this lab, you will create a new Logic App and then trigger it automatically using workflow automation feature when there is a change with a specific recommendation.

**Create a new Logic App:**
1.	On the Azure Portal, type *Logic Apps* on the search field at the top or [click here](https://ms.portal.azure.com/#blade/HubsExtension/BrowseResource/resourceType/Microsoft.Logic%2Fworkflows).
2.	Click **Add** to create a new Logic App.
3.	On the Basics tab, select **Azure subscription 1** and resource group **asclab**.
4.	On the Logic app name field enter a unique name such as *SendRecommendationsChanges12* (Note: There will be an error if the Logic app name is not unique) .
5.	Select location, for example: **West Europe** (it’s recommended to use the same region as used in the previous exercises).
6.	Under the Plan section, **select consumption**. 
7.	Leave all other options as per the default.
8.	Select **Review + Creation** and then **Create**.
9.	The Logic Apps Designer opens, select **Blank Logic App**.
10.	At the search control, type *Microsoft Defender for Cloud* and select **When an Microsoft Defender for Cloud Recommendation is created or triggered**.
11. Click on new step and type *Outlook.com*.
12. Scroll down the list, and click **Send an email (V2)** action to add it to the Designer.

> Note: you will need to sign into your Outlook.com (Microsoft Account) and grant permissions for the Logic App to send email using your account.
> 
13.	In the Send an email (V2), add your email address to the **To** field.

> Later, you will use that email address to check if you received an email using workflow automation feature.

14.	Click in the **Subject box**, then type: *Recommendation changed:*
15.	Click just after Recommendation changed: to get your cursor in the right place. In the dynamic content box, click on **Dynamic content** and then select `Properties Display Name` (click Add dynamic content if it doesn’t pop out automatically).
15.	Click into the Body text box and type the following:

**The following recommendation has been changed**</br>
**Recommendation:**</br>
**Description:**</br>
**Status:**</br>
**Link to recommendation:**</br>

16.	Click just after each section, to get your cursor in the right place. In the **dynamic content box**, click on **See more** and match each line to the following content:

Recommendation: `Properties Display Name`</br>
Description: `Properties Metadata Description`</br>
Status: `Properties Status Code`</br>
Link to recommendation: `Properties Links Azure Portal Uri`</br>

17.	Your Logic App should now look like the below screenshot. If so, click on **Save** in the Logic App Designer.

![Logic App worklfow](../Images/asc-logic-app-workflow.gif?raw=true)

**Create a new workflow automation instance**
1.	From Microsoft Defender for Cloud's sidebar, select **Workflow automation** which is found under the **Management** section.
2.	Click **Add workflow automation**.
3.	A pane appears on the right side. Enter the following for each field:
    - General:
        - Name: *Send-RecommendationsChanges*
        - Description: *Send email message when a recommendation is created or triggered*
        - Subscription: *Azure subscription 1*
        - Resource group: *asclab*
    - Trigger conditions:
        - Select Microsoft Defender for Cloud data types: *Microsoft Defender for Cloud recommendations*
        - Recommendations name: *All recommendations selected*
        - Recommendation severity: *All severities selected*
        - Recommendation state: *All states selected*
    - Actions:
        - Show Logic App instances from the following subscriptions: *Azure subscription 1*
        - Logic App name: *Send-RecommendationsChanges*
    Click **Create** to complete the task.
4.	Wait for the banner *Workflow automation created successfully. Changes may take up to 5 minutes to be reflected*. From now on, you will get email notifications for recommendations.
Once you start to get email notifications, you can disable the automation by selecting the workflow and clicking on **Disable**.

> Please be aware that if your trigger is a recommendation that has "sub-recommendations” / “nested recommendations”, the logic app will not trigger for every new security finding; only when the status of the parent

5. Once the automation is automatically triggered, you should expect the email message to look like the screenshot below:

![Workflow automation generated email message](../Images/asc-workflow-automation-automated-email.gif?raw=true)

6.	Test/trigger your automation manually:
    - On Microsoft Defender for Cloud sidebar, click on **Recommendations**.
    - Look for any recommendations that has a Quick Fix banner (which is the lightning symbol to the right of the recommendation).
    - Select a resource and then click on **Trigger Logic App** button.
    - In the Logic App Trigger blade, select the Logic App you created in the previous step (SendRecommendationsChanges).
    - You should receive an email containing ...
7.	From the top menu in Microsoft Defender for Cloud, click on **Guides & Feedback**.
8.	Here you can learn more about workflow automation, get useful links and explore our community tools from the GitHub repository.
9.	Click on **Community tools** and then **View all community tools**.

### Exercise 4: Accessing your secure score via ARG
Azure Resource Graph (ARG) provide an efficient and performant resource exploration with the ability to query at scale across a given set of subscriptions.
Azure Secure Score data is available in ARG so you can query and calculate your score for the security controls and accurately calculate the aggregated score across multiple subscription.

1.	From the Azure Portal, search for *Resource Graph Explorer* (or arg).

![Resource Graph Explorer](../Images/asc-resource-graph-explorer.gif?raw=true)

2.	Paste the following KQL query and then select **Run query**.

```
SecurityResources
| where type == 'microsoft.security/securescores'
| extend current = properties.score.current, max = todouble(properties.score.max)
| project subscriptionId, current, max, percentage = ((current / max)*100)
```

3.	You should now see your subscription ID listed along with the current score (in points), the max score and the score as percentage.
4.	To return the status of all the security controls, select **New query**, paste the following KQL query and click on **Run query**:

```
SecurityResources
| where type == 'microsoft.security/securescores/securescorecontrols'
| extend SecureControl = properties.displayName, unhealthy = properties.unhealthyResourceCount, currentscore = properties.score.current, maxscore = properties.score.max
| project SecureControl , unhealthy, currentscore, maxscore
```
### Exercise 5: Creating Governance Rules and Assigning Owners
Security teams are responsible for improving the security posture of their organizations but they may not have the resources or authority to actually implement security recommendations. Assigning owners with due dates and defining governance rules creates accountability and transparency so you can drive the process of improving the security posture in your organization.

Follow the progress for your created recommendations on the Security Posture page. Weekly email notifications to the owners and managers make sure that they take timely action on the recommendations that can improve your security posture and recommendations.

1. Return to Microsoft Defender for Cloud blade and Click on **Environment settings**. Click the down arrow on **Azure** to show the subscription, and then click the down arrow on **Azure Susbcription 1** to show the workspace. 
    ![Environment settings](../Images/mdfc-envsettings.png?raw=true)
2. From Settings's sidebar, select **Governance Rules** which is found under the **Policy Settings** section.
    <img width="339" alt="image" src="https://user-images.githubusercontent.com/15238159/179999129-68ba1e61-4a15-4583-9d7c-47e08d073eeb.png">
3. Click on **Add Rule**
   ![image](https://user-images.githubusercontent.com/15238159/180010137-35a610dd-1738-4f4e-a967-ab69ad9c5acc.png)
4. Fill out the new Goverance Rules with **Rule Name**, **Description**, **Priority**, **By Severity select High**, **Set Owner by email Address**, **Set Remedation Timeframe to 14 days, **Select both check marks**, click **Create**
   
   <img width="359" alt="image" src="https://user-images.githubusercontent.com/15238159/180060164-6f28dd5f-3791-4f38-989e-0b87b255aa65.png">
5. To confirm Click on **Security Posture** under **Cloud Security** and select **Owners**
    <img width="1051" alt="image" src="https://user-images.githubusercontent.com/15238159/180055872-6da285ca-124b-4eaf-955d-f6984fd81ef7.png">


```

More details on the [official article](https://docs.microsoft.com/en-us/azure/security-center/secure-score-security-controls) or on the [blog post](https://techcommunity.microsoft.com/t5/azure-security-center/querying-your-secure-score-across-multiple-subscriptions-in/ba-p/1749193)

### Continue with the next lab: [Module 6 - Workload Protections](../Modules/Module-6-Azure-Defender.md)
