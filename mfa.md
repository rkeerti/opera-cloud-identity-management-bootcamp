# OPERA Cloud Identity Management MFA Lab​

## Task 1 - Create an OCI IAM group

1. Log in to OCI Cloud console as an OCI cloud administrator user.

2. Open the navigation menu and click Identity & Security. Under Identity, click Domains.

3. Click the name of the identity domain in which you want to work. (You might need to change the compartment to find the domain that you want)

4. On the Domain page, click Groups


5. On the Groups page, click Create Group


6. Enter a name for the group, for example **MFAENABLED**


7. Search and Add users as members of the group for which MFA is to be triggered during OPERA Cloud services login.


8. Click Create and go back to the Domain page.

    <img src= "images/mfa1.png" alt="MFA" style="border: 1px solid black;">

## Task 2 - Configure MFA and Sign-on Policy

9. On the Domain Details page, click Security.


10. On the Security page, click MFA.


11. Under Factors, select each of the factors required to access the identity domain. For an explanation of each factor, see [Configuring Authentication Factors](https://docs.oracle.com/en-us/iaas/Content/Identity/mfa/configure-authentication-factors.htm#configure-authentication-factors)

    <img src= "images/mfa2.png" alt="MFA" style="border: 1px solid black;">

12. (Optional step) Click Configure for the MFA factors you have selected. 


13. (Optional step) Set the Maximum number of enrolled factors users can configure.


14. (Optional step) Use the Trusted devices section to configure trusted device settings. Similar to "remember my computer," trusted devices do not require the user to provide secondary authentication each time they sign in.


15. (Optional step) Under Sign-in rules, set the maximum number of unsuccessful MFA attempts a user can make before being locked out.


16. Click Save changes, and then confirm the change.


17. Follow the below steps to configure new sign on rules to enable MFA in the default sign-on policy. This default sign-on policy will be available out of the box in a customer's OCI IAM Identity Domain.
    * On the Security page for the domain, click Sign-on policies.

    * On the Sign-on policies page, click Default Sign-On Policy.

    * On the Default Sign-On Policy page, under Resources, click Sign-on rules.

    * Click the Add sign-on rule, carefully read the confirmation, and click Continue.

    * Enter the rule name, for example, ”Group based MFA”

    * Under conditions, in Group Membership, add the group created earlier in step 6.

        <img src= "images/mfa3.png" alt="MFA" style="border: 1px solid black;">

    * Under Actions, select Allow access. Select the prompt for an additional factor and select Specified factors only.

    * Select factors, we recommend Mobile app passcode, Mobile app notification, and Fast ID Online (FIDO) passkey authenticator.

        <img src= "images/mfa4.png" alt="MFA" style="border: 1px solid black;">

    * Select Once per session or trusted device under Frequency.

    * Select Required under Enrollment.

    * Click Add sign-on rule.

    * On the Default Sign-On Policy page, click Edit Priority.
    
    * Carefully read the confirmation and click Continue.

    * Click the priority number of the newly created rule to ensure it is above the Default Sign On Rule where priority 1 is the newly created rule and priority 2 is the Default Sign On Rule.

        <img src= "images/mfa5.png" alt="MFA" style="border: 1px solid black;">
    
    * Click Save Changes.

## Task 3 - Test MFA

18. Test MFA with the user who is part of the newly created group (the group added in the sign-on rule).