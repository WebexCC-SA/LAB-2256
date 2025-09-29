# Module 1: Direct Routing with CUBE and Interworking with CUCM via CUBE
## **Module 1a: Direct Routing with CUBE** \[Approx 45 min\]

Microsoft Direct Routing is a Microsoft solution that lets you connect a
certified, customer-provided Session Border Controller (SBC) to
Microsoft Teams Phone for on-premises or customer-provided PSTN
connectivity.

![A diagram of a phone system Description automatically generated](module_1a_media/media/image1.png)

### Direct Routing CUBE Configuration \[Approx 10 min\]

In this module there are 6 sub modules, out of which 4 sub-modules are CLI (Command Line Interface) based.  These 4 sub-modules entail importing required certificates for CUBE connectivity with the Microsoft Teams Phone, configure SIP profiles, dial-peers, and other required CLI configurations.  The entire required configuration for CUBE has been generated and put it on **Workstation 1 Desktop** in a file called **Ready-CL_DR_CUBE-Config.txt** file. Configure the CUBE by copying and pasting commands from the file.

> **NOTE:** If you are interested in understanding all these commands/certificates/SIP Profiles etc., we have all this information listed in [Appendix section](/665b511720/appendix/appendix/) for your review after the lab.

1.  Continuing on Workstation 1, Minimize all applications and open text
    file **Ready-CL_DR-CUBE-Config.txt** with **Notepad++**. Right click
    on the file and choose **Edit with Notepad++**.

    > **NOTE**: ***DO NOT*** open this file with Microsoft default notepad
application, the certificates will not be formatted correctly.

    ![A screenshot of a computer Description automatically
generated](module_1a_media/media/image2.png)

2.  Open **Putty** from the taskbar and open an SSH connection to
    **198.18.133.231** (or you can load **cube.dcloud.cisco.com** from
    available saved logins on Putty) and login as **admin** and
    **dCloud123!**

3.  Copy all (use **Ctrl + a**) the contents of the file
    (**Ready-CL_DR-CUBE-Config.txt**). Go to the putty window and paste
    (**Right click** anywhere on the putty window).

4.  Once all the configuration is entered on Putty, scroll up and make
    sure there are **NO** error messages for any of the commands and
    also make sure the certificate **import is successful** as show
    below.

    ![A screenshot of a computer screen Description automatically
generated](module_1a_media/media/image3.png)

5.  The CUBE configuration from CLI is complete and we will move to Microsoft Admin Center to continue to configure Direct Routing configuration.


### Module 1a.1: Add CUBE to the Microsoft Teams and configure Voice policies \[Approx 25 min\]

> **NOTE**: *In the Microsoft admin center, we will add CUBE as a Session
Border Controller (SBC)*

1.  Continuing on Workstation 1, open a new browser tab, go to **Collab
    Admin links,** and choose **Microsoft Teams Admin Center**. Login
    with <cholland@cbXXX.dc-YY.com> and **dCloud123!**, if prompted.

    > **NOTE:** *You need to Replace XXX, YY (in domain name) with your session-specific details. If you haven't already done as explained in Accessing your lab section, go to Lab_info.txt file located on your **workstation 1** and copy the domain and password.*    

2.  Once logged into the **Microsoft Teams admin center,** on the left
    side pane, go to **Voice** \> **Direct Routing**. On the Direct
    Routing page click **Add** to add a new SBC (CUBE).

3. On the **Add SBC** page, name the SBC as **cube.cbXXX.dc-YY.com** (the FQDN of the CUBE), and toggle ON the option for **Enabled,** and set SIP signaling port to 5061. Scroll down and click **Save**.

    > **NOTE:** *You need to Replace XXX, YY (in domain name) with your session-specific details. If you haven't already done as explained in Accessing your lab section, go to Lab_info.txt file located on your **workstation 1** and copy the domain and password.*

    ![A screenshot of a computer Description automatically
generated](module_1a_media/media/image21.png)

4.  You will be taken to the SBCs page and there you will see the newly
    added SBC.

    ![A screenshot of a phone Description automatically
generated](module_1a_media/media/image22.png)

    > **NOTE**: *Sometimes CUBE may take longer to show as Active. Also TLS connectivity status may show an exclamation mark (indicating a warning) due to inactivity but you can ignore that.*

    At this point, CUBE should be able to talk to Microsoft Cloud services
and establish a TLS connection. You can test that using the below
commands on the CUBE to check active connections.

    **`show sip-ua connections tcp tls brief`**

    ![A screenshot of a computer Description automatically
generated](module_1a_media/media/image23.png)

    **`show sip-ua connections tcp tls detail`**

    ![A screenshot of a computer program Description automatically
generated](module_1a_media/media/image24.png)

    > **NOTE**: *The **52.114.X.X** subnet belongs to Microsoft Cloud indicating CUBE has successfully established communication with Microsoft Cloud/tenant.*

5.  Now go to **Voice** \> **Voice routing policies**. There will be a
    default routing policy named **Global (Org-wide default)**. Select
    the **Global** voice routing policy, and under **PSTN usage
    records** click **Add PSTN usage records.** It will bring up a
    fly-out window to add PSTN usage records. Click **Add** on the
    fly-out window and name it **PSTNUR**, checkmark the PSTN usage
    record you just created and click **Save and Apply.** The fly-out
    window will be closed and you will be taken back to the **Global**
    policy page, click **Save** and click **Confirm** on the pop-up
    window to update the Global policy with the newly created PSTN usage
    record (PSTNUR).

    ![A screenshot of a computer Description automatically
generated](module_1a_media/media/image25.png)

6.  Now let's add a voice route. Go to **Voice** \> **Direct Routing**.
    On the Direct routing page go to the **Voice routes** tab and click
    **Add** to add a new voice route.

    ![A screenshot of a computer Description automatically
generated](module_1a_media/media/image26.png)

7.  On the Add voice route page, populate the following parameters and
    click **Save**.

    | **Parameter**      | **Value**                                                                                                                                   |
    |--------------------|---------------------------------------------------------------------------------------------------------------------------------------------|
    | **Name**           | PSTN-DR                                                                                                                                     |
    | **Priority**       | 2                                                                                                                                           |
    | **Dialed number pattern**             | \\+.*                                                                                                                                     |
    | **SBCs enrolled**  | Click **Add SBCs** and on the fly-out window, drop down and select the available SBC (`cbXXX.dc-YY.com`) and click **Apply**.                          |
    | **PSTN usage records** | Click **Add PSTN usage records** and on the fly-out window, checkmark the available PSTN usage record (`PSTNUR`) and click **Apply**. |

    ![A screenshot of a computer Description automatically
generated](module_1a_media/media/image27.png)

8.  Now, let's add the Calling policy. Go to **Voice** \> **Calling
    policies.** Click **Add** to add a new Calling policy.

    ![A screenshot of a computer Description automatically
generated](module_1a_media/media/image28.png)

9.  Name the Calling policy as **PSTN-CP.** Toggle **On** for **Make private calls**. Scroll down on the page and
    select **On** for the option **Busy on busy during calls** option.
    Click **Save**.

    ![A screenshot of a computer Description automatically
generated](module_1a_media/media/image29.png)

10. Now we need to assign the phone number and apply the policies (we
    defined above) for the user that we are going to use in this section
    of the lab (**Charles Holland**). On the Microsoft Teams admin
    center go to **Users** \> **Manage users.**

11. From the list of users select **Charles Holland**
    (<cholland@cbXXX.dc-YY.com>). It will take you to the user page. On
    the user page click **Assign primary phone number** under
    **Account**.

12. It will bring up a fly-out window for **Assign phone number**. For
    **Phone number type** keep **Direct Routing** selected. Enter
    **6018** for the **Assigned phone number**. Click **Apply**.

    ![A screenshot of a computer Description automatically
generated](module_1a_media/media/image30.png)

    > **NOTE**: *Sometimes it will take longer to update the phone number and it may give you a warning. You can safely ignore the warning and just wait until the pop-up window goes away. It will take around 5 to 10 seconds for the pop-up window to go away.*

13. It will take you back to the user page. Now go to **Policies** tab
    and click **Edit** under the Policies tab.

    ![A screenshot of a computer Description automatically
generated](module_1a_media/media/image31.png)

14. It will bring up a fly-out window to configure user policies.

    Drop-down options for:

    **Select Calling policy** and **select PSTN-CP**

    Click **Apply**. Click **Confirm** on the pop-up window to confirm.

    ![A screenshot of a computer Description automatically
generated](module_1a_media/media/image32.png)

15. This completes the Direct Routing configuration for Microsoft Teams.

### Module 1a.2: Testing the calls from Microsoft Teams for Direct Routing \[Approx 10 min\]

> **NOTE**: *If you have completed any of Modules 3 or 4 before completing this module, you may have disabled Microsoft Native dialing. If so, login to Microsoft Teams Admin Center and* go to **Voice** \> **Calling policies**. On the Calling policies page select **Global (Org-wide default).** On the **Global (Org-wide default)** policy page toggle **on** the option for **Make private calls** and click **Save**. Click **Confirm** on the pop-up window.

1.  Continuing on Workstation 1. Open Microsoft Teams from the
    desktop/taskbar and log in with credentials
    <cholland@cbXXX.dc-YY.com> and **dCloud123!** Click **OK**. Click
    **Done** on the next pop-up window.

    > **NOTE:** *You need to Replace XXX, YY (in domain name) with your session-specific details. If you haven't already done as explained in Accessing your lab section, go to Lab_info.txt file located on your **workstation 1** and copy the domain and password.*

    > **NOTE**: *DO NOT click* ***_No, sign into this app only_***. Ignore the warning about Microsoft Teams update and continue to use Classic one.

    ![A screenshot of a computer Description automatically
generated](module_1a_media/media/image33.png)

2.  Accept any information/warning messages while logging in.

    > **NOTE**: *Before we continue to test, on workstation 1, go to the notifications 
    \[*![](module_1a_media/media/image34.png)*\] (bottom right corner, next to the time) and make sure **Quiet hours** are turned **off**. If it is turned on (shows in the color Blue) click it to turn it off.*

    ![A screenshot of a computer Description automatically generated](module_1a_media/media/image35.png)

3.  Now on Microsoft Teams, go to **Calls** on the left side pane.  Using the dial pad, dial the phone number (**MUST be a US Phone number**)
    in E.164 format. Example +19725556018 or if you do not have a US
    Phone number, you can dial Cisco support number **+18005532447**.

    > **NOTE**: *Click continue to use Teams Classic if you are prompted in this module or switch when I am not using Teams*.

4.  Make sure the call is connected. Hang up the call after a few
    seconds.

    ![A screenshot of a computer Description automatically
generated](module_1a_media/media/image36.png)

    > **NOTE**: *You will experience one-way audio as you are using a virtual workstation and will not be able to use the microphone.*

5.  To make an inbound call, on **workstation 1**, go to
    **Lab_info.txt** and note down the DID number assigned for Charles
    Holland. Dial that number from your mobile. If you cannot make calls
    to a US number from your mobile phone, contact one of your proctors.

    ![A screenshot of a computer Description automatically
generated](module_1a_media/media/image37.png)

6.  The incoming call should ring on workstation 1. Answer the call and
    verify the call is connected. Hang up the call after a few seconds.

    ![A screenshot of a computer Description automatically
generated](module_1a_media/media/image38.png)

7.  This completes testing the calls from Microsoft Teams for Direct
    Routing.

This completes ***Module 1a -- Direct Routing with CUBE.*** Let's
proceed to **Module 1b -- Interworking between CUCM and Microsoft Phone
System using CUBE.**

## Module 1b: Interworking between Cisco Unified CM and Microsoft Teams Phone via CUBE \[Approx 20 min\]

> **IMPORTANT NOTE**: Make sure you have **COMPLETED Module 1a** (Direct
Routing with CUBE) before continuing. Module 1a is a
**mandatory/prerequisite** module to go through Module 1b.

Customers using Microsoft Teams Phone have the option of not only
connecting to the PSTN using CUBE, but also **to an internal phone
system such as Cisco Unified Communications Manager.**

The following topology uses a co-resident CUBE for Direct Routing. You
can also use a dedicated CUBE instance for Direct Routing and an
additional gateway for connection to the PSTN.

![A diagram of a computer network Description automatically generated](module_1b_media/media/image1.png)

### Module 1b.1: Add required dial-peers on CUBE for Cisco UCM routing \[Approx 5 min\]

We need to add two dial-peers (inbound and outbound) on CUBE for routing
calls to/from CUCM.

1.  Continuing on Workstation 1, go to the putty session where you have
    logged into CUBE. If the previous login has timed out, log back in
    again as **admin** and **dCloud123!**

    > **NOTE**: *Like before, all the commands that you need to execute in
 this section are saved in a text file named **MSFT-To-UCM.txt** and
 put on Workstation'1 Desktop. We recommend copying the commands from
 that text file and pasting it onto Putty, to avoid any formatting
 issues from PDF/Word. You can still follow this guide for command
 explanations*.

    > **IMPORTANT NOTE**: *Be cautious of copying & pasting the
 commands/certificates as adding an extra space or leaving a character
 out would cause issues and that involves a lot of troubleshooting and
 redoing of those commands.*

2.  Add below voice class uri and an inbound dial-peer for accepting the
    inbound calls from CUCM (198.18.133.33)

        config t

            voice class uri 390 sip

                host ipv4:198.18.133.33

            end

        !

        config t

            dial-peer voice 390 voip

                description inbound dial-peer from Cisco UCM

                session protocol sipv2

                incoming uri via 390

                voice-class codec 1

                voice-class sip tenant 100

                dtmf-relay rtp-nte

                no vad

            end

        !

    ![A screen shot of a computer code Description automatically
generated](module_1b_media/media/image2.png)

3.  Add outbound dial-peer to route calls to CUCM using the below
    commands.

    > **NOTE**: *By default, when you make an outbound call, Microsoft Teams
    adds **+1** to the dialed number. To make it easy for configuration in
    the lab we are adding the destination pattern with **+1** and we are
    adding dial-peer for only one user (Anita Perez). In production
    environments, you can use translation patterns on Microsoft Teams
    admin centre to not add +1 by default and you can generalize the
    dial-peer according to your organizational dial plan.*

        config t

        dial-peer voice 300 voip

            description outbound to UCM

            destination-pattern +16017$

            session protocol sipv2

            session target ipv4:198.18.133.33

            voice-class codec 1

            voice-class sip tenant 100

            dtmf-relay rtp-nte

            no vad

        end

    ![A screen shot of a computer code Description automatically
 generated](module_1b_media/media/image3.png)

Now cube configuration is complete for UCM calls. Save the
    configuration with following command & press **Enter** twice.

 `copy running-config startup-config`

### Module 1b.2: Configure SIP Trunk and Route Pattern on Cisco UCM to route calls to CUBE \[Approx 10 min\]

1.  Continuing on Workstation 1, open a new browser tab. From the
    browser home page go to **Collaboration Admin Links** \> **Cisco
    Unified Communications Manager** (or you can directly connect to
    <https://cucm1.dcloud.cisco.com>). Login as **administrator** &
    **dCloud123!**

2.  Once logged in to Cisco UCM go to **Device** \> **Trunk.** Click
    **Add New.** It will take you to Trunk Configuration page.

3.  On the Trunk configuration page drop down option for **Trunk Type**
    and choose **SIP Trunk.** Leave the rest of the options as is and
    click **Next**.

    ![A screenshot of a computer Description automatically
generated](module_1b_media/media/image4.png)

4. On the **Trunk Configuration** page populate the following information and click **Save** to save the configuration. You will need to scroll down to see the **Inbound Calls** and **SIP Information** sections on the Trunk Configuration page.


    | Parameter Name                              | Parameter Value                     |
    |---------------------------------------------|-------------------------------------|
    | Device Name                                 | Direct-Routing-Trunk                |
    | Device Pool                                 | dCloud_DP                           |
    | Inbound Calls \ Significant Digits          | 4                                   |
    | Inbound Calls \ Calling Search Space        | Call_Everyone                       |
    | SIP Information \ Destination \ Destination Address | 198.18.133.231                |
    | SIP Information \ SIP Trunk Security Profile | Non Secure SIP Trunk Profile       |
    | SIP Information \ SIP Profile               | dCloud Standard SIP Profile         |


    ![A screenshot of a computer Description automatically generated](module_1b_media/media/image5.png)
    
    ![A screenshot of a computer Description automatically generated](module_1b_media/media/image6.png)

    ![A screenshot of a computer Description automatically generated](module_1b_media/media/image7.png)
  
5. Once the Trunk is saved, click **Reset** and click **Reset again**
    on the pop-up window to confirm. Within two minutes the trunk should
    come into **Full Service** as shown below.

    ![A screenshot of a computer Description automatically generated](module_1b_media/media/image8.png)

6.  Now, on the Cisco UCM go to **Call Routing** \> **Route/Hunt** \>
    **Route Pattern.** Click **Add New**

7.  On the Route Pattern Configuration page populate the following and
    Click **Save**. Click **OK** to accept any pop-up windows while
    saving the route pattern.

    ```
    -----------------------------------------------------------------------
    Parameter                     Value
    ----------------------------- -----------------------------------------
    Route Pattern                 6018

    Route Partition               Base_PT

    Gateway/Route List            Drop down and choose Direct-Routing-Trunk
    -----------------------------------------------------------------------
    ```

    ![A screenshot of a computer Description automatically generated](module_1b_media/media/image9.png)

8.  This completes the configuring SIP Trunk and route patterns on Cisco
    UCM. Now, you have routing configured between Microsoft Teams &
    Cisco UCM (both ways) using CUBE.

### Module 1b.3: Testing the calls between Microsoft Teams and Cisco UCM using CUBE \[Approx 5 min\]

1.  Open RDP connection to Workstation 2 using the one of the methods
    described in **Accessing the lab section.** Credentials for
    workstation 2 (Anita Perez) are **dcloud\\aperez** & **dCloud123!**

2.  Once logged into workstation 2, open **Cisco Jabber** from the
    desktop. The Jabber application should auto login as **Anita
    Perez**. If not, enter the email address <aperez@dcloud.cisco.com>
    on Jabber and click **Continue**. ON the next screen, enter username
    as **aperez** and password as **dCloud123!** Click Login.

    ![A screenshot of a login screen Description automatically
generated](module_1b_media/media/image10.png)

3.  Now, let's make inbound call towards Microsoft Teams. From **Cisco
    Jabber** (as **Anita Perez**), dial **6018** (extension number of
    **Charles Holland** on Microsoft Teams). Answer the call on
    **Workstation 1** Microsoft Teams (as **Charles Holland**). Make
    sure the call gets connected. Wait for few seconds and hang up the
    call.

    > **NOTE**: *You will not be able to hear the audio because we are using
    virtual workstations and microphone is not available.*

    ![A screenshot of a video chat Description automatically generated](module_1b_media/media/image11.png)

4.  Now, let's try to make outbound call from Microsoft Teams. From
    workstation 1 (as **Charles Holland**) dial extension number
    **6017** (extension number of **Anita Perez** on Cisco CUM). Answer
    the call on Workstation 2 Cisco Jabber (as Anita Perez). Make sure
    the call gets connected. Wait for few seconds and hang up the call.

5.  This completes testing the calling between Microsoft Teams and Cisco
    UCM using CUBE.
