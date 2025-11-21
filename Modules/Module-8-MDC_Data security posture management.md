# Module 23 - Data security posture management

<p align="left"><img src="../Images/asc-labs-intermediate.gif?raw=true"></p>

#### 🎓 Level: 200 (Intermediate)

#### ⌛ Estimated time to complete this lab: 1-2 hours

#### 💁💁‍♀️ Authors

Pavel Kratky [GitHub](https://github.com/pavelkratky), [LinkedIn](https://www.linkedin.com/in/pavelkratky/)

Yura Lee  [GitHub](https://github.com/yura-lee/), [LinkedIn](https://www.linkedin.com/in/yura-lee/)

## Objectives

이 연습에서는 Microsoft Defender for Cloud에서 민감한 데이터 검색을 활성화하고 구성하는 방법을 안내하며, Defender CSPM과 Defender for Storage 계획에서 제공하는 추가 민감도 컨텍스트를 활용하는 다양한 방법을 보여줍니다.

## Exercise 1: Enabling sensitive data discovery

민감한 데이터 검색을 활성화하려면 특정 구독에서 Defender CSPM 또는 Defender for Storage 계획을 활성화해야 합니다.: 

1. Sign in to the **Azure portal**.
2. Navigate to **Microsoft Defender for Cloud**, then **Environment settings**.
3. Select the relevant subscription.
4. Toggle the **Defender CSPM** or **Storage** plan to **On**.

<img width="1803" height="1023" alt="image" src="https://github.com/user-attachments/assets/f705ced2-97da-4360-8597-4e7e78f02471" />

<img width="1792" height="1017" alt="image" src="https://github.com/user-attachments/assets/66930048-2ba4-4f4b-83d8-2a7eaf4cdf4a" />


   민감한 데이터 검색을 실행하기 위한 상세 권한은 당사 문서에 설명되어 있습니다. [documentation](https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-data-security-posture-prepare#whats-supported).

> [!NOTE]
> Storage Plan 만 활성화된 경우, 민감한 데이터 검색은 해당 계획에서 지원하는 리소스에만 적용됩니다. Defender CSPM Plan 을 활성화하면 데이터베이스와 멀티클라우드 리소스를 포함해 모든 지원 리소스가 스캔 대상에 포함됩니다.

5. 위 그림 상단에 **Settings & monitoring** 을 클릭합니다.
6. 여러 메뉴 항목중  **Sensitive data discovery** 컴포넌트의 토글을 **ON** 으로 활성화 합니다.

<img width="1810" height="961" alt="image" src="https://github.com/user-attachments/assets/4e2e87a3-a2d9-49dd-891f-c29765719f18" />

8.  **Continue** 를 선택하고 다음 페이지에서  **Save** 합니다.

> [!Important]
> 계획을 활성화한 후 첫 번째 검색 결과가 표시되기까지 최대 24시간이 소요됩니다. 이후 스캔은 매주 수행됩니다. 이전 모듈에서 이러한 계획 중 하나를 활성화했다면 검색이 완료될 때까지 최소 8일을 허용해야 합니다. 또는 새 Storage 계정을 구독에 추가할 수도 있습니다. 이미 검색된 구독에 새 Azure Storage 계정을 추가하면 24시간 이내에 검색됩니다.

## (Optional) Exercise 2: Enabling sensitive data discovery for AWS and GCP

### AWS integration

If you want to use sensitive data discovery for AWS S3 Buckets and RDS databases, visit [**Module 11 - Connecting an AWS project**](Module-11-AWS). Even if you have already done this step, you may have to redeploy the connection scripts with updated permissions.

1. Enable sensitive data discovery as described in **Excercise 1**.

2. Proceed with the instructions to download the CloudFormation template and to run it in AWS.

The snapshot is used to create a live instance that is spun up, scanned and then immediately destroyed (together with the copied snapshot).

Only scan findings are reported by the scanning platform.

### GCP integration

In case of GCP storage buckets, please visit [**Module 10 - Connecting a GCP project**](Module-10-GCP).

1. Enable sensitive data discovery as described in **Excercise 1**.

2. Proceed with the instructions to use GCP Cloud Shell or Terraform to connect GCP resources.

<br>

> [!NOTE]
> It takes up to 48 hours for first scan results in case of AWS and GCP.

# 데이터 민감도 설정 (Data Sensitivity Settings)

## Exercise 3: 민감한 데이터 범주 구성하기 (Configure sensitive data categories)

1. Navigate to **Microsoft Defender for Cloud > Environment settings** 으로 이동합니다. 

3. 페이지 상단의 **Data sensitivity** 를 선택합니다.

<img width="1793" height="1060" alt="image" src="https://github.com/user-attachments/assets/53da7492-821f-4e84-bfe4-243fd4a46e12" />


4.  **Other** 카테고리 유형을 선택합니다:

<img width="1818" height="852" alt="image" src="https://github.com/user-attachments/assets/3bd4a7db-0823-4e8e-be01-a8d509cdfd2c" />


5. 기본적으로, **Other**  카테고리 정보 유형은 sensitive data discovery 제외됩니다. 그래서 이 예제에 대해서는, **All** 을 선택하고 그리고 and **Apply** 를 선택합니다.

<img width="1771" height="1052" alt="image" src="https://github.com/user-attachments/assets/31f631c7-37cf-49b0-ae0f-11f5e3d56137" />


6. 새로운 설정 확인 하기 위해, Data sensitivity 페이지 상단에 **Save** 를 선택합니다.


7. 커스텀도 가능하다. Purview 에서 설정한 커스텀도 다음과 같이 목록에 표시되며 선택한다.
<img width="1822" height="1030" alt="image" src="https://github.com/user-attachments/assets/d9dad0cf-a933-4531-9d10-f814e2f8902e" />


## (Optional) Exercise 4: 사용자 지정 민감 정보 유형과 민감도 레이블 가져오기 및 구성 (Import and configure custom sensitive info types and sensitivity labels)

Defender for Cloud는 Microsoft Purview에서 제공하는 **기본 민감 정보 유형(SIT)**을 즉시 사용할 수 있도록 제공합니다. Enterprise Mobility and Security E5/A5/G5 라이선스를 보유한 경우, Microsoft Purview 규정 준수 포털에서 사용자 지정 민감 정보 유형과 레이블을 가져와 추가로 구성할 수도 있습니다. Microsoft Purview와의 통합을 활성화하면 레이블 임계값을 설정하고 민감한 데이터 검색에 사용할 사용자 지정 SIT(Custom SIT)를 선택할 수 있는 옵션이 제공됩니다..

### Microsoft Purview 와의 연계 활성화 (Enable integration with Microsoft Purview)

1. **Microsoft Purview compliance portal** 에 로그인 합니다.
2. **Information Protection > Labels** 로 이동합니다.
3. 처음 접속하면 아래와 같은 경보 메시지가 나올수 있습니다. **Turn on** 를 선택하고, MDC 와 사용자 지정 정보 유형 (Custom info types) 과 민감도 레이블(sensitivity labels) 연계하기 위해  **Yes** 를 선택합니다.

<img width="772" height="605" alt="image" src="https://github.com/user-attachments/assets/710a329a-52cb-47de-9076-82f9354eaf8d" />


<img width="948" height="471" alt="image" src="https://github.com/user-attachments/assets/4f953fe1-534d-408a-a7d7-9808dbf98ce4" />

<!--
> [!NOTE]
> Purview 포털의 연계 관련 메시지는 변경될 수 있으므로, 이번 연습에서 보이는 화면과 정확히 동일하지 않을 수 있습니다.
-->

### 사용자 지정 민감 정보 유형 만들기 (Create a custom sensitive info type)

1. 메뉴를 이동합니다. **Data classification > Classifiers > Sensitive info types**.
    - 새로운 Microsoft Purview portal 에서는, **Information Protection** 블레이드에서 찾을 수 있습니다.

<img width="1800" height="932" alt="image" src="https://github.com/user-attachments/assets/ed56d7b7-7820-4b73-baaf-dba9739a86b0" />


2. **Create sensitive info type** 를 선택합니다.
3. 이름 과 설명을 입력합니다.

<img width="1826" height="692" alt="image" src="https://github.com/user-attachments/assets/a77421ba-9319-4b6f-a048-6ed9e0b8d15a" />


4. **Patterns** 단계에서,  **Create pattern** 을 선택합니다.
5. 주요 구성요소 (primary element) 를 추가하고 **Keyword list** 를 선택합니다.

<img width="1427" height="758" alt="image" src="https://github.com/user-attachments/assets/f5e256a4-d78e-4492-bbb2-084ccd661dcd" />

6. **ID** 필드에서,   *"DSPM"* 을 타이핑합니다.
7. **Keyword group #1, Case insensitive** 에서, *"data security posture management"* 를 타이핑합니다.
8. **String match** 옵션을 선택하고, **Done** 을 클릭합니다.

<img width="1821" height="1036" alt="image" src="https://github.com/user-attachments/assets/155a3cac-0ac1-4f5a-adf2-6a9efc826e3c" />

<img width="1823" height="1030" alt="image" src="https://github.com/user-attachments/assets/3ea0e895-2a9f-4145-a2d7-fb4432a00398" />

<img width="1850" height="1032" alt="image" src="https://github.com/user-attachments/assets/1519afa8-4f32-4337-a475-7325c779e498" />

<img width="1832" height="1036" alt="image" src="https://github.com/user-attachments/assets/9da6742f-4aa7-4d52-ab82-e0c1d25ae98f" />


9. **Create** 버턴을 클릭하여 확인합니다.
10. 다음 단계에서 **High confidence level** 이 선택된 채로 남겨 둡니다.
11. 마지막 페이지에서, 설정을 검토하고, **Create** 버튼을 선택하여 새로운 Custom SIT 를 저장합니다. 

<img width="1838" height="968" alt="image" src="https://github.com/user-attachments/assets/ac0103b5-bb1c-427b-9a8c-02fc466a2876" />

이제 **데이터 민감도(Data sensitivity)** 설정의 **사용자 지정(Custom)** 범주에서 만든 사용자 지정 SIT를 선택할 수 있습니다. 테스트를 위해 *"data security posture management"* 라는 문구를 포함한 문서를 작성하여 업로드합니다.

<img width="1815" height="1027" alt="image" src="https://github.com/user-attachments/assets/46fc1684-533e-4c27-9b10-e1336c5ebb36" />


### 민감도 레이블의 임계값 설정 (Set the threshold for sensitivity labels)

Microsoft Purview 규정 준수 포털에서 민감도 레이블 범위가 *항목(Items)*으로 설정되어 있는지 확인합니다.; 그 아래에서 **파일(Files)**과 **이메일(Emails)**에 대한 자동 레이블링(auto labeling)을 구성해야 합니다. 레이블은 적용되기 위해 반드시 레이블 정책과 함께 게시되어야 합니다.

<img width="1845" height="877" alt="image" src="https://github.com/user-attachments/assets/d5990e88-0808-461e-8a89-3ec3cb207568" />



> [!NOTE]
> 기존 민감도 레이블(sensitivity labels)이 없다면, 레이블을 만드는 방법에 대한 안내는 [링크](https://learn.microsoft.com/en-us/purview/how-to-automatically-label-your-content)를 따라가세요.

 이전에 만든 사용자 지정 SIT를 자동 레이블링 조건으로 사용할 수 있습니다. 이후 해당 키워드가 포함된 문서를 생성하면 문서가 자동으로 레이블링됩니다. 또는 Office 애플리케이션에서 문서를 수동으로 레이블링할 수도 있습니다.

<img width="1833" height="1002" alt="image" src="https://github.com/user-attachments/assets/4d10e750-bd86-41c2-9071-3b560c18fc17" />

<img width="1840" height="1040" alt="image" src="https://github.com/user-attachments/assets/341c267a-5d36-47cf-98d1-ea79ab29b5f9" />


Defender for Cloud에서 레이블이 지정된 데이터가 표시되도록 하려면, 민감한 데이터 검색에 레이블이 포함되어 있는지 확인하기 위해 다음 단계를 따르세요 : 

1. 앞 연습3 에서 설명한  **Microsoft Defender for Cloud > Environment settings > Data sensitivity** 메뉴로 이동합니다.

2. **Change** 를 선택하면, 민감도 레이블(sensitivity labels)을 볼수 있고, 임계값으로 사용할 민감도 레이블을 선택하세요. **(Lowest sensitivity)** 레이블을 선택하면, 발견된 모든 레이블이 지정된 리소스는 Defender for Cloud에 표시됩니다.

<img width="1826" height="1041" alt="image" src="https://github.com/user-attachments/assets/880f0917-5aa0-48c3-a59d-bd69715c9ceb" />

3. **Apply** 를 선택하고 **Save** 를 누릅니다.  

# Exercise 5: 민감 데이터 업로드 (sensitive data)

### Storage account 에 민감 데이터 업로드

새로운 storage account 를 생성합니다. 이전 Lab을 참고합니다. [Module 19](https://github.com/Azure/Microsoft-Defender-for-Cloud/blob/main/Labs/Modules/Module%2019%20-%20Defender%20for%20Storage.md#exercise-2-create-a-storage-account).

1.  **Azure Portal**, 에서 **Storage accounts** 로 이동합니다..
2. 생헝한 storage account 를 엽니다.
3. Navigate to **Data storage > Containers** and create new container by selecting the **+ Container** button on top of the page.

<img width="1817" height="1025" alt="image" src="https://github.com/user-attachments/assets/c0c75fa9-0c4d-42a9-aefa-abfc3131c10b" />

<img width="1826" height="1040" alt="image" src="https://github.com/user-attachments/assets/77cfab3e-15c9-4e98-aaa2-7190c22ab4bb" />


<img width="1812" height="817" alt="image" src="https://github.com/user-attachments/assets/c78b1c8e-2934-42b4-8f90-d11d9af8a6a9" />
> [!NOTE]
> 방화벽에서 IP 를 열어주고 해야함

4. Choose a name, leave other settings by default and select **Create**.
5. Open the new container by clicking on its name and select the **Upload** button on top of the page.
6. Navigate to [Files](https://github.com/Azure/Microsoft-Defender-for-Cloud/blob/main/Labs/Files/TestData.zip) and download the *TestData.zip* file. This is a file that contains sample of sensitive data we will use in this exercise.
7. Select the file *"Credit Card Expenses.docx"* located in *CreditCardNumber* folder from the extracted zip archive and upload it to the container.

   ![Upload data to Container](../Images/uploaddatatocontainerdasp.png?raw=true)

> [!NOTE]
> It takes up to 24 hours for first scan results in case of newly created storage account. Databases are scanned on a weekly basis or within 24 hours on newly enabled subscriptions.

### (Optional) Upload data to Azure SQL database

In [Module 1](https://github.com/Azure/Microsoft-Defender-for-Cloud/blob/main/Labs/Modules/Module-1-Preparing-the-Environment.md), you created an Azure SQL database, *asclab-db*. In this exercise, we will connect to the database and upload sensitive information.

1. Follow instructions [on this page](https://learn.microsoft.com/en-us/sql/relational-databases/import-export/import-data-from-excel-to-sql?view=sql-server-ver16) to upload the .xlsx file into the database created as part of **Module 1**. We recommend to use Microsoft SQL Management Studio for the import (SMSS) with the following steps.
2. In SMSS, select the **asclab-db** database and choose **Import Data** via **Tasks**.

   ![SMSS import data 1](../Images/smssimportdata1.png?raw=true)

3. In the wizard, select the *"Sales Force Expense Cards.xlsx*" file and choose version *Microsoft Excel 2016*.

   ![SMSS import data 2](../Images/smssimportdata2.png?raw=true)

4. On the destination selection step, choose *Microsoft OLE DB Provider for SQL Server* and enter the credentials you used in **Module 1**.

   ![SMSS import data 3](../Images/smssimportdata3.png?raw=true)

5. In the next step, select **Copy data from one or more tables or views**.

   ![SMSS import data 4](../Images/smssimportdata4.png?raw=true)

6. Click on **Edit Mappings**.

   ![SMSS import data 5](../Images/smssimportdata5.png?raw=true)

7. Change *CC Number* and *CVV* type to **numeric**.

   ![SMSS import data 6](../Images/smssimportdata6.png?raw=true)

8. Confirm and finish the Wizard.

> [!NOTE]
> As described in **Exercise 1** you will now have to wait for the specified time, depending on when you have enabled the plans or created the resources, to allow the scan to finish. Follow [this link](https://learn.microsoft.com/en-us/azure/defender-for-cloud/concept-data-security-posture-prepare#discovery) to our documentation for more details.

# Explore risks to sensitive data

After you discover resources with sensitive data, Microsoft Defender for Cloud lets you explore sensitive data risk for those resources in several ways. We will have a look at the following options:

- **Security Explorer**: You can use Cloud Security Explorer to find sensitive data insights.
- **Attack Paths**: You can use attack paths to discover risk of data breaches.
- **Security alerts**: You can prioritize and explore ongoing threats to sensitive data stores by applying sensitivity filters Security Alerts settings.
- **Inventory**: You will get enhanced context in the Inventory for supported resources.
- **Data security dashboard**: Data-centric security dashboard helps effectively prioritize alerts and potential attack paths for data across multicloud data resources.

## Exercise 6: Explore risks with Cloud Security Explorer

Explore data risks and exposure in cloud security graph insights using a query template, or by defining a manual query.

1. In Defender for Cloud, open **Cloud Security Explorer**.

2. In the Query builder, from the **Select resource types** drop down menu, select *Data > Object storage > **Azure Storage accounts*** and click **Done**.

   ![Security explorer query 1](../Images/daspsecurityexplorer1.png?raw=true)

3. Add condition by selecting the **+** button. Choose *Data > **Contains sensitive data***

   ![Security explorer query 2](../Images/daspsecurityexplorer2.png?raw=true)

4. Run the query by clicking on the **Search** button.

   ![Security explorer query 3](../Images/daspsecurityexplorer3.png?raw=true)

5. In the *Results* section, look for the Storage account you've created in previous exercise and where you uploaded the *Credit Card Expenses.docx* file. After selecting it, *Result details* window will pop-up in the side, where you can review details. Select the **Export** button to export finding details to a csv file.

   ![Security explorer query 4](../Images/daspsecurityexplorer4.png?raw=true)

4. After opening the exported csv file, you can identify the specific files in which Defender for Cloud identified sensitive content and what sensitive info types did it match.

   ![Security explorer query 5](../Images/daspsecurityexplorer5.png?raw=true)

> [!NOTE]
> Sensitive data discovery in Defender for Cloud uses smart sampling scanning to achieve high efficiency of scanning and does not provide by design, an exhaustive list of all files in the scanned resource.

## Exercise 7: Identify sensitive resources in Inventory

1. In Defender for Cloud, open **Inventory**.
2. Add a filter **Sensitive info types** to narrow down the list.

   ![Inventory sensitive data 1](../Images/daspinventory1.png?raw=true)

3. In the **Value** drop-down list, uncheck ***(Unclassified)*** to show only resources containing sensitive info types and confirm by selecting **OK**.

   ![Inventory sensitive data 2](../Images/daspinventory2.png?raw=true)

4. Click on the name of the Storage account where you have uploaded sensitive data sample in previous exercise.

   ![Inventory sensitive data 3](../Images/daspinventory3.png?raw=true)

5. On the *Resource health overview*, you can review the *Sensitive info types* in the **Security value** section.

   ![Inventory sensitive data 4](../Images/daspinventory4.png?raw=true)

## (Optional) Exercise 8: Explore risks through attack paths

1. In Defender for Cloud, open **Attack path analysis**.

2. In **Risk Factors**, select **Sensitive data** to filter the data-related attack paths.

   ![Attack Path risk factors](../Images/daspattackpaths1.png?raw=true)

3. Review the attack paths.

4. To view sensitive information detected in data resources, select the resource name and then **Insights**. There is a section **Insights - Contains sensitive data**, where you can investigate details of the sensitive data discovery.

   ![Attack Path insights](../Images/daspattackpaths2.png?raw=true)

## (Optional) Exercise 9: Explore sensitive data security alerts

When sensitive data discovery is enabled in the Defender for Storage plan, you can prioritize alerts that affect resources with sensitive data.

1. In Defender for Cloud, open **Security alerts**.
2. Click on **Add filter** and search for **Sensitive info types**. In the **Value** parameter, uncheck **(Unclassified)** and confirm the filter by selecting **OK**.

   ![Alerts SIT 1](../Images/daspalerts1.png?raw=true)

3. After selecting one of the alerts, you can identify the sensitive info types by scrolling down in the details window.

   ![Alerts SIT 2](../Images/daspalerts2.png?raw=true)

## (Optional) Exercise 10: Data security dashboard investigation

1. In Defender for Cloud, open **Data security**.
Check the following tiles and look for unusual data:

    ![Data security dashboard 1](../Images/datasecuritydashboard1.png?raw=true)

- **Data resources requiring attention** - displays the number of sensitive resources that have either high severity security alerts or attack paths. Click on **high severity alerts** or **attack paths** to further drill down on the findings.
  - **Data resources with high severity alerts** - summarizes the active threats to sensitive data resources and which data types are at risk.

     ![Data security dashboard 2](../Images/datasecuritydashboard2.png?raw=true)

  - **Data resources with critical and high attack paths** - summarizes the potential threats to sensitive data resources by presenting attack paths leading to sensitive data resources and which data types are at potential risk.

     ![Data security dashboard 3](../Images/datasecuritydashboard3.png?raw=true)

- **Data queries in security explorer** - presents the top data-related queries in security explorer that helps focus on multicloud risks to sensitive data. Click on **View** to narrow down the specific query.

   ![Data security dashboard 4](../Images/datasecuritydashboard4.png?raw=true)

- **Sensitive data discovery** - summarizes the results of the sensitive resources discovered, allowing you to explore a specific sensitive information type and label. You can also open the data sensitivity settings described in **Exercise 3** by using the **Manage data sensitivity settings** button.

   ![Data security dashboard 5](../Images/datasecuritydashboard5.png?raw=true)

- **Internet-exposed data resources** - summarizes the discovery of sensitive data resources that are internet-exposed for storage and managed databases. Click on **View all data resources exposed to the internet** to run a query in Cloud security explorer.

   ![Data security dashboard 6](../Images/datasecuritydashboard6.png?raw=true)
