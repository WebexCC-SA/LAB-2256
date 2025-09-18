# **Module 2: Cisco Call for Microsoft Teams (Webex Calling) \[Approx 1 hr 40 min\]**

With Cisco Call for Microsoft Teams, the Microsoft Teams users can access the enterprise-grade Webex Calling experience directly in the Microsoft Teams app. With a single click from the Microsoft Teams interface, you can access a complete suite of Webex Calling features. The features include directory search, PSTN dialing, speed dials, voicemail, call history, and artificial intelligence-powered background noise removal.

![A screenshot of a phone call AI-generated content may be incorrect.](module_2_media/media/image1.png)

This integrated app works with the Cisco Unified Communications Manager (UCM) call-control solution, Webex Calling for cloud deployment or the Dedicated Instance offering.

This would be the call flow diagram when using Webex Calling Multitenant as the call control:

![A screenshot of a webex cloud Description automatically generated](module_2_media/media/image2.png)

## Module 2a: Configure Single Sign-On (SSO) for Control Hub \[Approx 15 min\]

 > **NOTE:** *If you have completed module 3, you would have configured the SSO already as part of that module. So, you can skip this section and go to next section directly. If you have not run through module 2 yet, you can continue to configure SSO.*
 
**Microsoft tenant information for your lab:**

If you have your own identity provider (IdP) in your organization, you can integrate it with Control Hub for single sign-on (SSO). SSO lets your users use a single, common set of credentials for Webex App applications and other applications in your organization.

Cisco Webex supports a wide variety of IdPs for Single Sign-On configuration like Microsoft (both O365 and AD FS), Okta, PingFederate, Duo, etc.,

In this lab, we will explore the SSO configuration with **Microsoft O365**.

Integrating O365 with your Webex Control Hub you can also import/synchronize users and groups from Microsoft O365, Import Avatars (user profile pictures), define user attributes for mapping (like first name, email, etc.,) and configure SSO. In this lab, we will explore SSO configuration only.

1.  Open RDP connection to **Workstation 5** at 198.18.135, using one of the options mentioned in **Accessing your Lab** module. Use the credentials **dcloud\\kmelby** & **dCloud123!**

2.  Once connected to workstation, open the chrome browser from desktop and from home page go to **Cisco Webex Links** \> **Cisco Webex Control Hub** or you can directly go to <https://admin.webex.com> & log in with **cholland@cbXXX.dc-YY.com** and **dCloud*AAAA*!**

    > **NOTE:** *You need to Replace XXX, YY (in domain name) & AAAA (in password) with your session-specific details. If you haven't already done as explained in Accessing your lab section, go to Lab_info.txt file located on your **workstation 1** and copy the domain and password.*

    ![A screenshot of a computer Description automatically generated](module_2_media/media/image3.png)

    **NOTE**: *If you are asked for a PIN when signing to Control Hub or to the Webex App, you can get this pin by signing in to **Outlook Web Access** under **the Collaboration User Links** on your Chrome browser new tab.*

    ![A screenshot of a computer Description automatically generated](module_2_media/media/image4.jpeg)

    ![A screenshot of a computer Description automatically generated](module_2_media/media/image5.png)

    *Insert **dCloud\\cholland** as the username (for Charles Holland) and **dCloud123!** as your password.*

    ![A login screen with blue text and blue letters Description automatically generated](module_2_media/media/image6.png)

    *You will find the PIN requested in your Inbox:*

    ![A screenshot of a computer Description automatically generated](module_2_media/media/image7.png)

3.  For security reasons, Webex Control Hub signs out every 20 minutes (Idle timeout) by default. For this lab, let's make the idle time out longer so the Control Hub does not sign you out often during this lab. Go to **MANAGEMENT \> Organization Settings \> Control Hub's idle timeout.** Drop down the option for **Control Hub idle timeout** and select **12 hours** or **no timeout**. Click **Save**.

    ![A screenshot of a computer Description automatically generated](module_2_media/media/image8.png)

4.  Continuing on **Organization Settings** page, scroll down to the section **Microsoft Azure Active Directory Wizard App** and click **Set up.**

    ![A screenshot of a computer Description automatically generated](module_2_media/media/image9.png)

5.  It will take you to the Microsoft authentication page. Log in with the Microsoft credentials <cholland@cbXXX.dc-YY.com> & **dCloud123!** Click **Login**.

    > **NOTE:** *You need to replace XXX & YY in domain name with your session-specific details. If you haven\'t already done as explained in Accessing your lab section, go to Lab_info.txt file located on your workstation 1 and copy the domain and password**.***

6.  On the following page, Microsoft login page will show you the permissions required. Review the permissions. Check mark option for **Consent on behalf of your organization**. Click **Accept**.

    ![A screenshot of a phone Description automatically generated](module_2_media/media/image10.png)

7.  On the following page, you will be promoted for login again to Microsoft Org. Select the <cholland@cbXXX.dc-YY.com> from available logins, it should not prompt for password. Now, it will show you all details about permissions that are required for SSO configuration. **Click Accept**.

    ![A screenshot of a application Description automatically generated](module_2_media/media/image11.png)

8.  You will be taken back to Webex Control Hub and a pop-up window will be displayed. Keep the radio button selected for **Sync defaults** and click **Proceed**.

    ![Graphical user interface, text, application, email Description automatically generated](module_2_media/media/image12.png)

9.  It will create the instance/integration with Microsoft tenant. It will take around 2 to 3 minutes for the process to complete.

10. Once the integration process is completed, Job status will be displayed **NotRun**.

    ![A screenshot of a phone Description automatically generated](module_2_media/media/image13.png)

11. Within few min the Job status would change to **Active.** Wait until the job status is changed to **Active**. You may need to refresh the page, after 2 to 3 minutes, to see the updated status. At this point all users from your Microsoft tenant should be imported to Webex under **MANAGEMENT** \> **Users**. Notice few users with status **Verified** indicating they are imported from a trusted source (in this case the Microsoft tenant that we are integrating with).

12. Now go back to **MANAGEMENT** \> **Organization Settings** and scroll down to the **Microsoft Azure Active Directory Wizard App** section. Click the three dots on the right side and select **Edit Configuration**.

    ![A screenshot of a computer Description automatically generated](module_2_media/media/image14.png)

13. It will bring up the Microsoft Azure AD integration page, under **Attributes** tab drop down the field **phoneNumbers\[type eq "work"\].value** & choose **telephoneNumber** from the drop down list.

    ![A screenshot of a computer AI-generated content may be incorrect.](module_2_media/media/image15.png)

14. Now, go to **More** tab and select the checkbox option for **Activate single sign-on** and click **Save**.

    ![A screenshot of a computer AI-generated content may be incorrect.](module_2_media/media/image16.png)

15. You have now successfully enabled single sign-on for your Webex tenant. From now on, all logins to this Webex tenant will be redirected to Microsoft for authentication & you will use <cholland@cbXXX.dc-YY.com> & dCloud123! for logging into Webex Control Hub.

16. This completes the SSO configuration!.

## Module 2b: Ordering PSTN Numbers for users \[Approx 10 min\]

For Webex Calling, the DID numbers and call control is controlled by Webex Cloud. We need to order 5 new DID numbers for calling scenarios in this module.

1.  Continuing on workstation 5, go back to the browser where you logged into **Cisco Webex Control Hub**. or go to [https://admin.webex.com](https://admin.webex.com) & Login as cholland@cbXXX.dc-YY.com & dCloud123!, if the previous login is timed out.


2.  Go to **SERVICES** \> **Calling**. Click **+ Add Numbers**.

    ![A screenshot of a call center Description  automatically generated](module_2_media/media/image17.png)

3.  On the **Add Numbers** page, drop down the option for Location and choose **dCloud.** Since we are setting up this location for the first time, first we need to select the PSTN Connection for this location. Click **Edit** **PSTN**.

    ![A screenshot of a computer AI-generated content may be incorrect.](module_2_media/media/image18.png)

4.  You will be taken to **Edit PSTN connection for dCloud** (Location) and under the connection type choose **Cisco Calling Plans** and click **Next**.

    > **NOTE:** *If you do not see the option Cisco Calling Plans, close the page and repeat steps 2 through*

    ![A screenshot of a computer AI-generated content may be incorrect.](module_2_media/media/image19.png)

    > **NOTE:** *If its taking long on the page to load after selecting Cisco Calling Plan, close the page (top right corner x mark) & go to MANAGEMENT > Locations.  Select dCloud on the locations page and go to Calling tab.  On the Calling tab drop down Manage option for PSTN connection and enter Emergency Contact information and service address one by one manually (using the same information from steps 5 through 8).  Then go to SERVICES > Calling & click Add numbers  then continue from step 10*

    ![A screenshot of a call center Description  automatically generated](module_2_media/media/image17_note.png)


5.  Enter the following information & leave rest of the fields blank and click **Next**.

    | **Parameter**                       | **Value**                        |
    | ----------------------------------- | -------------------------------- |
    | First Name                          | Charles                          |
    | Last Name                           | Holland                          |
    | Email Address & Confirm Email Address | cholland@cbXXX.dc-YY.com         |

    **NOTE:** *You need replace domain with the domain assigned for your session (from Lab_info.txt file)*.

    ![A screenshot of a contact form Description automatically generated](module_2_media/media/image20.png)

6.  On the pop up window click **Yes, Change**.

7.  Under the **Emergency disclaimer**, read & scroll the disclaimer information all the way down. Enter Authorized Contact as **Charles Holland** and title as **Engineer** & Click **Agree and Continue**.

    ![A screenshot of a computer Description automatically generated](module_2_media/media/image21.png)

8.  Under **Emergency Services Address**, leave everything default for address and **Save**. Click **Apply** for suggested address. Click **Save**

    ![A screenshot of a computer AI-generated content may be incorrect.](module_2_media/media/image22.png)

9.  It will save all the information for PSTN connection we entered and take you summary page. On the following page, click **Add numbers.**

    ![A screenshot of a computer Description automatically generated](module_2_media/media/image23.png)

10. On the **Add Numbers** page, make sure location is selected as **dCloud** and the number type is selected as **PSTN number**. Keep the option **Order New Numbers** is selected and click **Next.**

    ![A screenshot of a computer Description automatically generated](module_2_media/media/image24.png)

11. On the **Specify numbers you want to order page**, drop down the option for **State/Province/Region** and choose any of the available states in United States (In this lab we support Cisco PSTN **ONLY** for **United States**).

12. Keep the search by option as **Area Code** and drop down the option for **Area Code** & choose any of area code of your choice. For **How may numbers do you want auto-selected for you?** Enter **5** and click **Search.**

    ![A screenshot of a computer Description automatically generated](module_2_media/media/image25.png)

13. On the next page, it will show you list of available number in that area code that you specified above. It will auto select five numbers. If you like any specific number from list that is not auto selected, you can unselect one of the auto selected number and select that number you like. For now, just keep the auto selected numbers as is and click **Order**.

    ![A screenshot of a computer Description automatically generated](module_2_media/media/image26.png)

14. Order will be submitted for these numbers. On the following page, click **View orders**. The status will read **Pending** then change to **Provisioned** in few seconds. You may need to refresh the page to see the correct/accurate state or select the order to view the slide out window.

15. Click on the order you placed (Order ID) \> Phone Numbers to verify all phone numbers are provisioned.

    ![A screenshot of a computer Description automatically generated](module_2_media/media/image27.png)

    Webex will not let incoming or outgoing PSTN calls until a **Main phone number** is assigned to the location. So first we need to assign one of these number to the location.

16. On **Webex Control Hub page** Navigate to **MANAGEMENT** \> **Locations**.

17. On the locations page select the existing location **dCloud**

18. On the **dCloud** location page, go to **Calling** tab

19. Observe, under Main number drop down option, there is a warning saying **You will not be able to make or receive calls until this number is added**.

20. Drop down the Main number option and choose one of the numbers we ordered above and click **Save**.

    ![A screenshot of a computer Description automatically generated](module_2_media/media/image28.png)

21. Observe that as soon as main number is assigned to location, the warning will be gone. Indicating now you will be able to make and receive calls from this location.


## Module 2c: Assign Webex Calling licenses and configure users for Microsoft Presence Sync [Approx 10 min]

In this section of the lab, we will use **Kellie Melby** and **Taylor Bard** users. Let's enable presence (with Microsoft) and assign Calling Licenses for both users on **Webex Control Hub**.

1. Continuing on **Workstation 5**, go to the browser tab where you had the **Webex Control Hub** open.

2. We can enable **Presence Sync** for the whole organization. It is not possible to enable it for individual users only, although this can later be managed through delegated Microsoft Graph API permissions.

3. On the Control Hub, go to **SERVICES** > **Calling**. On the Calling page, go to the **Client Settings** tab.

4. Scroll down on the **Client Settings** page to the Microsoft Teams Integration section and toggle the radio button **Presence Sync** & **Hide Webex windows**. If the option **Optimize Webex app for Microsoft Teams experience** is toggled **ON**, untoggle it for now. We will explore this option later.

    > **NOTE:** *If you have completed module 3, you may have already completed enabling Presence Sync & Hide Webex Windows. You can skip steps 3 and 4 above.*

    ![Image](module_2c_media/media/image1.png)

5. Now, let's assign a Webex Calling license for users. On the left-side pane, go to **MANAGEMENT** > **Users** and choose **Kellie Melby** from the list.

6. Scroll down on the summary page and click **Edit Licenses**.

    ![Image](module_2c_media/media/image2.png)

7. On the **Edit services for <kmelby@cbXXX.dc-YY.com>** page, click **Edit Licenses** again.

8. On the next page, go to the **Calling** tab. Checkmark both options for **Webex Calling** & **Professional**. Also, **uncheck** options for **Messaging** and **Meeting** to deploy phone-only services for this user. Click **Save**.

    ![Image](module_2c_media/media/image3.png)

9. On the next page, drop down the option for **Location** and choose **dCloud**, then drop down the option for **Phone Number** and choose one of the available numbers (that we ordered in the above section). Make sure you select a number other than the one you assigned to the location **Main Number**. Click **Save**. Click **Close**.

    ![Image](module_2c_media/media/image4.png)

    > **NOTE:** *Take note of the phone number being assigned to Kellie and Taylor. We will add these numbers to the contact information of users on Microsoft in the following steps.*


10. Go back to **MANAGEMENT** > **Users** again and, on the users page, choose `<tbard@cbXXX.dc-YY.com>` and repeat steps 6 through 9.

    > **NOTE:** *Once both users are assigned licenses and phone numbers, let's add these newly assigned phone numbers to user contacts on Microsoft. Users can use the click-to-dial feature in Microsoft Teams.*

11. Continuing on **Workstation 5**, open a new browser tab and, from the home page, go to **Collaboration Admin Links** > **Microsoft Admin Center**, or directly open the Admin Center at <https://admin.microsoft.com>. Log in with credentials `<cholland@cbXXX.dc-YY.com>` and **dCloud123!**.

12. Once logged in, go to **Users** > **Active Users** on the left-side pane.

13. On the Active Users page, select **Kellie Melby**. It will bring up a fly-out window for the user configuration. On the fly-out window, scroll a little down and click **Manage contact information**.

14. On the **Manage contact information** page, scroll down and find **Office phone**. Enter the same phone number you assigned to **Kellie** on Webex. Enter the phone number in E.164 format, for example: `+19725556038`. Click **Save changes**. Click **Close** to close the fly-out window.

    ![Image](module_2c_media/media/image5.png)

15. Similarly (steps 11 to 14), assign the number to **Taylor Bard** (use the same phone number you assigned to Taylor on Webex, and remember to enter the phone number in E.164 format, for example: `+19725556023`).

    > **NOTE:** *Sometimes Microsoft takes a long time to update contact information, and you may not be able to find it on Microsoft Teams immediately. This is not a limitation of the lab or Webex; it's just Microsoft Cloud taking longer to update contact information.*
   

## Module 2d: Publish the Cisco Calling app on Microsoft tenant and disable Native Teams Caling [Approx 10 min]

Now let's publish and authorize the **Cisco Calling app** for the whole Microsoft Organization so that each user is not prompted for authorization. Additionally, we will disable the Microsoft Native Calling option so users will not get confused between Microsoft Native Calling and Webex Calling.

   > **NOTE:** *If you have completed module 3, you may have already published the **Cisco Call** app. If so, you can skip the rest of the steps (16 through 23) and go to the next module.*


1. First, we are going to hide the Teams-to-Teams Calling button. Continuing in the **Microsoft Admin Center**, on the left-side page, click **Show all** to see all admin centers. Under **Admin Centers**, select **Teams**.

    ![Image](module_2c_media/media/image6.png)

2. It will open the **Microsoft Teams Admin Center** in a new tab. Once the Teams Admin Center is opened, go to **Voice** > **Calling policies**. On the Calling Policies page, select the radio button for **Disallow Calling** and click on **Manage Users/Assign users**.

    ![Image](module_2c_media/media/image7.png)

3. It will bring up fly-window to assign users. Search and add the users **Kellie Melby** and **Taylor Bard**, and click on **Apply**. Click on **Confirm** in the pop-up window.

    ![Image](module_2c_media/media/image8.png)
    ![Image](module_2c_media/media/image9.png)

4. Now, let's publish the **Cisco Call** app for the organization so that each user does not need to request admin authorization. Continuing in the **Teams Admin Center**, on the left-side page, go to **Teams apps** > **Manage apps**.

    > **NOTE:** *If you have already completed module 2, you may have already completed publishing and granting permissions for Cisco Call.*

5. On the Manage Apps page, search for **Cisco Call** on the right. Select the **Cisco Call** app that is listed.

    ![Image](module_2c_media/media/image10.png)

6. On the **Cisco Call** app page, go to the **Permissions** tab. Under the Permissions tab, click **Grant admin consent**. It will bring up a pop-up window to authorize as an admin. Log in as `<cholland@cbXXX.dc-YY.com>` and **dCloud123!**. It will prompt you to accept some permissions. Click **Accept**.

    ![Image](module_2c_media/media/image11.png)
    ![Image](module_2c_media/media/image12.png)

    > **NOTE:** *Some permissions are considered delegated level, while others are application level. Below is a description of the permissions used by Cisco Call for Microsoft Teams, and what changes are coming in June 2025.*

    ![Image](module_2c_media/media/image13.png)
    ![Image](module_2c_media/media/image14.png)


7. At this point, any user in the organization can go to Apps on **Microsoft Teams** and add the **Cisco Call** app from the store.

    > **NOTE:** *As an Organization Admin, you can also install/publish this app for all users. To publish the app for all users, go to **Teams apps** > **Setup policies** and update **Global (Org-wide default)** to include the **Cisco Call** app.*

    ![Image](module_2c_media/media/image15.png)

8. Now Microsoft and Webex tenants & users are ready for use.


## Module 2e: Testing scenarios for Microsoft Integration with Webex (Webex Calling) [Approx 75 min]

In this module, we will make some test calls to internal, PSTN, configure multiple features, watchlist, and Call Queues. This module consists of a total of 11 testing scenarios described below.

#### Logging into Clients [Approx 10 min]

1. Continuing on **Workstation 5**, open Microsoft Teams from Desktop and log in as `<kmelby@cbXXX.dc-YY.com>` with password **dCloud123!**. Click **OK**. Click **Done**.

    > **NOTE:** *DO **NOT** click **No, this app only**.*

    ![Image](module_2e_media/media/image1.png)

2. **Accept** any information/warning messages while logging in. If you have added Cisco Call as an admin in Module 2c, jump to step 3. If not, once logged in, click the eclipse icon (three dots) on the left side pane. On the new fly-out window, search for **Cisco Call**. It will list the Cisco Call app. Click **Add**. It will add **Cisco Call app** to Microsoft Teams and take you to the login screen.

    ![Image](module_2e_media/media/image2.png)

3. On the Cisco Call App, click **Continue**.

    ![Image](module_2e_media/media/image3.png)

4. This will use the same email address used to log in to Microsoft Teams. As we have an active session, you will be signed into **Cisco Call** on Microsoft Teams.

5. At this point, the Webex App will pop up for you to log in. Log in as `<kmelby@cbXXX.dc-YY.com>` with password **dCloud123!**.

    ![Image](module_2e_media/media/image4.png)

6. As we chose to hide the Webex windows, once the user logs in, the Webex App window will disappear. You will be prompted with a notification about Emergency Calling. Click **OK**.

    ![Image](module_2e_media/media/image5.png)

7. You might get a pop-up window guiding you through the new features of the Cisco Call app. Click on **Next**. Then, click on **Later** when it asks you to use the Calling Dock, as we will explore this feature later.

    ![Image](module_2e_media/media/image6.png)

8. Finally, right-click on the **Cisco Call app** on the left side pane and click **Pin**. This ensures it is always visible for easier access. If you have published the **Cisco Call app** for the entire organization under setup policies on the **Microsoft Teams Admin Center**, you will see the **Cisco Call app** pinned already.

    ![Image](module_2e_media/media/image7.png)

    > **NOTE:** *If you do not see the **Cisco Call** app on the left side, click on the three dots on the left side pane again, right-click on the **Cisco Call app**, and select **Pin** so the application always displays on the left side pane for easier access.*

9. Now both of your clients on **Workstation 5** are ready for use.

10. Open an RDP connection to **Workstation 6** using one of the methods described in the **Accessing Your Lab** module above. Repeat the steps above (1 through 9) on Workstation 6 using the credentials `<tbard@cbXXX.dc-YY.com>` and **dCloud123!**.


---

> **NOTE:** *Make sure you are logged in to both clients on both Workstations 5 and 6 before continuing.*

### Module 2e.1: **Calling Scenarios 1 of 11** - Making an Internal Call [Approx 5 min]


1. Continuing on **Workstation 5** as **Kellie Melby**, go to the **Cisco Call** app on Microsoft Teams (on the left-side pane) and search for **Taylor Bard** (right above the dial pad).

2. It will search the directory for **Taylor Bard** and display options to call. Click on either **Audio** or **Video**. It will display all available contact methods for Taylor, like **Phone number**, **Email**, etc. Click on any of the options to place the call.

    ![Image](module_2e_media/media/image14.png)

3. Answer the call on **Workstation 6** (as **Taylor Bard**). Verify that the call gets connected. Wait a few seconds and hang up the call. Also, verify the call status reflects as shown below.

    > **NOTE:** Click **OK** for the warning *No Microphone Found* message. *You will not be able to hear audio in either direction as we are using virtual workstations and the microphone is not available.*

    > **NOTE:** *If you do not see the correct status, try to bring Microsoft Teams into the foreground or initiate a chat conversation between **Kellie** and **Taylor**.*

    ![Image](module_2e_media/media/image15.png)

4. As soon as the call is hung up, verify that Kellie's availability status changes to **Available**.

    ![Image](module_2e_media/media/image16.png)

5. You will see the up-to-date call history synchronized/reflected in the **Cisco Call** app on Microsoft Teams. To verify the call history, go to **Cisco Call** app > **Recent Calls** as shown below.

    ![Image](module_2e_media/media/image17.png)

6. Similarly you can dial any PSTN number in E.164 format (+1AAABBBCCCC). Or you can dial the Cisco support number +**18005532447**. You can also make inbound calls to Kellie Melby DID number (you can find it in session details or in the file lab_info.txt) from your mobile. If you cannot dial US phone numbers from your mobile, reach out to one of your proctors.

    > **NOTE:** *You will only be able to call US numbers in this module, as the Webex location is created in the USA and ordering Cisco Calling Plan numbers is only available for the USA.*

---

### Module 2e.2: **Calling Scenarios 2 of 11** - Notification Badge and Cisco Call Bot [Approx 5 min]

For Cisco Call for Microsoft Teams, notifications are shown in two manners:

- **Notification Badge:** It shows a red **1** next to the Cisco Call app within Microsoft Teams when there's any notification (no matter the number of notifications; it's an indicator).
- **Cisco Call Bot:** It notifies the user about any missed calls and voicemail messages.

---

1. On **Workstation 6**, as **Taylor Bard**, make a call to **Kellie Melby** and hang up the call, so that Kellie receives a missed call notification.

    ![Image](module_2e_media/media/image18.png)

2. Go to **Workstation 5**, as **Kellie Melby**. Notice there's a notification badge next to the Cisco Call icon on the left-hand side. This means the user has received a missed call or a voicemail.

    ![Image](module_2e_media/media/image19.png)

3. Click on the **Chat** icon and go to **Cisco Call** chat. As soon as you open the chat with the bot, the notification badge disappears from the Cisco Call tab. Notice there's a new message regarding a missed call from **Taylor Bard**.

    ![Image](module_2e_media/media/image20.png)

---

### Module 2e.3: **Calling Scenarios 3 of 11** - Making Calls from Microsoft Teams Chat Window [Approx 5 min]

1. Continuing on **Workstation 5**, go to the **Microsoft Teams app** and go to **Chat** on the left-side page. On the top search window, search for **Taylor Bard**.

    ![Image](module_2e_media/media/image21.png)

2. Initiate a chat conversation with **Taylor Bard** and send a few messages back and forth.

3. Click on the **+** sign towards the right side of the typing window for chat and select **Cisco Call** from available options.

    ![Image](module_2e_media/media/image22.png)

4. It will bring up available calling options for **Taylor Bard**. Choose either **Phone number** or **Email Address** from the drop-down option. Then choose either **Audio** or **Video** option to make the call.

    ![Image](module_2e_media/media/image23.png)

5. Answer the call on **Workstation 6**, verify that the call is connected, and confirm that the presence status is updated to show that Taylor (and Kellie) is **In a call**. Hang up the call after a few seconds.

    ![Image](module_2e_media/media/image24.png)

---

### Module 2e.4 (NEW): **Calling Scenarios 4 of 11** - Optimize Webex App for Microsoft Teams Experience  [Approx 3 min]

 We are going to enable a feature on Control Hub that makes the Webex App optimized for being used with Microsoft Teams. This option enables:

* Webex branding removal
* Linking Calling Dock to MS Teams (shortcut to Call History, Voicemail, and Simplified Call Settings)
* Ability to mute Webex calls when on Teams meetings

---

1. Continuing on **Workstation 5**, go back to the browser tab where you logged into **Webex Control Hub**. On Control Hub, go to **MANAGEMENT** > **Users**, choose user **Kellie Melby.** On the user page, go to the **Calling** tab. On the calling tab, scroll down to **Call Settings** > **Microsoft Teams Integration**. On the Microsoft Teams integration page, toggle on for option **Optimize Webex App for Microsoft Teams Experience.** Click on **Save.**

    ![Image](module_2e_media/media/image25.png)

2. Restart the Webex App to apply the changes by clicking on **Exit** from the System tray (right-click + Exit).

    ![Image](module_2e_media/media/image52.png)

7. You will see a new banner on the Cisco Call App (we will explore it latter). Click on **Sign in** on the banner that shows the Cisco Call tab to re-open the Webex App.

    ![Image](module_2e_media/media/image53.png)

---

### Module 2e.5 (NEW): **Calling Scenarios 5 of 11** - Making a Call with the Optimized Experience [Approx 3 min]

1. Continuing on **Workstation 5** as **Kellie Melby**, go to the **Cisco Call** app on Microsoft Teams and make another call to **Taylor Bard**.

2. Notice the Webex logo is not shown within the in-call window anymore, as the option **Optimize Webex App for Microsoft Teams Experience** is enabled for this user.

    ![Image](module_2e_media/media/image26.png)

3. Hang up the call.

---

### Module 2e.6 (NEW): **Calling Scenarios 6 of 11** -- Presence Sync: Mute Webex App Calls When on Teams Meetings [Approx 10 min]

Presence sync is supported between Microsoft Teams and Webex for the following statuses:

![Image](module_2e_media/media/image27.png)

When on a **Microsoft Teams meeting or call**, users might want to decide if they want to receive or decline calls. The status when on a Teams Meeting or a call will show as **"In a call"** in Microsoft Teams, and as **"On a call"** in the Webex App.

However, this presence status itself doesn't mean incoming calls will be muted, but two settings are required for this to happen:

- **Organizational setting**: **Optimize Webex App for Microsoft Teams experience** must be enabled for the user, group, or organization.
- **User setting**: Under **Call Settings**, Call Notifications can be set to **Always mute** or to **Only mute notifications when I'm in a meeting or on a call**. These settings apply to either Webex calls or meetings, and also to Microsoft Calls and Meetings if the option **"Optimize Webex App for Microsoft Teams Experience"** is enabled for that user.

    ![Image](module_2e_media/media/image28.png)

#### Let's explore the option **Only mute notifications when I'm in a meeting or on a call.**

1. Continuing on **Workstation 5**, go to **Microsoft Teams**. Go to the **Meet** tab of left side pane and click on **Meet now**. Then click on **Start a meeting** to start a Microsoft Teams meeting.

    ![Image](module_2e_media/media/image29.png)

2. Select any audio option and click on **Join now**. Click close for option **Invite people to join you** pop-up window

    ![Image](module_2e_media/media/image30.png)

3. Leave the meeting open and go back to the **Cisco Call** tab within Microsoft Teams. Notice Kellie's status has changed to **"In a call."**

    ![Image](module_2e_media/media/image31.png)

4. Open **Call Settings** within the Cisco Call tab. It will bring up settings for the Webex App. Notice that Call Settings are now simplified in comparison to the default Call Settings from the Webex App (**Simplified Call Settings**).

    ![Image](module_2e_media/media/image13.png)
    
5.  On the settings, go to **Notifications**. Under Notifications, click on **Calls**. Ensure the option **Don't mute** is selected. Click **Save.**

    ![Image](module_2e_media/media/image32.png)

6. Now, navigate to **Workstation 6** and open Microsoft Teams (as Taylor Bard). From the Cisco Call tab, make a call to Kellie Melby's work number.

    ![Image](module_2e_media/media/image33.png)

7. On **Workstation 5**, notice Kellie Melby gets the call notification toast. Decline the call on Workstation 5 as Kellie Melby and/or hang up the call on Workstation 6 as Taylor Bard.

    ![Image](module_2e_media/media/image34.png)

8. Now, on **Workstation 5**, open **Call Settings** within the Cisco Call tab. It will bring up settings for Webex App. Go to **Notifications**. Under Notifications, click on **Calls**. Select the option **Only mute notifications when I'm in a meeting or on a call**. Click **Save.**

    ![Image](module_2e_media/media/image35.png)

9. Repeat the call from Taylor Bard to Kellie Melby: Navigate to **Workstation 6** and open Microsoft Teams (as Taylor Bard). From the Cisco Call tab, make a call to Kellie Melby's work number.

    ![Image](module_2e_media/media/image33.png)

10. Notice Taylor Bard can make the call, but Kellie Melby doesn't receive any notification toast while the call is happening. Hang up the call from **Workstation 6**, as Taylor Bard.

    ![Image](module_2e_media/media/image36.png)

11. Go back to **Workstation 5** and, still in the Cisco Call tab within Microsoft Teams, notice a **new missed call** from Taylor Bard under **Recent Calls**.

    ![Image](module_2e_media/media/image37.png)

12. Still on **Workstation 5**, open the Microsoft meeting window and end the Microsoft Teams meeting.

    ![Image](module_2e_media/media/image38.png)

13. Open **Call Settings** from the Cisco Call tab within Microsoft Teams and change the **Call Notifications** settings back to **Don't Mute**. Click **Save.**

    ![Image](module_2e_media/media/image39.png)


### Module 2e.7: **Calling Scenarios 7 of 11** - Calling Dock [Approx 5 min]

The Webex Calling Dock (formerly multi-call window) is a user-enabled setting to maximize calls for multiple lines and manage calls effectively. It can act as a companion app for Microsoft Teams. It also helps to hide the Webex app during calls.

1. Continuing on **Workstation 5**, on Microsoft Teams go to the **Cisco Call** app on the left-side pane. Click on the ellipsis menu on the right-hand side (next to Call Settings) and toggle on the **Calling Dock** to enable it.

    ![Image](module_2e_media/media/image41.png)

2. Notice that Webex will bring a small call window (called Calling Dock). You can use this **Calling Dock** for any calling functions like making calls, answering calls, recent calls, using the dial pad, and accessing voicemail.

3. Drag and drop the Calling Dock to the right side of the screen to notice it minimizes itself (docking feature).

    ![Image](module_2e_media/media/image42.png)

4. Hover your mouse over the new dock icon on the right to see the **Calling Dock** without keeping it open. Click on the dock to maximize the **Calling Dock** again.

    ![Image](module_2e_media/media/image43.png)

---

### Module 2e.8: **Calling Scenarios 8 of 11** - Multi-Line [Approx 5 min]

You can set up a profile with multiple lines with different phone numbers for calling. You can switch lines if you need to make outgoing calls from different lines, such as a front desk line, support team line, or an individual line with a different caller ID.

1. Continuing on **Workstation 5**, go back to the browser tab where you logged into **Webex Control Hub**, go to **SERVICES** > **Calling**, and on the Calling page go to **Virtual Lines**. Click **Create**.

    ![Image](module_2e_media/media/image47.png)

2. On the **Add Virtual Line** page, populate the following and click **Add**:

    - **First Name:** Kellie
    - **Last Name:** Melby
    - **Display Name:** Kellie Melby -- Personal
    - **Location:** Select **dCloud**
    - **Phone Number:** Choose a number other than the one assigned to the **Main Number** and users **Kellie** and **Taylor**.

    ![Image](module_2e_media/media/image48.png)

3. It will add the Virtual Line and take you to the next page with a couple of options. On the next page, choose **Assign**.

    ![Image](module_2e_media/media/image49.png)

4. On the **Assign Device** dropdown menu, select **Kellie Melby. Webex App. dCloud. +1XXXXX**, as shown below. Click **Assign**.

    ![Image](module_2e_media/media/image50.png)

5. On the next page, for **Line Label**, give a name like **Personal Line** or something descriptive of your choice. Click **Save**.

    ![Image](module_2e_media/media/image51.png)

6. Now Webex will have two lines configured. To make them appear in the Calling Dock, restart the Webex App by clicking on **Exit** from the System tray (right-click + Exit).

    ![Image](module_2e_media/media/image52.png)

7. Then, click on **Sign in** on the banner that shows the Cisco Call tab to re-open the Webex App.

    ![Image](module_2e_media/media/image53.png)

8. The Calling Dock will open again, showing both lines now: **Kellie Melby** and **Personal Line**.

    ![Image](module_2e_media/media/image54.png)

9. Click on **Kellie Melby** name (top-left corner) on the Calling Dock to switch from the line **Kellie Melby** to the **Personal Line** (the line that you added above) to make outbound calls.

    ![Image](module_2e_media/media/image55.png)

10. Now, search for **Taylor Bard** on the Calling Dock and click on the call button. Answer the call on Workstation 6. Verify that the call gets connected.

    ![Image](module_2e_media/media/image56.png)

11. Also, on Workstation 5, observe that the call is made from Line 2 (**Personal Line**) of **Kellie Melby**.

    ![Image](module_2e_media/media/image57.png)

    > **NOTE:** *Call Presence status is currently not supported on secondary lines for Webex Calling Multitenant.*

12. Hang up the call after a few seconds. On Workstation 5, now make the call from the Cisco Call tab within Microsoft Teams. You can make the call from the **Recent Calls** tab. Notice the call goes through the secondary line as well.

    ![Image](module_2e_media/media/image58.png)
    ![Image](module_2e_media/media/image59.png)

13. Hang up the call after few seconds. Now, switch back to the **primary line** on the Calling Dock (**Kellie Melby**) by clicking on the current line (Personal Line) on the top-left corner of the Calling Dock. It will display both lines for Kellie. Click on the line named **Kellie Melby**.

    ![Image](module_2e_media/media/image60.png)

    > **NOTE:** *Make sure you switch to the primary line before continuing to the next module.*

### Module 2e.9: **Calling Scenarios 9 of 11** (NEW) - Phone Disconnection Banner [Approx 3 min]

When phone services are disconnected (for example, when the Webex App is logged out), there will be a banner showing that in the Cisco Call App. It also appears when it detects the Webex App is not running (when you exit from it), as we have seen before. Let's test the experience when signing out from the Webex App.

1. Continuing on **Workstation 5** as **Kellie Melby**, go to the taskbar to find the Webex App. Click on the icon to open it.

    ![Image](module_2e_media/media/image8.png)

2. Click on Kellie's avatar and on **Sign Out**.

    ![Image](module_2e_media/media/image9.png)

3. On Cisco Call app page in Microsoft Teams, a new banner will appear on the Cisco Call App advising you about your phone services being disconnected.

    ![Image](module_2e_media/media/image10.png)

4. Click on **Sign in** on the banner to connect them again. If this banner is there because you are logged out from the Webex App, it will ask you to log in to the Webex App by bringing in the Webex App sign-in page.

5. Notice the status of the banner is now "Connecting". Sign in as <kmelby@cbXXX.dc-YY.com> (Password: dCloud123!).

    ![Image](module_2e_media/media/image11.png)

6. Once you log in, the banner will show that services are now connected.

    ![Image](module_2e_media/media/image12.png)

---

### Module 2e.10 (OPTIONAL): **Calling Scenarios 10 of 11** - Create a Call Queue & Assign Users/Agents to Call Queue [Approx 10 min]

We can create a call queue and assign users (agents) to it. Those users will have visibility of the Call Queues they have been assigned to on the Calling Dock. They can sign in/out of the queue and set their status.

1. Continuing on **Workstation 5**, go back to the browser tab where you logged into **Webex Control Hub**. On the Control Hub, go to **SERVICES** > **Calling**, and click on the tab **Features**. Then, click on **Add new** on the tab **Call Queue**.

    > **NOTE:** *You can close the information pop-up window about Webex Calling Features.*

    ![Image](module_2e_media/media/image61.png)

2. It will take you to **Add Call Queue** page. Assign the location **dCloud** and name the call queue as **dCloud Call Queue**.

3. Drop down the option for **Phone Number** and choose one of the available PSTN numbers. Make sure to select the number other than the number assigned to **Main Number**. You can add the last 4 digits of the DID number for the extension field or choose to ignore that field.

    ![Image](module_2e_media/media/image62.png)

    > **NOTE:** *Make a note of the phone number assigned to the Queue here, as we will need this number to dial later.*

4. Scroll down a little, and for the **Caller ID**, select **Direct Line** under **External caller ID phone number**. Click **Next**.

    ![Image](module_2e_media/media/image63.png)

5. Keep the defaults and click **Next** for the three subsequent steps:

    - **Call Routing Type:** Circular
    - **Overflow Settings:** Perform busy treatment
    - **Announcements:** Welcome Message (checked) and Comfort Message (checked)

6. On the **Select Users to Add to the Call Queue** screen, drop down the option **Add user, workspace, or virtual line** and select **Kellie Melby** (with primary line) and **Taylor Bard**. Check the option **Allow agents to join or unjoin the queue.** Click on **Next**.

    ![Image](module_2e_media/media/image64.png)

7. Review the selected options and click **Create.** Click on **Done** on the next screen.

    ![Image](module_2e_media/media/image65.png)

8. You will be taken back to **Calling** > **Features** > **Call Queue**, where you will see the newly created Call Queue.

    ![Image](module_2e_media/media/image66.png)

9. Now go to the Webex Calling Dock for **Kellie Melby** (Workstation 5). You will find there a new icon with the status **Available.**

    ![Image](module_2e_media/media/image67.png)

    > **NOTE:** *If you do not see Queue Available status, exit Webex from the system tray (right-click/exit) and sign in to Phone Services on the banner from the Cisco Call tab within Microsoft Teams, as you previously did when enabling the Virtual line.*

10. Click on the Queues icon to explore the available options.

    ![Image](module_2e_media/media/image68.png)

11. Dial the DID number that is assigned to the **Call Queue**. Make the call from your personal phone or ask one of the proctors to make the call for you. Notice the **incoming** call for one of the users (**Kellie Melby** or **Taylor Bard**). Decline the call for the user that is receiving it (in this example, **Kellie** on Workstation 5).

    ![Image](module_2e_media/media/image69.png)

12. Switch to the other workstation (different from where you received the call) and notice the incoming call for the other user (in this example, the call came first to **Kellie** and later to **Taylor**, when **Kellie** declined the call).

    ![Image](module_2e_media/media/image70.png)

13. Either answer the call on Workstation 6 (as **Taylor**) or decline it. If you choose to decline the call again, it will go back to **Kellie Melby**, as the **Queue Behavior** is configured as **Circular**. Hang up the call from where you made the call from.

---

### Module 2e.11 (OPTIONAL): **Calling Scenarios 11 of 11** - Enable Watchlist [Approx 10 min]

**Watchlist**

Users can have a list of monitored users (**Busy Lamp Field** - BLF). They will see the presence status of the monitored users and can pick up their calls from the Calling Dock.

In the Watchlist, you will see a list of people in your BLF list and can monitor their availability. If someone in your list has an incoming call, you have the option to pick up the call on their behalf. You can check if someone is available before transferring a call to them.

1. Continuing on **Workstation 5**, go back to the browser tab where you logged into **Webex Control Hub**. On the Control Hub, go to **MANAGEMENT** > **Users**, and choose the user **Kellie Melby.** On the user page, go to the **Calling** tab. On the calling tab, scroll down to **Between-user permissions** > **Monitoring**.

    ![Image](module_2e_media/media/image71.png)

2. Drop down the option **Add Monitored Line** and choose **Taylor Bard** from the available list.

3. You will now see **Taylor Bard** as part of the Monitoring List for **Kellie Melby**. Click on **Save.**

    ![Image](module_2e_media/media/image72.png)

4. On **Workstation 5**, open **Call Settings** from the Cisco Call app within Microsoft Teams or from the **Webex Calling Dock** (the wheel icon).

    ![Image](module_2e_media/media/image73.png)

5. Drop down the **Notifications** option and go to **Calls**. Under **Call Pickup**, look for **Watchlist** and uncheck the option **Turn off notifications**. This will allow you to do Call Pickup from your monitored users. Click on **Save**.

    ![Image](module_2e_media/media/image74.png)

6. Go back to the **Calling Dock** for **Kellie Melby** and notice that **Taylor Bard** is now part of the **Watchlist.**

    > **NOTE:** *If you do not see the **Watchlist**, exit Webex and sign in to Phone Services again to relaunch the **Webex** App.*

    ![Image](module_2e_media/media/image75.png)

7. Make a phone call to **Taylor Bard's phone number** (check the phone number on the Cisco Call app within Microsoft Teams on **Workstation 6** or on Control Hub). You can make the call from your personal phone or ask one of the proctors to make the call for you. **Don't answer this call as Taylor (Workstation 6).**

8. Switch to **Workstation 5**. Wait a few seconds and notice the **Call Pick-up** notification coming to **Kellie Melby.**

    ![Image](module_2e_media/media/image76.png)

9. Click on **Pick-up** to pick up the incoming call. Notice the call has been established with **Kellie Melby.**

    ![Image](module_2e_media/media/image77.png)

19. Hang up the call

---

This completes the entire **Module 2: Cisco Calling Integration for Microsoft Teams (Webex Calling)**.