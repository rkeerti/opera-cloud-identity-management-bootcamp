# OPERA Cloud Identity Management Federation with Okta

## Prerequisites for Okta Integration with OCIM

* An Okta account with administrator privileges.
* User account in OCI IAM Identity Domain with Administrator role.

## Task 1 : Create a confidential application in OCI IAM Identity Domain​

1. Open a supported browser and enter the following Console URL: 

    ```
    https://cloud.oracle.com
    ```
2. Enter your Cloud Account Name, also referred to as your tenancy name, and click Next.

3. Enter the login information and sign in to the OCI console. 

4. Open the navigation menu and click **Identity & Security**. Under Identity, click **Domains**.

     <img src= "images/oci1.png" alt="OCI1" style="border: 1px solid black;">

5. Select the identity domain in which you want to configure Okta provisioning and click **Integrated Applications**.

6. Click **Add Application** and choose **Confidential Application** and then click **Launch workflow**.

    ![Add Application](images/add_application.png)

7. Enter a name for the confidential application, for example, “OktaSync” Click Next.

8. Under Client configuration, select Configure this application as a client now. Under Authorization, select Client credentials

     <img src= "images/add-app2.png" alt="Add Application 2" style="border: 1px solid black;">

9. Scroll to the bottom and click Add app roles.

10. Under **App roles** click **Add roles**, and in the Add app roles page, select **User Administrator** and click **Add**.

    <img src= "images/app-role.png" alt="Add Application 3" style="border: 1px solid black;">

    ![Add Application 4](images/add_app_roles.png)

11. Click Next and then click Finish.

12. On the application details page, click Activate and confirm that you want to activate the new application.

## Task 2 : Find the Domain URL and Generate a Secret Token

1. Return to the identity domain overview by clicking the identity domain name in the breadcrumbs. Click Copy next to the Domain URL in Domain information and save the URL to an app where you can edit it. The OCI IAM GUID is the **IdentityDomainID** part of the domain URL:

    ```
    https://<IdentityDomainID>.identity.oraclecloud.com:443/fed/v1/idp/sso
    ```

    ![Domain1](images/domain1.png)

2. In the confidential app in OCI IAM, click the OAuth configuration under Resources.

3. Scroll down and find the Client ID and Client secret under General Information.

4. Copy the client ID and store it.

    <img src= "images/domain2.png" alt="Domain2" style="border: 1px solid black;">

5. Click Show secret and copy the secret and store it.

    ![Domain3](images/domain3.png)
    
6. The secret token is the base64 encoding of clientID:clientsecret or

    ```
    base64(<clientID>:<clientsecret>)
    ```

The following examples show how to generate the secret token on Microsoft Windows and Apple MacOS.

In a Microsoft Windows environment:

* Open CMD and use this powershell command to generate base64:

    ```
    [Convert]::ToBase64String([System.Text.Encoding]::Unicode.GetBytes('client_id:secret'))
    ```
* Make a note of the secret token value.

In an Apple MacOS, use the following:

* Open terminal and use the following command

    ```
    echo -n <clientID>:<clientsecret> | base64
    ```
    
* Make a note of the secret token value.

## Task 3 : Configure the OCI IAM Application in the Identity Provider (Okta)​

1. Sign in to your Okta account.

2. Click on **Admin** on the top right corner to access the admin console. **OR** use the following URL where **< okta-org >** is the prefix for your organization with Okta:

    ```
    https://<okta-org>-admin.okta.com
    ```

    <img src= "images/okta1.png" alt="Okta1" style="border: 1px solid black;">

3. From the navigation menu on the left, Click **Applications** , then Click **Browse App Catalog**

     <img src= "images/okta2.png" alt="Okta2" style="border: 1px solid black;">

4. Search for **Oracle Cloud Infrastructure IAM** and select it. Click **Add Integration**

    <img src= "images/okta3.png" alt="Okta3" style="border: 1px solid black;">

    <img src= "images/okta4.png" alt="Okta4" style="border: 1px solid black;">

5. Under General settings, enter a name for the application, for example **OCI-App**, and click **Done**.


## Task 4 : Configure Provisioning and User Attribute Mappings in the Identity Provider (Okta)

1. In the newly created application page, click the **Sign On** tab.
In Settings, click **Edit**.

    <img src= "images/okta5.png" alt="Okta5" style="border: 1px solid black;">  

2. Scroll down to Advanced Sign-on Settings.
Enter the OCI IAM GUID (Identity Domain ID) that you saved earlier from the Domain URL. Click **Save**

    <img src= "images/okta6.png" alt="Okta" style="border: 1px solid black;"> 

3. Scroll to the top and click the Provisioning tab. Click Configure API Integration.

    <img src= "images/okta7.png" alt="Okta" style="border: 1px solid black;"> 

4. Select Enable API Integration. Enter the secret token value you copied earlier in API Token.

    <img src= "images/okta8.png" alt="Okta" style="border: 1px solid black;"> 

5. Click Test API Credentials.
If you get an error message, check the values that you have entered and try again.

    Okta has successfully connected to the OCI IAM SCIM endpoint when you get the ‘Oracle Cloud Infrastructure IAM was verified successfully!’ message.

6. Click Save.
    
    The Provisioning to App page opens, where you can create users, update user attributes, and map attributes between OCI IAM and Okta.

7. Under Settings, select **To App**, then Click **Edit**.

    <img src= "images/okta9.png" alt="Okta" style="border: 1px solid black;"> 

8. Enable Create Users, Update User Attributes & Deactivate Users. Click Save.

    <img src= "images/okta10.png" alt="Okta" style="border: 1px solid black;"> 

9. Scroll down to the Attribute Mappings section. Click **Go to Profile Editor**; the Attribute section lists OCI IAM Attributes.

    <img src= "images/okta11.png" alt="Okta" style="border: 1px solid black;">

10. Click on **Add Attribute** 
    <img src= "images/okta12.png" alt="Okta" style="border: 1px solid black;">

    
    To Add an attribute, Refer to the User Mapping table and enter the following details:

    * Data type : Refer to value from the **Mapping Type** column from the User Mapping Table
    * Display name : Refer to the value from the **IAM Domain (IDCS) User Attribute** column from the User Mapping Table
    * Variable name: Refer to the value from the **IAM Domain (IDCS) User Attribute** column from the User Mapping Table
    * External name : Automatically populated by the value of the variable name.
    * External namespace : Refer to the value from the **External Namespace** column from the User Mapping Table. If there is no value in the column, leave it blank.
    * Attribute type : Select **Personal**

    
    The User Mapping table to map user attributes between OCI IAM and Okta is shown below. Ensure all of the mandatory attributes. Some attributes may have already been created by default, you do not have to add them.

    

    | Okta Attribute      | IAM Domain (IDCS) User Attribute | External Namespace | Mapping Type | Attribute Value | Description | Mandatory Attribute |
    | ----------- | ----------- |-------|------|------|------|--------|
    | login      | userName       | | Direct| Map from Okta profile | User name| Yes|
    | lastName   | name.familyName | | Direct| Map from Okta profile| Last name| Yes|
    |email| emails[type eq "work"].value| | Direct| Map from Okta profile| Email address| Yes |
    |(user.email != null && user.email != '') ? 'work' : ''| emailType| | string| (user.email != null && user.email != '') ? 'work' : '' | Email Type| Yes |
    |extensionAttributePrimaryWorkLocation| OC_PrimaryWorkLocation | urn:ietf:params:scim:schemas:idcs:extension:custom:User | string | Same value for all Users. Refer description | Mandatory Single Valued User Attribute. Indicates the User primary work location. Primary Work Location can have values <CHAINCODE>:C for multi chain customers derived from the User profile. For customers having only a single chain, the source value can be set to constant <CHAINCODE>:C for all users. | Yes |
    | isFederatedUser| isFederatedUser | urn:ietf:params:scim:schemas:oracle:idcs:extension:user:User| boolean | true | Enable Federated User flag in Identity Domain.| Yes|
    |bypassNotification|bypassNotification|urn:ietf:params:scim:schemas:oracle:idcs:extension:user:User| boolean | true | The bypass notification flag controls whether an email notification is sent after creating or updating a user account in Identity Domain. The bypassNotification must be set to "true" for Federated users. This disables user account activation notification in IAM Identity Domain for the user. | Yes | 

    See the following example to add the 'OC_PrimaryWorkLocation' attribute:

    <img src= "images/okta13.png" alt="Okta" style="border: 1px solid black;">

11. Once all the mandatory attributes have been created, click **Mapping**. Click on the tab **Okta User to OCI App**

    <img src= "images/okta14.png" alt="Okta" style="border: 1px solid black;">

    <img src= "images/okta15.png" alt="Okta" style="border: 1px solid black;">

12. Refer to the the **User Mapping** table again and enter the values from the **Attribute Value** column. 
Note: Use single quotes ('') for string values, for example primary work location. Save the mappings.

     <img src= "images/okta16.png" alt="Okta" style="border: 1px solid black;">

13. Syncing Groups from Okta to Oracle Identity Domain can be done manually or can be automated by selecting the **Push Group** tab under the OCI IAM application to define a rule.

    Select the Push Group tab and click on **Push Group**

    <img src= "images/okta17.png" alt="Okta" style="border: 1px solid black;">

14. Click on **Find groups by name** and Enter the group name to push from Okta to OCI IAM Domain. Then click **Save**

    <img src= "images/okta18.png" alt="Okta" style="border: 1px solid black;">


## Task 5 : Test User and Group Provisioning into OCI IAM 

1. In the newly created application, click the Assignments tab.
2. Click Assign and select Assign to People.

    <img src= "images/okta19.png" alt="Okta" style="border: 1px solid black;">

3. Search for the user to provision from Okta to OCI IAM.

4. Click Assign next to the user. For example, here we are assigning "test user1" to provision from Okta to OCI

    <img src= "images/okta20.png" alt="Okta" style="border: 1px solid black;">

5. Click Save and then click Go Back.

6. Now provision Okta groups into OCI IAM. In the Assignments tab, click Assign and select Assign to Groups.

7. Search for the groups to be provisioned to OCI IAM. Next to the group name, click Assign.

    <img src= "images/okta21.png" alt="Okta" style="border: 1px solid black;">

8. Click Done.

9. Open a supported browser and enter the following Oracle Cloud Infrastructure (OCI) Console URL: https://cloud.oracle.com and sign in to the OCI console

10. Open the navigation menu and click **Identity & Security**. Under Identity, click **Domains**

11. Select the identity domain in which Okta has been configured.
Click Users.
The user which was assigned to the OCI IAM application in Okta is now present in OCI IAM.
Click Groups.
The group which was assigned to the OCI IAM application in Okta is now present in OCI IAM.

    <img src= "images/okta22.png" alt="Okta" style="border: 1px solid black;">








