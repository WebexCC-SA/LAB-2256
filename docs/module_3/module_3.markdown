# **Module 3: Cisco Call for Microsoft Teams (UCM Calling)** \[Approx 1 hour 45 min\]

With Cisco Call for Microsoft Teams for CUCM deployments, the Microsoft Teams users can access the enterprise-grade CUCM experience directly in the Microsoft Teams app. With a single click from the Microsoft Teams interface, you can access a complete suite of CUCM features. The features include directory search, PSTN dialing, speed dial, voicemail, call history, and artificial intelligence-powered background noise removal.

![A screenshot of a phone call AI-generated content may be incorrect.](module_3_media/media/image1.png)

This integrated app works with the Cisco Unified Communications Manager (CUCM) call-control solution, Webex Calling for cloud deployment or the Dedicated Instance offering.

This would be the call flow diagram when using CUCM as the call control:

![A diagram of a telephone call Description automatically generated](module_3_media/media/image2.png)

**Webex Cloud-Connected UC (CCUC) Overview \[Approx 5 min Read\]:**

![Image](module_3_media/media/image3.jpeg)

Webex Cloud-Connected UC (CCUC) is a suite of Webex cloud services with a single global view to manage on-premises UC and Unified CM cloud services. CCUC is an efficient, cloud-based managed services product for an on-premises Unified CM deployment. It provides a centralized cloud-based tool for analytics and troubleshooting. It allows customers to leverage the benefits of the Webex cloud while keeping critical calling workloads on premises.

Customers can subscribe to the UC management services on Control Hub. Customers can access the Control Hub to get a single global view and host the entire on-premises Unified CM network from a single operation control panel that supports the Cisco cloud services. Cloud-Connected UC helps manage multiple clusters, for both Unified CM and Unified CM Cloud deployments. Cloud-Connected UC achieves this with plugins that are installed on individual Unified CM applications that send telemetry data to the Webex cloud. Plugins register with the Webex cloud during onboarding and are authenticated to the cloud using the Webex Common Identity framework. Subsequent updates to these plugins are automatically managed through the cloud.

CCUC can also help to perform automated device firmware migration from Enterprise Firmware to MPP Firmware. The MPP firmware can run on certain models of the Cisco IP Phone 6800, 7800, and 8800 series. However, only the Cisco IP Phone 7800 and 8800 series can run either MPP firmware or Enterprise firmware. When an appropriate license is applied to the IP Phone, you can migrate between MPP and Enterprise firmware on the Cisco IP 7800 and 8800 series phones.

## Module 3a: Get Webex Org ID from Control Hub \[Approx 5 min\]

1.  Open RDP connection to Workstation 3 at 198.18.1.39, using one of the options mentioned in **Accessing your Lab** module. Use the credentials **dcloud\\amckenzie** and **dCloud123!**

2.  Open Chrome Browser from the taskbar or Desktop

3.  From Home Page, select **Cisco Webex Links** \> **Cisco Webex Control Hub**. Log in with **cholland@cbXXX.dc-YY.com** and **dCloud*AAAA*!**

    > **NOTE:** You need to Replace **XXX** and **YY** *with your session-specific details. If you haven\'t already done as explained in **Accessing your lab** section, go to **Lab_info.txt** file located in your workstation 1 and copy the domain.*

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image4.png)

    > **NOTE:** *If you have completed module 2 you may have already configured SSO with Microsoft, in that case the password for <cholland@cbXXX.dc-YY.com> would be **dCloud123!***

4.  For security reasons, Webex Control Hub signs out every 20 minutes (Idle timeout) by default. For this lab, let's make the idle time out longer so the Control Hub does not sign you out often during this lab. Go to **MANAGEMENT \> Organization Settings \> Control Hub's idle timeout.** Drop down the option for **Control Hub idle timeout** and select **12 hours** or **no timeout**. Click **Save**.

    > **NOTE**: *If you have completed module 2 you may have already set the idle time out as part of that module. If so, you can skip step 5.*

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image5.png)

5.  Now, go to **MANAGEMENT** \> **Account** and copy the **Organization ID** to a notepad on the Workstation 3 Desktop.

    ![Graphical user interface, application Description automatically generated](module_3_media/media/image6.png)

## Module 3b: Onboard a UC Nodes (UCM & CUC) using the Administrator CLI \[Approx 10 min -- <span style="color:red;">***Review Only***</span>\]

> <span style="color:red;">**IMPORTANT NOTE:**</span> When you onboard an on-prem Unified Communications device (like Cisco UCM or Cisco Unity Connection) with Webex Cloud, it takes around 30 to 45 min for the cloud to see it. Instead of making attendees onboard and wait for 45 min to sync up during the lab, we have pre-onboarded Cisco UCM and Unity Connection for this Lab. **Below steps are your reference purpose only**, you <span style="color:red;">**DO NOT need to execute any steps**</span>. After reviewing below steps you can directly move to next module 3c.

1.  Continuing on Workstation 3, open the **Putty** application located on the Desktop.

2.  Open SSH connection to Cisco Unified Communications Manager at **198.18.133.33.** Accept any security warnings, if prompted.

3.  Log in as **administrator** and **dCloud123!** when prompted and accept any security warnings.

4.  Once logged in, at the admin prompt, execute the below command, to start onboarding **Cisco UCM** with Webex.

    ```
    utils ucmgmt organization **organization_id**
    ```

    **NOTE:** *Replace **organization_id** with the Organization ID you copied in above module Step 4.*

5. Now run the following command to enable the CCUC agent.

    ```
    utils ucmgmt agent enable
    ```

    ![Text Description automatically generated](module_3_media/media/image7.png)

6. Run the following command to verify that the CCUC agent is **running**. The Agent process should show the status to be **running.**

    ```
    utils ucmgmt agent status
    ```

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image8.png)

7. If the agent process is **not running**, run the following command to kick-start or restart the agent process.

    ```
    utils ucmgmt agent restart
    ```

    ![A screenshot of a computer Description automatically generated with medium confidence](module_3_media/media/image9.png)

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image10.png)

8. Check the agent status again with the command, to make sure the agent process status is **running**

    ```
    utils ucmgmt agent status
    ```

9. When you see agent process status is **running,** you have initiated the onboarding process successfully. **Make a note of the time that the process moved to the running state, you may need to reference it later.**

10. Now, let's onboard **Cisco Unity Connection** (CUC) node. Open new **Putty** session/window and open SSH connection to **198.18.133.5**, accept any security warnings.

11. Login as **administrator** and **dCloud123!**

12. Repeat steps 4 through 9 for **Cisco Unity Connection** node.

    ![A screenshot of a computer screen Description automatically generated](module_3_media/media/image11.png)

13. Go back to browser tab where you had **Webex Control Hub** opened. Go to **SERVICES** \> **Connected UC** and click **Enable Connected UC**

    ![Graphical user interface, application Description automatically generated](module_3_media/media/image12.png)

14. Once Enabled, click **Get Started** on the **UC Management** tab

    ![Graphical user interface, application, website Description automatically generated](module_3_media/media/image13.png)

15. It will pop-up the **Getting Started** window, which will walk you through creating an agent file for Cisco On-Premises devices.

16. Click **Next** on the **Getting Started** Page.

17. Give the "CCUC-Agent" name in File Name. You can see in this page that if in your real live scenario you have a proxy you can define here the information of that proxy.

18. Click **Save**. You have to wait a couple of minutes while the file agent is created.

    **NOTE**: This Agent file does not need to be downloaded in this lab as it\'s already bundled with this version of Cisco UCM (14.0 SU3) but we will create it to get familiar with the process.

19. Click **Next**.

20. We need to create a new cluster group for Cisco UCM.

21. Give the Cluster Group a **Name** and a **Group Description** of your choice. Example: **dCloud-UCM** and **UCM Group**.

    ![A screenshot of a computer Description  automatically generated](module_3_media/media/image14.png)

22. Click **Next** and then click **Finish**.

23. Go to Inventory under UC Management & Click **Add Cluster Group** again and give Cluster Group Name & Group Description for CUC. Example: **dCloud-CUC** & **CUC Group**. Click **Save**.

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image15.png)

24. This completes onboarding of On-Prem Cisco UC applications.

## Module 3c: Verify the onboarded UCM & CUC nodes on Webex Control Hub \[Approx 10 min\]

1.  Continuing on Workstation 3, go back to the browser tab where **Webex Control Hub** was opened. Or if you have not yet logged in, go to <https://admin.webex.com> & log in with **cholland@cbXXX.dc-YY.com** and **dCloud*AAAA*!** Or **dCloud123!** (if you have configured SSO as part of module 2)

    > **NOTE:** You need to Replace **XXX** and **YY** *with your session-specific details. If you haven\'t already done as explained in **Accessing your lab** section, go to **Lab_info.txt** file located your workstation 1 and copy the domain. AAAA is the last 4 digits of your session ID on dCloud*

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image4.png)

2.  Once logged in, go to **SERVICES** \> **Connected UC**.

3.  On the Connected UC page click **Inventory** under **UC Management.** If you do not see inventory option, refresh the page.

4.  You will see there are two **Unassigned** nodes/clusters that needs assignment to a cluster group.

5.  Click **Resolve**.

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image16.png)

6.  On the next page, click **Verify** for cucm1.dcloud**.**cisco.com

    ![Image](module_3_media/media/image17.png)

7.  It will bring up a new pop-up window for the node. Drop down the option for **Change Cluster Group** and choose **dCloud-CUCM.** Now check mark (towards right side of the node list) option for the product CUCM to confirm Verification and Click Save and Click **Save**.

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image18.png)

8.  You will be taken back to Unverified Cluster Group. Now, click Verify for cuc1.dcloud.cisco.com. Drop down the option for **Change Cluster Group** and choose **dCloud-CUC.** Now click the check mark for the product CUCM to confirm Verification and Click Save and Click **Save**.

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image19.png)

9.  Lastly, on the Control Hub, go to **SERVICES** \> **Connected UC** \> **Inventory** & choose **Details** for dCloud-CUCM. Click **Details** (again). Click on the eclipse icon (three dots) in the top right corner and choose **Service Management**.

    ![A screenshot of a computer Description automatically generated with low confidence](module_3_media/media/image20.png)

10. Toggle all the settings under Service Management and select the option for **Yes, I agree** and click **Submit**.

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image21.png)

11. Repeat steps 9 & 10 for dCloud-CUC cluster.

    ![A screenshot of a service management Description automatically generated](module_3_media/media/image22.png)

12. Now the Cisco UCM & CUC servers are successfully onboarded with Cisco Webex Cloud. This completes the **Onboard a UC Node using the Administrator CLI** section.

## Module 3d: Configure Single Sign-On (SSO) for Control Hub \[Approx 15 min\]

> **NOTE**: *If you have completed module 2, you would have configured the SSO already as part of that module. So, you can skip this section and go to next section. If you have not run through module 2 yet, you can continue to configure SSO*.

If you have your own identity provider (IdP) in your organization, you can integrate it with Control Hub for single sign-on (SSO). SSO lets your users use a single, common set of credentials for Webex App applications and other applications in your organization.

Cisco Webex supports a wide variety of IdPs for Single Sign-On configuration like Microsoft (both O365 and AD FS), Okta, PingFederate, Duo, etc.,

In this lab, we will explore the SSO configuration with **Microsoft O365**.

Integrating O365 with your Webex Control Hub you can also import/synchronize users and groups from Microsoft O365, Import Avatars (user profile pictures), define user attributes for mapping (like first name, email, etc.,) and configure SSO. In this lab, we will explore SSO configuration only.

1.  Continuing on Workstation 3 and go to the browser tab where you had the **Webex Control hub** open.

2.  On the **Webex Control Hub** page go **MANAGEMENT** \> **Organization Settings** and scroll down to the section **Microsoft Entra ID Wizard App** and click **Set up.**

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image23.png)

3.  It will take you to the Microsoft authentication page. Log in with the Microsoft credentials <cholland@cbXXX.dc-YY.com> & **dCloud123!** Click **Login**.

    > **NOTE**: ***You need to Replace XXX and YY with your session-specific details. If you haven\'t already done as explained in Accessing your lab section, go to Lab_info.txt file located on your **workstation 1** and copy the domain.***

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image4.png)

4.  On the following page, Microsoft login page will show you the permissions required. Review the permissions. Check mark option for **Consent on behalf of your organization**. Click **Accept**.

    ![A screenshot of a phone Description automatically generated](module_3_media/media/image24.png)

5.  On the following it will prompt you for admin credenatils. Choose cholland@cbXXX.dc-YY.com from available logins & then it will show you all details about permissions that are required for SSO configuration. Click **Accept**.

    ![A screenshot of a application Description automatically generated](module_3_media/media/image25.png)

6.  You will be taken back to Webex Control Hub and a pop-up window will be displayed. You might be asked if you want to create a new app ir migrate an existing one. If that's the case, select "Create new app". If not, go to the next step.

    ![A screenshot of a application Description automatically generated](module_3_media/media/image11b.png)

7. Then, you will be prompted with another pop-up window. Keep the radio button selected for **Sync defaults** and click **Proceed**.

    > **NOTE:** *If Sync defaults is not prompted, scroll down to Entra ID App section on Organizations settings page.*

    ![Graphical user interface, text, application, email Description automatically generated](module_3_media/media/image26.png)

8.  It will create the instance/integration with Microsoft tenant. It will take around 2 to 3 minutes for the process to complete.

9.  Once the integration process is completed, Job status will be displayed **NotRun**.

    ![A screenshot of a phone Description automatically generated](module_3_media/media/image27.png)

10.  Within few min the Job status would change to **Active.** Wait until the job status is changed to **Active**. You need to refresh the page to see the updated status. At this point all users from your Microsoft tenant should be imported to Webex under **MANAGEMENT** \> **Users**. Notice few users with status **Verified** indicating they are imported from a trusted source (in this case the Microsoft tenant that we are integrating with).

11. Now go back to **MANAGEMENT** \> **Organization Settings** and scroll down to the **Microsoft Azure Active Directory Wizard App** section. Click the three dots on the right side and select **Edit Configuration**.

    ![A screenshot of a computer Description automatically generated](module_3_media/media/image28.png)

12.  It will bring up the Microsoft Azure AD integration page, under **Attributes** tab drop down the field **phoneNumbers\[type eq "work"\].value** & choose **telephoneNumber** from the drop down list.

    ![A screenshot of a computer AI-generated content may be incorrect.](module_3_media/media/image29.png)

13.  Now, go to **More** tab and select the checkbox option for **Activate single sign-on** and click **Save**.

    ![A screenshot of a computer AI-generated content may be incorrect.](module_3_media/media/image30.png)

14. You have now successfully enabled single sign-on for your Webex tenant. From now on, all logins to this Webex tenant will be redirected to Microsoft for authentication & you will use <cholland@cbXXX.dc-YY.com> & dCloud123! for logging into Webex Control Hub.

15. This completes the SSO configuration and verification.

## Module 3e: Assign Licenses & Configure Users for Microsoft Presence Sync [Approx 5 min]

In this section of the lab, we will use **Adam McKenzie** and **Monica Cheng** users. Let’s configure Microsoft & Webex integration parameters for presence and assign Calling Licenses to both these users.

1. Continuing on **Workstation 3**, go to the browser tab where you had the **Webex Control Hub** open. If you need to log in to Webex Control Hub, use the credentials `<cholland@cbXXX.dc-YY.com>` and **dCloud123!**.

2. On the Control Hub, go to **SERVICES** > **Calling**. On the Calling page, go to **Client Settings**.

3. On the **Client Settings** page, scroll down to the Microsoft Teams Integration section and toggle the radio button **Presence Sync** & **Hide Webex windows.** If the option **Set Microsoft Teams as the default app for calling dock** is toggled ON, untoggle it for now. We will explore this option later.

    > **NOTE:** *If you have completed Module 2, you may have already toggled on the Presence Sync and Hide Webex Windows options.*

    ![Image](module_3e3f_media/media/image1.png)

4. Now, let's assign UCM licenses for users. Go to **MANAGEMENT** > **Users** and choose **Adam McKenzie** (`amckenzie@cbXXX.dc-YY.com`).

5. Scroll down on the summary page, and click **Edit Licenses**.

6. On the **Edit services for amckenzie@cbXXX.dc-YY.com** page, click **Edit Licenses** again.

7. On the next page, go to the **Calling** tab. Checkmark **Register to Unified Communication Manager (UCM)**. Also, **uncheck** options for **Messaging** and **Meeting** to deploy phone-only services for this user. Click **Save**. Click **Close** for edit services for <amckenzie@cbXXX.dc-YY.com>.

    ![Image](module_3e3f_media/media/image2.png)

8. Go back to **MANAGEMENT** > **Users** again, and on the users' page, choose **Monica Cheng** (`mcheng@cbXXX.dc-YY.com`) and repeat steps 4 through 7 to assign the **Register to Unified Communications Manager (UCM)** License for calling.

---

## Module 3f: Update User Contacts, publish Cisco Call app and disable Microsoft Native Calling [Approx 5 min]

Now let's update contact phone numbers for users **Adam McKenzie** and **Monica Cheng** on the Microsoft trial tenant so users will be able to call with the click-to-call feature from Teams. Also, as we are using Webex Calling (UCM Calling) for calling services, let’s disable the native Microsoft calling option so users are not confused between both calling options.

1. Continuing on **Workstation 3**, open a new browser tab and from the home page, go to **Collab Admin Links** > **Microsoft Admin Center** or directly go to <https://admin.microsoft.com>. Log in with the credentials `<cholland@cbXXX.dc-YY.com>` and **dCloud123!** if prompted.

2. Once logged in, go to **Users** > **Active Users** on the left-side pane.

3. On the Active Users page, select **Adam McKenzie**. This will bring up a fly-out window for the user configuration. Scroll down a little and click **Manage contact information**.

    ![Image](module_3e3f_media/media/image3.png)

4. On the **Manage contact information** page, scroll down and find **Office phone**. Enter **6016**. Click **Save changes**. Click **Close** to close the fly-out window.

    ![Image](module_3e3f_media/media/image4.png)

5. Similarly, repeat steps 3 and 4 for **Monica Cheng** and update the office phone number with extension **6020**.

    > **NOTE:** *Sometimes Microsoft takes a long time to update contact information, and it may not immediately reflect on Microsoft Teams. This is not a limitation of the lab or Webex, but rather Microsoft Cloud taking longer to update contact information.*

---

    Now let’s publish and authorize the **Cisco Calling app** for the entire Microsoft Organization so that each user is not prompted for authorization. Additionally, we will disable the native Microsoft calling option so users are not confused between Microsoft Native Calling and Cisco Call.

6. First, we are going to hide the Teams-to-Teams Calling button. Go back to where you have logged into **Microsoft Admin Center**. On the left-side page, click **Show all** to see all admin centers. Under **Admin Centers**, select **Teams**.

    ![Image](module_3e3f_media/media/image5.png)

7. It will open the **Microsoft Teams Admin Center** in a new tab. Once the Teams Admin Center is opened, go to **Voice** > **Calling policies**. On the Calling Policies page, select the radio button for **Disallow Calling** and click on **Manage Users/Assign users.**

    ![Image](module_3e3f_media/media/image6.png)

8. It will bring up fly-window to assign users. Search and add the users **Adam McKenzie** and **Monica Cheng**, and click on **Apply**. Click **Confirm** in the pop-up window.

    ![Image](module_3e3f_media/media/image7.png)

    ![Image](module_3e3f_media/media/image8.png)

    > **NOTE:** *If you have completed Module 2, you may have already published the **Cisco Call** app. If so, you can skip the remaining steps (4 through 9) and proceed to Module 3g.*

9. Now, let’s publish the Cisco Call app for the organization so that each user does not need to request admin authorization. Continuing in the **Teams Admin Center**, on the left-side page, go to **Teams apps** > **Manage apps.**

10. On the Manage Apps page, search for **Cisco Call** on the right. Select the **Cisco Call** app that is listed.

    ![Image](module_3e3f_media/media/image9.png)

11. On the Cisco Call app page, go to the **Permissions** tab. Under the Permissions tab, click **Grant admin consent.** It will bring up a pop-up window to authorize as admin. Log in as `<cholland@cbXXX.dc-YY.com>` and **dCloud123!**. It will prompt you to accept some permissions. Click **Accept.**

    ![Image](module_3e3f_media/media/image10.png)

    ![Image](module_3e3f_media/media/image11.png)

    > **NOTE:** *Some permissions are considered delegated level, and others are application level. Below is a description of the permissions used by Cisco Call for Microsoft Teams, and what changes are coming in June 2025.*

    ![Image](module_3e3f_media/media/image12.png)

    ![Image](module_3e3f_media/media/image13.png)

12. Now any user in the organization can go to Apps in **Microsoft Teams** and add the **Cisco Call** app from the store.

    > **NOTE:** *As an Organization Admin, you can also install/publish this app for all users. To publish the app for all users, go to **Teams apps** > **Setup policies** and update **Global (Org-wide default)** to include the **Cisco Call** app.*

    ![Image](module_3e3f_media/media/image14.png)

13. At this point, Microsoft and Webex tenants & users are ready for use.

This completes **Update User Contacts, publish Cisco Call app and disable Microsoft Native Calling**.

## Module 3g: Testing the Calls for Microsoft Integration with Webex (UCM Calling) [Approx 60 min]

In this module, we will make some test calls to internal, PSTN & also configure multiple features and Hunt groups. This module consists of a total of 10 testing scenarios that are described below.

---

#### Logging into Clients [Approx 10 min]

> **NOTE**: *You can continue using Teams Classic or choose to update to the version being prompted. Pleas be aware we do not control Microsoft updates.*

1. Continuing on **Workstation 3**, open Microsoft Teams and log in as `<amckenzie@cbXXX.dc-YY.com>` with password **dCloud123!**. Click **OK**. Click **Done**.

    > **NOTE:** *DO **NOT** click **No, this app only**.*

    ![Image](module_3g_media/media/image1.png)

2. **Accept** any information/warning messages while logging in. If you have added Cisco Call as an admin in Module 2c, jump to step 3. If not, once logged in, click the eclipse icon (three dots) on the left side pane. On the new fly-out window, search for **Cisco Call**. It will list the Cisco Call app. Click **Add**. It will add the **Cisco Call app** to Microsoft Teams and take you to the login screen.

    ![Image](module_3g_media/media/image2.png)

3. Open the Cisco Call App and click **Continue**.

    ![Image](module_3g_media/media/image3.png)

4. This will use the same email address used to log in to Microsoft Teams. As we have an active session, you will be signed into **Cisco Call** on Microsoft Teams.

5. At this point, the Webex App will pop up for you to log in. Log in as `<amckenzie@cbXXX.dc-YY.com>` with password **dCloud123!** If you close the Webex login page, you can access it from the System Tray.

    ![Image](module_3g_media/media/image4.png)

6. As we chose to hide the Webex windows, once the user logs in, the Webex App window will disappear. You will be prompted with a pop-up window to sign in to UCM services. Log in as **amckenzie** with **dCloud123!**.

    ![Image](module_3g_media/media/image5.png)

7. You will be prompted with a notification about Emergency Calling. Click **OK**.

    ![Image](module_3g_media/media/image6.png)

8. You might get a pop-up window guiding you through the new features of the Cisco Call app. Click on **Next**. Then, click on **Later** when it asks you to use the Calling Dock, as we will explore this feature later.

    ![Image](module_3g_media/media/image7.png)

9. Finally, right-click on the **Cisco Call app** on the left-side pane and click **Pin**. This ensures it is always visible for easier access. If you have published the **Cisco Call app** for the entire organization under setup policies on the **Microsoft Teams Admin Center**, you will see the **Cisco Call app** pinned already.

    ![Image](module_3g_media/media/image8.png)

    > **NOTE:** *If you do not see the **Cisco Call** app on the left side, click on the three dots on the left-side pane again, right-click on the **Cisco Call app**, and select **Pin** so the application always displays on the left-side pane for easier access.*

10. Now both of your clients on **Workstation 3** are ready for use.

11. Open an RDP connection to **Workstation 4** using one of the methods described in the **Accessing Your Lab** module above. Repeat the steps above (1 through 9) on Workstation 4 using the credentials `<mcheng@cbXXX.dc-YY.com>` with password **dCloud123!**.

> **NOTE**: *Make sure you are logged in to both clients on both workstations 3 and 4 before continuing*.


---

### Module 3g.1: **Calling Scenarios 1 of 10** -- Making calls \[Approx 5 min\]


After configuring Cloud Connected UC, we should have Presence sync, Call History and Voicemail populated on our landing page. However, please notice these settings take up to 8 hours to apply, so you might not see this working.

Optional reading: reason why this process takes 8 hours explained in the following diagram:

![A diagram of a web page Description automatically generated with medium confidence](module_3_media/media/image48.png)

1.  Make sure you are logged in to both clients on both workstations 3 and 4 before continuing. From workstation 3 as **Adam McKenzie**, go to **Cisco Call** app on Microsoft Teams (On left side pane) & Search for **Monica Cheng** (right above dial pad). **OR** you can dial extension number 6020.

2.  It will search the directory for **Monica Cheng** and display options to call, click on either Audio or Video. It will display all available contact methods for Monica, like Phone number Email etc., Click on any of the options to place the call.

    ![A screenshot of a phone call AI-generated content may be incorrect.](module_3_media/media/image49.png)

3.  Answer the call on workstation 4. Verify that call gets connected. Wait for few seconds and hang up the call.

    **Once the 8 hour has been passed after onboarding UCM cluster**:

4.  Once the 8 hours has been passed after onboarding UCM Cluster, you will see the call presence status on Microsoft Teams as **In a call**, as shown below.

    > **NOTE**: *If you do not see the correct status, try to bring the Microsoft Teams into foreground or initiate a chat conversation between Adam and Monica.*

    ![A screenshot of a video chat Description automatically generated](module_3_media/media/image50.png)

5.  As soon as the call is hung up, you will see that Adam's status changes to **Available**.

    ![A screenshot of a computer Description  automatically generated](module_3_media/media/image51.png)

6.  Similarly you can dial any PSTN number in E.164 format (+1AAABBBCCCC). Or you can dial the Cisco support number +**18005532447**. You can also make inbound calls to Adam McKenzie DID number (you can find it in session details or in the file lab_info.txt) from your mobile. If you cannot dial US phone numbers from your mobile, reach out to one of your proctors.

7.  Also, Once the 8 hours has been passed after onboarding UCM Cluster, you will be able to observe that up to date call history is synchronized/reflected to **Cisco Call** app on Microsoft Teams. To verify the call history go to **Cisco Call app** \> **Recent Calls** as shown below.

    ![Image](module_3_media/media/image52.png)

### Module 3g.2: **Calling Scenarios 2 of 10** - Making calls from Microsoft Teams chat Window \[Approx 5 min\]

1.  Continuing on Workstation 3, go to Microsoft Teams app and go to **Chat** on left side pane. On the top search window search for **Monica Cheng**.

    ![Image](module_3_media/media/image53.png)

2.  Initiate a chat conversation with Monica and send few messages back and forth.

3.  Click on the + sign towards right side of typing window for chat and select **Cisco Call** from available options.

    ![A screenshot of a computer AI-generated content may be incorrect.](module_3_media/media/image54.png)

4.  It will bring up available calling options for **Monica Cheng**. Choose either **Phone number** or **Email Id** from the drop down option. Then choose either **Audio** or **Video** option to make the call.

    ![A screenshot of a phone call Description automatically generated](module_3_media/media/image55.png)

5.  Answer the call on Workstation 4 and verify that call is connected. Hang up the call after few seconds.

    > **NOTE**: *As explained before once the 8 hours for the initial sync has passed, you will see the presence status updated to show that Adam (and Monica) **In a call**.*

    ![A screenshot of a chat Description automatically generated](module_3_media/media/image56.png)

### Module 3g.3: **Calling Scenarios 3 of 10** - Optimize Webex App for Microsoft Teams Experience \[Approx 3 min\]

We are going to enable a feature on Control Hub that makes the Webex App optimized for being used with Microsoft Teams. This option enables:

* Webex branding removal
* Linking Calling Dock to MS Teams (shortcut to Call History, Voicemail, and Simplified Call Settings)
* Ability to mute Webex calls when on Teams meetings

---

1. Continuing on Workstation 3, go back to the browser tab where you logged into **Webex Control Hub**. On Control Hub, go to **MANAGEMENT** > **Users**, choose user **Adam McKenzie.** On the user page, go to the **Calling** tab. On the calling tab, scroll down to **Call Settings** > **Microsoft Teams Integration**. On the Microsoft Teams integration page, toggle on for option **Optimize Webex App for Microsoft Teams Experience.** Click on **Save.**

    ![Image](module_3g3-8_media/media/image1.png)

2. Restart the Webex App to apply the changes by clicking on **Exit** from the System tray (right-click + Exit).

    ![Image](module_3g3-8_media/media/image52.png)

7. Then, click on **Sign in** on the banner that shows the Cisco Call tab to re-open the Webex App.

    ![Image](module_3g3-8_media/media/image53.png)

---

### Module 3g.4 (NEW): **Calling Scenarios 4 of 10** - Making a Call with the Optimized Experience

> **NOTE:** *Make sure you are logged in to both clients on both Workstations 3 and 4 before continuing.*

1. Continuing on Workstation 3 as **Adam McKenzie**, go to the **Cisco Call** app on Microsoft Teams and make another call to **Monica Cheng**.

2. Notice the Webex logo is not shown within the in-call window anymore, as the option **Optimize Webex App for Microsoft Teams Experience** is enabled for this user.

    ![Image](module_3g3-8_media/media/image2.png)

3. Hang up the call.

---

### Module 3g.5 (NEW): **Calling Scenarios 5 of 10** - Presence Sync: Mute Webex App Calls When on Teams Meetings [Approx 10 min]

> **NOTE:** *This scenario will only work after 8 hours from configuring CCUC have passed.*

Presence sync is supported between Microsoft Teams and Webex for the following statuses:

![Image](module_3g3-8_media/media/image3.png)

When on a **Microsoft Teams meeting or call**, users might want to decide if they want to receive or decline calls. The status when on a Teams Meeting or a call will show as **"In a call"** in Microsoft Teams, and as **"On a call"** in the Webex App.

However, this presence status itself doesn't mean incoming calls will be muted, but two settings are required for this to happen:

- **Organizational setting**: **Optimize Webex App for Microsoft Teams Experience** must be enabled for the user, group, or organization.
- **User setting**: Under **Call Settings**, Call Notifications can be set to **Always mute** or to **Only mute notifications when I'm in a meeting or on a call**. These settings apply to either Webex calls or meetings, and also to Microsoft Calls and Meetings if the option **"Optimize Webex App for Microsoft Teams Experience"** is enabled for that user.

    ![Image](module_3g3-8_media/media/image4.png)

#### Let's explore the option **Only mute notifications when I'm in a meeting or on a call.**

1. Continuing on Workstation 3, go to **Microsoft Teams**. Go to the **Meet** tab and click on **Meet now**. Then click on **Start a meeting** to start a Microsoft Teams meeting. 

    ![Image](module_3g3-8_media/media/image5.png)

2. Select any audio option and click on **Join now**. Click close for option **Invite people to join you** pop-up window

    ![Image](module_3g3-8_media/media/image6.png)

3. Leave the meeting open and go back to the **Cisco Call** tab within Microsoft Teams. Notice Adam's status has changed to "In a call."

    ![Image](module_3g3-8_media/media/image7.png)

4. Open **Call Settings** within the Cisco Call tab. It will bring up settings for the Webex App. Notice that Call Settings are now simplified in comparison to the default Call Settings from the Webex App (**Simplified Call Settings**).

    ![Image](module_3g_media/media/image14.png)

4. On the settings, go to **Notifications**. Under Notifications, click on **Calls**. Ensure the option **Don't mute** is selected. Click **Save.**

    ![Image](module_3g3-8_media/media/image8.png)

5. Now, navigate to **Workstation 4** and open Microsoft Teams (as Monica Cheng). From the Cisco Call tab, make a call to Adam McKenzie's work number.

    ![Image](module_3g3-8_media/media/image9.png)

6. On Workstation 3, notice Adam McKenzie gets the call notification toast. Decline the call on Workstation 3 and/or hang up the call on Workstation 4.

    ![Image](module_3g3-8_media/media/image10.png)

7. Now, on Workstation 3, open **Call Settings** within the Cisco Call tab and go to **Notifications**. Under Notifications, click on **Calls**. Select the option **Only mute notifications when I'm in a meeting or on a call**. Click on **Save.**

    ![Image](module_3g3-8_media/media/image11.png)

8. Repeat the call from Monica Cheng to Adam McKenzie: Navigate to **Workstation 4** and open Microsoft Teams (as Monica Cheng). From the Cisco Call tab, make a call to Adam's work number.

    ![Image](module_3g3-8_media/media/image12.png)

9. Notice Monica Cheng can make the call, but Adam McKenzie doesn't receive any notification toast while the call is happening. Hang up the call from **Workstation 4**, as Monica Cheng.

    ![Image](module_3g3-8_media/media/image13.png)

10. Adam will get a missed call.

11. Still on Workstation 3, open the Microsoft meeting window and finish the Microsoft Teams meeting.

    ![Image](module_3g3-8_media/media/image14.png)

12. Open again **Call Settings** from the Cisco Call tab within Microsoft Teams and change the **Call Notifications** settings back to **Don't Mute**. Click on **Save.**

    ![Image](module_3g3-8_media/media/image15.png)

---

### Module 3g.6: **Calling Scenarios 6 of 10** - Calling Dock [Approx 5 min]

The Webex Calling Dock (formerly multi-call window) is a user-enabled setting to maximize calls for multiple lines and manage calls effectively. It can act as a companion app for Microsoft Teams. It also helps to hide the Webex app during calls.

![Image](module_3g3-8_media/media/image16.png)

1. Continuing on Workstation 3, on Microsoft Teams go to the **Cisco Call** app on the left-side pane. Click on the ellipsis menu on the right-hand side (next to Call Settings) and toggle on the Calling Dock to enable it.

    ![Image](module_3g3-8_media/media/image17.png)

2. Notice that Webex will bring a small call window (called as Calling Dock) as shown above. You can use this **Calling Dock** for any calling functions, like making calls, answering calls, recent calls, using the dial pad, and accessing voicemail.

3. Drag and drop the Calling Dock to the right side of the screen to notice it minimizes itself (docking feature).

    ![Image](module_3g3-8_media/media/image18.png)

4. Hover your mouse over the new dock icon on the right to see the **Calling Dock** without keeping it open. Click on the dock to maximize the **Calling Dock** again.

    ![Image](module_3g3-8_media/media/image19.png)

---

### Module 3g.7: **Calling Scenarios 7 of 10** - Multi-Line [Approx 10 min]

You can set up a profile with multiple lines with different phone numbers for calling. You can switch lines if you need to make outgoing calls from different lines, such as a front desk line, support team line, or an individual line with a different caller ID.

Let's add a multi-line (secondary line) to **Adam McKenzie**.

1. Continuing on **Workstation 3**, open a new browser tab & from the home page go to **Collaboration Admin Links** > **Cisco Unified Communications Manager**. Log in as **administrator/dCloud123!**.

2. Once logged in, go to **Device** > **Phone**. On the Find and List Phones page, drop down the option for **Find Phone where** to **Description**, **contains**, and in the search field type **mckenzie** (Adam's last name) and click **Find**.

    ![Image](module_3g3-8_media/media/image23.png)

3. From the search results, choose/click the device **CSFAMCKENZIE**.

4. On the phone page, click on **Line [2] -- add a new DN** (towards the top-left corner).

    ![Image](module_3g3-8_media/media/image24.png)

5. It will take you to the new **Directory Number Configuration** page. On the page populate the following details and click **Save**.

    | Parameter Name           | Value                              |
    |--------------------------|------------------------------------|
    | Directory Number         | 7016                              |
    | Route Partition          | Base_PT                           |
    | Voice Mail Profile       | Default                           |
    | Calling Search Space     | Call_Everyone                     |
    | Display (Caller ID)      | Adam McKenzie - x7016             |
    | ASCII Display (Caller ID)| Adam McKenzie - x7016             |
    | Line Text Label          | Adam McKenzie - x7016             |
    | Options                  | Caller Name & Dialed Number       |

    ![Image](module_3g3-8_media/media/image25.png)

    ![Image](module_3g3-8_media/media/image26.png)

6. Once saved, scroll down all the way to the bottom of the directory number page. You will see the option called **Users Associated with Line**. Click on **Associate End Users**. It will bring up the Find and List Users page. In the search field, enter **Adam** and click **Find**. It will list the user ID **amckenzie**. Checkmark the user and click **Add Selected**.

    ![Image](module_3g3-8_media/media/image27.png)

7. It will associate the user and take you back to the **Directory Number Configuration** page. Click **Save**. Click **Apply Config**. Click **OK** on the pop-up window.

8. Now go to the Calling Dock, and you will have two lines configured. If you do not see the second line yet, just quit (from the system tray, right-click on the Webex icon and Exit Webex) & Connect Phone services on the Cisco Call app within Microsoft Teams.

9. Observe on the Calling Dock you now have two lines configured.

    ![Image](module_3g3-8_media/media/image28.png)

10. Go to Microsoft teams & Cisco Call app.  Click on **Call Settings**.  It will bring up Settings pop-up window for Webex. Uncheck the option for **Answer calls with my video on** under Calling tab.  Click **Save**.

    ![Image](module_3g3-8_media/media/image28_2.png)

11. Go to Workstation 4 (as **Monica Cheng**). On Microsoft Teams, go to the **Cisco Call** app and dial **7016** (the **secondary line** that we configured). Answer the call on Workstation 3. Verify that the call is connected, wait for a few seconds, and hang up the call.

12. As explained before, once the 8 hours for the initial sync has passed, you will see the presence status updated to show that Adam is **"In a call"** when the second line is in use, just like the primary line.

    ![Image](module_3g3-8_media/media/image29.png)

---

### Module 3g.8: **Calling Scenarios 8 of 10** - Voicemail [Approx 5 min]

1. If you can dial US numbers from your mobile phone, dial the DID number you noted for **Adam McKenzie** (from Session Details) in the Accessing the Lab module. If you cannot dial US numbers, you can contact one of your proctors to make the call for you.

    > **NOTE:** *If you have not noted the DID number at the beginning of the lab, you can find the DID number by going to your **dCloud Lab** > **Session Details** and noting the DID number associated with extension number **6016** (it will be labeled as **Adam McKenzie**).*

2. Do not answer the call on Workstation 3 & let it go to voicemail (or decline the call). Leave a voice message for a few seconds and hang up the call.

3. As explained before, once 8 hours have passed since the CCUC is onboarded, you can go to **Microsoft Teams** > **Cisco Call** app and go to the Voicemail tab. Observe that you have a new voicemail. Click **Play** to listen to the voicemail. Make sure you can listen to the voicemail.

    ![Image](module_3g3-8_media/media/image30.png)

---

### Module 3g.9 (NEW): **Calling Scenarios 9 of 10** - Phone Disconnection Banner [Approx 3 min]

> **NOTE:** *If you have completed Module 2, skip to the next Calling scenario.*

When phone services are disconnected (for example, when the Webex App is logged out), there will be a banner showing that in the Cisco Call App. It also appears when it detects the Webex App is not running (when you exit from it), as we have seen before. Let's test the experience when signing out from the Webex App.

1. Continuing on **Workstation 3** as **Adam McKenzie**, go to the taskbar to find the Webex App. Click on the icon to open it.

    ![Image](module_3g_media/media/image9.png)

2. Click on Adam’s avatar and on **Sign Out**.

    ![Image](module_3g_media/media/image10.png)

3. A new banner will appear on the Cisco Call App advising you about your phone services being disconnected.

    ![Image](module_3g_media/media/image11.png)

4. Click on **Sign in** to connect them again. If this banner is there because you are logged out from the Webex App, it will ask you to log in to the Webex App by bringing in the Webex App sign-in page.

5. Notice the status of the banner is now "Connecting." Sign in as **Adam McKenzie** to the Webex App and the UCM services.

    ![Image](module_3g_media/media/image12.png)

    ![Image](module_3g_media/media/image5.png)

6. Once you log in, the banner will show that services are reconnected.

    ![Image](module_3g_media/media/image13.png)

### Module 3g.10 (OPTIONAL): **Calling Scenarios 10 of 10** - Create a Hunt Group and Assign Users to It [Approx 10 min]

1. Continuing on Workstation 3, go back to the browser page where you are signed into Cisco Unified Communications Manager. Log back in as **administrator/dCloud123!** if the previous login has timed out.

2. Once logged in, go to **Call Routing** > **Route/Hunt** > **Line Group**. Click on **Add new**.

    ![Image](module_3g3-8_media/media/image31.png)

3. Name the Line Group as **dCloud Line Group**. Select extension **6016/Base_PT** (Adam McKenzie) and click **Add to Line Group**. Similarly, select extension **6020/Base_PT** (Monica Cheng) and click **Add to Line Group**. Click **Save**.

    ![Image](module_3g3-8_media/media/image32.png)

4. Now, let's add this Line Group to a **Hunt List**. Go to **Call Routing** > **Route/Hunt** > **Hunt List**. Click on **Add new**.

    ![Image](module_3g3-8_media/media/image33.png)

5. Assign the name **dCloud Hunt List**. Select **dCloud_CMGroup** under Cisco Unified Communications Manager Group. Checkmark **Enable this Hunt List**. Click **Save.**

    ![Image](module_3g3-8_media/media/image34.png)

6. Once the page reloads, click on **Add Line Group** on the newly created Hunt List page. Drop down the option **Line Group** and select the Line Group you just created (**dCloud Line Group**). Click on **Save.** Click **OK** on the prompt message that will appear.

    ![Image](module_3g3-8_media/media/image35.png)

7. Once the Line Group is added, click **Save** on the Hunt List Configuration. Click **OK**.

8. Now we are going to create the **Hunt Pilot**. Go to **Call Routing** > **Route/Hunt** > **Hunt Pilot**. Click on **Add new**.

    ![Image](module_3g3-8_media/media/image38.png)

9. Enter the directory number **7800** for the **Hunt Pilot**. Select the **Route Partition** as **Base_PT.** Drop down the option for **Hunt List** and choose the Hunt List we just created: **dCloud Hunt List.** Leave the rest of the fields as defaults. Click **Save.**

    ![Image](module_3g3-8_media/media/image39.png)

10. Now go to the **Webex Calling Dock** and notice that the Hunt Group is enabled. You can click on it, and it will be disabled (**Off**). Click **OK** on the pop-up window. Click on the icon again to log in (**On**) to the Hunt Group.

    ![Image](module_3g3-8_media/media/image40.png)

11. Go to your dCloud Session **Info** > **Phone Numbers**. Drop down the phone numbers and find the DID number associated with the extension **7800** (the one we assigned to the Hunt Group). This number will be different for each lab.

    ![Image](module_3g3-8_media/media/image42.png)

12. Dial the DID number from your personal phone or ask one of the proctors to make the call for you. Notice the incoming call for **Adam McKenzie** (Workstation 3). Do not answer the call on Workstation 3.

    ![Image](module_3g3-8_media/media/image43.png)

13. Wait a few tones and notice the call moving to **Monica Cheng** (Workstation 4). Hang up the call from your phone or the proctor's phone.

    ![Image](module_3g3-8_media/media/image44.png)

---


This completes the entire **Module 3: Cisco Call (UCM Calling) Integration with Microsoft Teams.**