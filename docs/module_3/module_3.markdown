# **Module 3: Webex Calling (UCM Calling) Integration with Microsoft Teams** \[Approx 1 hour 45 min\]

With Webex Calling for Microsoft Teams, the Microsoft Teams users can access the enterprise-grade Webex Calling experience directly in the Microsoft Teams app. With a single click from the Microsoft Teams interface, you can access a complete suite of Webex Calling features. The features include directory search, PSTN dialing, speed dial, voicemail, call history, and artificial intelligence-powered background noise removal.

This integrated app works with the Cisco Unified Communications Manager (CUCM) call-control solution, Webex Calling for cloud deployment or the Dedicated Instance offering.

This would be the call flow diagram when using CUCM as the call control:

![A diagram of a telephone call Description automatically generated](module_3_media/media/image1.png)

> **IMPORTANT NOTE:** Make sure you have added the domain (cbXXX.dc-YY.com) to Microsoft tenant in **Add cbXXX.dc-YY.com domain to Microsoft Trial tenant** section of the lab before you are continuing.

**Webex Cloud-Connected UC (CCUC) Overview \[Approx 5 min Read\]:**

![Image](module_3_media/media/image2.jpeg)

Webex Cloud-Connected UC (CCUC) is a suite of Webex cloud services with a single global view to manage on-premises UC and Unified CM cloud services. CCUC is an efficient, cloud-based managed services product for an on-premises Unified CM deployment. It provides a centralized cloud-based tool for analytics and troubleshooting. It allows customers to leverage the benefits of the Webex cloud while keeping critical calling workloads on premises.

Customers can subscribe to the UC management services on Control Hub. Customers can access the Control Hub to get a single global view and host the entire on-premises Unified CM network from a single operation control panel that supports the Cisco cloud services. Cloud-Connected UC helps manage multiple clusters, for both Unified CM and Unified CM Cloud deployments. Cloud-Connected UC achieves this with plugins that are installed on individual Unified CM applications that send telemetry data to the Webex cloud. Plugins register with the Webex cloud during onboarding and are authenticated to the cloud using the Webex Common Identity framework. Subsequent updates to these plugins are automatically managed through the cloud.

CCUC can also help to perform automated device firmware migration from Enterprise Firmware to MPP Firmware. The MPP firmware can run on certain models of the Cisco IP Phone 6800, 7800, and 8800 series. However, only the Cisco IP Phone 7800 and 8800 series can run either MPP firmware or Enterprise firmware. When an appropriate license is applied to the IP Phone, you can migrate between MPP and Enterprise firmware on the Cisco IP 7800 and 8800 series phones.

## Module 3a: Get the Organization ID from Webex Control Hub \[Approx 5 min\]

1.  Open RDP connection to Workstation 3 at 198.18.1.39, using one of the options mentioned in **Accessing your Lab** module. Use the credentials **dcloud\\amckenzie** and **dCloud123!**

2.  Open Chrome Browser from the taskbar or Desktop

3.  From Home Page, select **Cisco Webex Links** \> **Cisco Webex Control Hub**. Log in
    with **cholland@cbXXX.dc-YY.com** and **dCloud*AAAA*!**

    > **NOTE:** You need to Replace **XXX** and **YY** *with your session-specific details. If you haven\'t already done as explained in **Accessing your lab** section, go to **Lab_info.txt** file located oyour workstation 1 and copy the domain.*

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image3.png)

    > **NOTE:** *If you have completed module 3, you may have already configured SSO with Microsoft, in that case the password for* <cholland@cbXXX.dc-YY.com> *would be **dCloud123!***

4.  For security reasons, Webex Control Hub signs out every 20 minutes (Idle timeout) by default. For this lab, let's make the idle time out longer so the Control Hub does not sign you out often during this lab. Go to **MANAGEMENT \> Organization Settings \> Control Hub's idle timeout.** Drop down the option for **Control Hub idle timeout** and select **12 hours** or **no timeout**. Click **Save**.

    > **NOTE**: *If you have completed module 3, you may have already set the idle time out as part of that module. If so, you can skip step 4.*

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image4.png)

5.  Now, go to **MANAGEMENT** \> **Account** and copy the **Organization ID** to a notepad on the Workstation 3 Desktop.

    ![Graphical user interface, application Description automatically generated](module_3_media/media/image5.png)

## Module 3b: Onboard a UC Nodes (UCM & CUC) using the Administrator CLI \[Approx 5 min -- Review Only\]

>**<span style="color: red;">IMPORTANT NOTE:</span>** *When you onboard a on-prem Unified Communications device (like Cisco UCM or Cisco Unity Connection) with Webex Cloud, it takes around 30 to 45 min for the cloud to see it. Instead of making attendess to onboard and wait for 45 min to sync up during the lab, we have pre-onboarded Cisco UCM and Unity Connection for this Lab. ***Below steps are your reference purpose only, you <span style="color: red; font-weight: bold; font-style: italic;">DO NOT</span> need to execute any steps.*** After reviewing below setps you can directly* **move to next module 3c**

1.  Continuing on Workstation 3, open the **Putty** application located on the Desktop.

2.  Open SSH connection to Cisco Unified Communications Manager at **198.18.133.33.** Accept any security warnings, if prompted.

3.  Log in as **administrator** and **dCloud123!** when prompted, and accept any security warnings**.**

4.  Once logged in, at the admin prompt, execute the below command, to start onboarding **Cisco UCM** with Webex.

        utils ucmgmt organization organization_id

    > **NOTE:** *Replace **organization_id** with the Organization ID you copied in above module Step 4.*

5.  Now run the following command to enable the CCUC agent.

        utils ucmgmt agent enable

    ![Text Description automatically generated](module_3_media/media/image6.png)

6.  Run the following command to verify that the CCUC agent is **running**. The Agent process should show the status to be **running.**

        utils ucmgmt agent status

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image7.png)

7.  If the agent process is **not running**, run the following command to kick-start or restart the agent process.
        utils ucmgmt agent restart

    ![A screenshot of a computer Description automatically generated with medium confidence](module_3_media/media/image8.png)

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image9.png)

8.  Check the agent status again with the command, to make sure the agent process status is **running**

        utils ucmgmt agent status


9.  When you see agent process status is **running,** you have initiated the onboarding process successfully. **Make a note of the time that the process moved to the running state, you may need to reference it later.**

10. Now, lets onboard **Cisco Unity Connection** (CUC) node. Open new **Putty** session/window and open SSH connection to **198.18.133.5**, accept any security warnings.

11. Login as **administrator** and **dCloud123!**

12. Repeat setps 4 through 9 for **Cisco Unity Connection** node.

    ![A screenshot of a computer screen Description automatically generated](module_3_media/media/image10.png)

13. Go back to browser tba where you had **Webex Control Hub** opened. Go to **SERVICES** \> **Connected UC** and click **Enable Connected UC**

    ![Graphical user interface, application Description automatically generated](module_3_media/media/image11.png)

14. Once Enabled, click **Get Started** on the **UC Management** tab

    ![Graphical user interface, application, website Description automatically generated](module_3_media/media/image12.png)

15. It will pop-up the **Getting Started** window, which will walk you through creating an agent file for Cisco On-Premises devices.

16. Click **Next** on the **Getting Started** Page.

17. Give the "CCUC-Agent" name in File Name. You can see in this page that if in your real live scenario you have a proxy you can define here the information of that proxy.

18. Click **Save**. You have to wait a couple of minutes while the file agent is created.

    > **NOTE:** *This Agent file does not need to be downloaded in this lab as it\'s already bundled with this version of Cisco UCM (14.0 SU3) but we will create it to get familiar with the process.*

19. Click **Next**.

20. We need to create a new cluster group for Cisco UCM.

21. Give the Cluster Group a **Name** and a **Group Description** of your choice. Example: **dCloud-UCM** and **UCM Group**.

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image13.png)

22. Click **Next** and then click **Finish**.

23. Go to Inventory under UC Management & Click **Add Cluster  Group** again and give Cluster Group Name & Group Description for CUC. Example: **dCloud-CUC** & **CUC Group**. Click **Save**.

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image14.png)

## Module 3c: Verify the onboarded UCM & CUC nodes on Webex Control Hub \[Approx 10 min\]

1.  Continuing on Workstation 3, go back to the browser tab where **Webex Control Hub** was opened and refresh the browser page. Go to **SERVICES** \> **Connected UC**.

2.  On the Connected UC page click **Inventory** under **UC Management.**

3.  You will see there are two **Unassigned** nodes/clusters that needs assignment to a cluster group.

4.  Click **Resolve**.

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image15.png)

5.  On the next page, click **Verify** for cucm1.dcloud**.**cisco.com

    ![](module_3_media/media/image16.png)

6.  It will bring up a new pop-up window for the node. Drop down the option for **Change Cluster Group** and choose **dCloud-CUCM.** Now check mark (towards right side of the node list) option for the product CUCM to confirm Verification and Click Save and Click **Save**.

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image17.png)

7.  You will be taken back to Unverified Cluster Group. Now, click Verify for cuc1.dcloud.cisco.com. Drop down the option for **Change Cluster Group** and choose **dCloud-CUC.** Now click the check mark for the product CUCM to confirm Verification and Click Save and Click **Save**.

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image18.png)

8.  Lastly, on the Control Hub, go to **SERVICES** \> **Connected UC** \> **Inventory** & choose **Details** for dCloud-CUCM. Click **Details** (again). Click on the eclipse icon (three dots) in the top right corner and choose **Service Management**.

    ![A screenshot of a computer Description automatically generated with low confidence](module_3_media/media/image19.png)

9.  Toggle all the settings under Service Management and select the option for **Yes, I agree** and click **Submit**.

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image20.png)

10. Repeat steps 8 & 9 for dCloud-CUC cluster.

    ![A screenshot of a service management Description automatically generated](module_3_media/media/image21.png)

11. Now the Cisco UCM & CUC servers are successfully onboarded with Cisco Webex Cloud. This completes the **Onboard a UC Node using the Administrator CLI** section.

## Module 3d: Configure Single Sign-On (SSO) for Control Hub \[Approx 15 min\]

> **NOTE:** *If you have completed module 3, you would have configured the SSO already as part of that module. So, you can skip this module and go to next module. If you have not run through module 3 yet, you can continue to configure SSO.*

If you have your own identity provider (IdP) in your organization, you can integrate it with Control Hub for single sign-on (SSO). SSO lets your users use a single, common set of credentials for Webex App applications and other applications in your organization.

Cisco Webex supports a wide variety of IdPs for Single Sign-On configuration like Microsoft (both O365 and AD FS), Okta, PingFederate, Duo, etc.,

In this lab, we will explore the SSO configuration with **Microsoft O365**.

Integrating O365 with your Webex Control Hub you can also import/synchronize users and groups from Microsoft O365, Import Avatars (user profile pictures), define user attributes for mapping (like first name, email, etc.,) and configure SSO. In this lab, we will explore SSO configuration only.

1.  Continuing on Workstation 3 and go to the browser tab where you had the **Webex Control hub** open.

2.  On the **Webex Control Hub** page go **MANAGEMENT** \> **Organization Settings** and scroll down to the section **Microsoft Azure Active Directory Wizard App** and click **Set up.**

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image22.png)

3.  It will take you to the Microsoft authentication page. Log in with the Microsoft credentials <cholland@cbXXX.dc-YY.com> & dCloud123! Click **Login**.

    > **NOTE:** ***You need to Replace XXX and YY with your session-specific details. If you haven\'t already done as explained in Accessing  your lab section, go to Lab_info.txt file located oyour workstation 1 and copy the domain.***

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image3.png)

4.  On the following page, Microsoft login page will show you the permissions required. Review the permissions. Check mark option for **Consent on behalf of your organization**. Click **Accept**.

    ![A screenshot of a phone Description automatically generated](module_3_media/media/image23.png)

5.  On the following it will show you all details about permissions that are required for SSO configuration. **Click Accept**.

    ![A screenshot of a application Description automatically generated](module_3_media/media/image24.png)

6.  You will be taken back to Webex Control Hub and a pop-up window will be displayed. Keep the radio button selected for **Sync defaults** and click **Proceed**.

    ![Graphical user interface, text, application, email Description automatically generated](module_3_media/media/image25.png)

7.  It will create the instance/integration with Microsoft tenant. It will take around 2 to 3 minutes for the process to complete.

8.  Once the integration process is completed, Job status will be displayed **NotRun**.

    ![A screenshot of a phone Description automatically generated](module_3_media/media/image26.png)

9.  Within few min the Job status would change to **Active.** Wait until the job status is changed to **Active**. You need to refresh the page to see the updated status. At this point all users from your Microsoft tenant should be imported to Webex under **MANAGEMENT** \> **Users**. Notice few users with status **Verified** indicating they are imported from a trusted source (in this case the Microsoft tenant that we are integrating with).

10. Now go back to **MANAGEMENT** \> **Organization Settings** and scroll down to the **Microsoft Azure Active Directory Wizar App** section. Click the three dots on the right side and select **Edit Configuration**.

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image27.png)

    It will bring up the Microsoft Azure AD integration page, go to the **More** tab. Select the checkbox option for **Activate single sign-on** and click **Save**.

    ![Graphical user interface Description automatically generated](module_3_media/media/image28.png)

11. You have now successfully enabled single sign-on for your Webex tenant. From now on, all logins to this Webex tenant will be redirected to Microsoft for authentication & you will use <cholland@cbXXX.dc-YY.com> & dCloud123! for logging into Webex Control Hub.

12. This completes the SSO configuration and verification.

## Module 3e: Assign Licenses & configure users for Microsoft Presence Sync \[Approx 5 min\]

In this section of lab we will use **Adam Mckenzie** and **Monica Cheng** users. So, lets configure Microsoft & Webex integration parameters for presence & assign Calling Licenses to both these users.

1.  Continuing on Workstation 3, go to the browser tab where you had the **Webex Control Hub** open.

2.  On the Control Hub, go to **SERVICES** \> **Calling**. On the Calling page to Client Settings

3.  On the **Client Settings** page scroll down to Microsoft Teams Integration section and toggle the radio button **Presence sync** & **Hide Webex windows.**

    > **NOTE:** *If you have completed module 4, you may have already toggled on the Presnece Sync and Hide Webex Widnows option.*

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image29.png)

4.  Now, let's assign Webex Calling licenses for users, go to **MANAGEMENT** \> **Users** and choose **Adam McKenzie** (amckenzie@cbXXX.dc-YY.com)**.**

5.  Scroll down on the summary page, click **Edit Licenses**

6.  On the Edit services for <amckenzie@cbXXX.dc-YY.com> page, click **Edit Licenses** again.

7.  On the next page go to **Calling** tab. Check mark option for **Register to Unified Communications Manager (UCM)** & click **Save**. Click **Close**