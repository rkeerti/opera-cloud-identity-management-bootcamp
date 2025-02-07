# Non-Federated User

This lab covers how to manage Identity and Access Management (IAM) administrators, groups, and users in OPERA Cloud Identity Management using the OPERA Cloud Identity Management Portal.

* [Managing Users](#managing-users)
* [Managing IAM Administrator Roles](#managing-iam-administrator-roles)
* [Managing Groups](#managing-groups)



## Managing Users

### Create User


1. Log in to OPERA Cloud Identity Management portal as an administrator. The URL will follow the following pattern:

 ```
    https://<Host>/<CUSTOMER ENTERPRISE ID>/ocimportal
 ```


2. Click **Users**. Click **Create User**.  

3. Enter the following user information. 
    * Last Name
    * Email Address
    * Username
    * Primary Work Location: This is the chain or property code representing the location where the user works.

4. Click **Create** to create the user.

### User Profile Management

#### Editing a User

1. From the User Management page, Click **Locations** and select the location to search for the associated users in that location

2. Click on the Username of the user that you created to open the User Profile page.

3. Click Edit User to open the prompt to edit user fields.
    Adjust the editable fields as needed:
    * Last Name
    * Email Address
    * Username
    * Primary Work Location

4. Click Update to update the user.

#### Resetting a User Password

1. Click Username to open the User Profile page.

2. Select one or multiple users. After your selection, the Reset Password button appears.

3. Click the Reset Password button to reset the passwords for all selected users.
Users receive an email that allows them to enter a new password.

#### Changing Primary Work Location for a User

1. On the User Profile page for a user, click **More Actions** and then click **Edit User Primary Work Location**.

2. Click **New Primary Work Location** to select the new primary work location from the list of values, which is depicted as Chain followed by its properties.

3. Click Current Primary Work Location Groups to view group memberships for that user associated with the current primary work location. Before you update the primary work location, remove group memberships for the user associated with the current primary work location.

4. Click Update to update the User Primary Work Location.

#### Deleting a User

1. On the User profile page for a user, click **More Actions** and then click **Delete User**.

2. Click **Delete** to delete the user account.

### Add User to a Seeded Group

Seeded Groups are groups available out of the box in OPERA Cloud Identity Management and are associated with chains and properties. Seeded groups are created in a customer’s OCI IAM Identity Domains during chain or property provisioning in OPERA Cloud applications. These group cannot be deleted using the OPERA Cloud Identity Management Portal.

1. Log in to OPERA Cloud Identity Management as an administrator.

2. Click the **Groups** tile on the home page.

3. Click **Locations** and select the location to search the associated groups for that location

4. Click on the **DEVELOPERPORTALACCESS** role name to display the Role details page for that role.  

6. Click **Assign Users** to search for existing users. 

7. Select the user that you created and click on **Update**

8. The IAMADMIN Administrator role is now added to the user.


## Managing IAM Administrator Roles

### Adding Administrative Roles to an existing user

1. Log in to the OPERA Cloud Identity  Management portal as an Administrator.

2. From the homepage, Click **Administrator Roles**

3. Click **Locations**. Select a location for the user that was 
created in the previous steps and press Enter

4. Click the Locations filter chip in the search bar and select the location.

5. Click on the **IAMADMIN** role name to display the Administrator Role  details profile page for that role.  

6. Click **Assign Users** to search for existing users. 

7. Select the user that you created and click on **Update**

8. The IAMADMIN Administrator role is now added to the user.

## Managing Groups

### Create Custom Group

1. Click the **Groups** tile on the home page of the OPERA Cloud Identity Management Portal.

2. Click the **Create Group** button on the Group Management page.

3. Enter the custom Group Name.

4. Select a location from the location list of values.

5. Click **Submit** to create the custom group.

### Assign User to Custom Group

1. Click the **Groups** tile on the home page of the OPERA Cloud Identity Management Portal.

2. To search groups, click on the location filterchip and select the location where the group was created.

3. Click **Edit Group** to edit the group description.

4. Click **Assign Users** to assign user group membership in the group. 

5. Select the user that you created and click **Update** to assign the group membership.

### Copy Groups

