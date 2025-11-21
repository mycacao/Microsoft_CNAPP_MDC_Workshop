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

# Data Sensitivity Settings

## Exercise 3: Configure sensitive data categories

1. Navigate to **Microsoft Defender for Cloud > Environment settings** 으로 이동합니다. 

3. 페이지 상단의 **Data sensitivity** 를 선택합니다.

<img width="1793" height="1060" alt="image" src="https://github.com/user-attachments/assets/53da7492-821f-4e84-bfe4-243fd4a46e12" />


4.  **Other** 카테고리 유형을 선택합니다:

<img width="1818" height="852" alt="image" src="https://github.com/user-attachments/assets/3bd4a7db-0823-4e8e-be01-a8d509cdfd2c" />


5. 기본적으로, **Other**  카테고리 정보 유형은 sensitive data discovery 제외됩니다. 그래서 이 예제에 대해서는, **All** 을 선택하고 그리고 and **Apply** 를 선택합니다.

<img width="1771" height="1052" alt="image" src="https://github.com/user-attachments/assets/31f631c7-37cf-49b0-ae0f-11f5e3d56137" />


6. 새로운 설정 확인 하기 위해, Data sensitivity 페이지 상단에 **Save** 를 선택합니다.

## (Optional) Exercise 4: Import and configure custom sensitive info types and sensitivity labels

Defender for Cloud provides built-in sensitive info types (SITs) from Microsoft Purview out-of-the-box. If you have Enterprise Mobility and Security E5/A5/G5 licensing you can also optionally import your own custom sensitive info types and labels from Microsoft Purview compliance portal. After enabling integration with Microsoft Purview, you will get the option to set-up label thresholds and select your custom SITs to be used for sensitive data discovery.

### Enable integration with Microsoft Purview

1. Log into **Microsoft Purview compliance portal**.
2. Navigate to **Information Protection > Labels**.
3. In the consent notice messages, select **Turn on** and then select **Yes** to share your custom info types and sensitivity labels with Defender for Cloud.

   ![Enable Purview integration 1](../Images/turnonpurviewintegration1.png?raw=true)

   ![Enable Purview integration 2](../Images/turnonpurviewintegration2.png?raw=true)

<!--
> [!NOTE]
> Purview portal integration messages are subject to changes, so it is possible they will not look exactly the same like in this excercise.
-->

### Create a custom sensitive info type

1. Navigate to **Data classification > Classifiers > Sensitive info types**.
    - In case of the new Microsoft Purview portal, this can be found in the **Information Protection** blade.

      ![Custom SIT creation 1](../Images/customsit1.png?raw=true)

2. Select **Create sensitive info type**.
3. Enter name and description.

   ![Custom SIT creation 2](../Images/customsit2.png?raw=true)

4. On the **Patterns** step, select **Create pattern**.
5. Add primary element and choose **Keyword list**.

   ![Custom SIT creation 3](../Images/customsit3.png?raw=true)

6. In the **ID** field, type  *"DSPM"*.
7. In the **Keyword group #1, Case insensitive**, type *"data security posture management"*.
8. Select the **String match** option and click **Done**.

   ![Custom SIT creation 4](../Images/customsit4.png?raw=true)

9. Confirm by selecting the **Create** button.
10. Leave **High confidence level** selected in the next step.
11. On the Finish page review the settings and save the new Custom SIT by selecting the **Create** button.

    ![Custom SIT creation 5](../Images/customsit5.png?raw=true)

You can now select your Custom SIT from the **Custom** category in the **Data sensitivity** settings described in **Excercise 3**. Create and upload a document which will include the phrase *"data security posture management"* to test your Custom SIT.

### Set the threshold for sensitivity labels

 In the Microsoft Purview compliance portal, make sure your sensitivity label scope is set to *Items*; under which you should configure auto labeling for *Files* and *Emails*. Labels must be published with a label policy to take effect.

> [!NOTE]
> If you don't have any existing sensitivity labels, follow [this link](https://learn.microsoft.com/en-us/purview/how-to-automatically-label-your-content) for instruction on how to create them.

 You can use the previously created Custom SIT to be used as auto-labeling condition. If you then create a document with the key phrase, the document will then be automatically labeled. Alternatively, you can manualy label documents for example in Office applications.

 ![Auto-labeling](../Images/autolabeling.png?raw=true)

To have your labeled data visible in Defender for Cloud, follow these steps to check that your labels are included in the sensitive data discovery:

1. Navigate to **Microsoft Defender for Cloud > Environment settings > Data sensitivity** as described in **Exercise 3**.

2. Select **Change** to see the list of sensitivity labels and select the sensitivity label that will serve as your threshold. If you select the **(Lowest sensitivity)** label, all discovered labeled resources will be shown in Defender for Cloud.

   ![Setting label threshold](../Images/labelthreshold.png?raw=true)

3. Select **Apply** and **Save**.  

# Exercise 5: Upload sensitive data

### Upload data to Storage account

Create a new storage account based on the instructions in [Module 19](https://github.com/Azure/Microsoft-Defender-for-Cloud/blob/main/Labs/Modules/Module%2019%20-%20Defender%20for%20Storage.md#exercise-2-create-a-storage-account).

1. In the **Azure Portal**, navigate to **Storage accounts**.
2. Open the storage account you have created.
3. Navigate to **Data storage > Containers** and create new container by selecting the **+ Container** button on top of the page.

   ![Create Container](../Images/createcontainerdasp.png?raw=true)

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
