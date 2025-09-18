## Accessing your Lab -- \[Approx 10 min\]

1.  Open a browser on your laptop and go to <https://dcloud.cisco.com> 

2.  Click **Login** at the top right corner and log in with your
    ***cisco.com*** credentials

    ![Graphical user interface, text, application, email Description
    automatically generated](lab_access_and_tenant_config_media/media/image1.png)

3.  Once logged in, open a new browser tab and paste the **event URL**
    for your lab. The **event URL** is
    [https://dcloud2-sjc.cisco.com/event/397145/access](https://dcloud2-sjc.cisco.com/event/397145/access).

4.  You will be automatically assigned to a lab session and will be
    taken to the lab topology page as shown below.

    ![A computer network diagram with many computers Description automatically generated](lab_access_and_tenant_config_media/media/image2.png)

5.  Click on the **Workstation 1** **Charles Holland** icon on the
    topology page and it will bring up a fly-out window on left with
    **Workstation 1** related information like **IP Address**,
    **username,** and **password** as shown below.

    ![A screenshot of a computer Description automatically generated](lab_access_and_tenant_config_media/media/image3.png)

6.  Similarly, you can click on any other Virtual Machine on the
    topology page to get its accessing details.

7.  In this lab, you will access **Workstation 1** (through **WebRDP or
    Remote Desktop**) and from **Workstation 1** you will be able to
    access all the other virtual machines or Cisco UC applications like
    Cisco UCM, CUBE, etc., to complete the lab tasks.

8.  There are **two** ways you can access **Workstation 1**. You can
    either connect via a **local RDP connection** (option A - preferred)
    connection or via a **WebRDP connection** (option B) from your
    classroom laptop.

    **Option (A) -- \[Preferred\]**
    
    To connect to the Workstation using your **local RDP connection**,
    first, you need to connect to your lab session via a VPN. Open **Cisco
    AnyConnect** on your laptop. It will prompt you for the **Host
    Address**, **username,** and **password** information for your
    session. You will find all these details under the **Info** \ 
    **AnyConnect** **Credentials** section of your lab. Enter all the
    details as shown below and click **OK** to connect to your session.
    The **Host Address**, **username,** and **password** will be different
    for each lab. Use **YOUR OWN** assigned lab details.
    
    ![A screenshot of a computer Description automatically generated](lab_access_and_tenant_config_media/media/image4.png)
    
    Once you are connected to your lab session over VPN, you can open a
    local RDP connection on your laptop and connect to **Workstation 1**
    using the following details:
    
    Host: **198.18.1.36**
    
    Username: **dcloud\\cholland**
    
    Password: **dCloud123!**
    
    **Option (B)**
    
    To access Workstation 1 over **WebRDP**, click on the **Workstation
    1** icon on the topology page and when it brings up a fly-out window
    with workstation details. On the fly-out window go to click on the
    **Remote Access \  Web RDP**. It will open a new browser tab and
    connect you to Workstation 1.
    
    ![A screenshot of a computer Description automatically
    generated](lab_access_and_tenant_config_media/media/image5.png)

9.  On the lab topology page, click on the **Info** tab on the top a
    fly-out window will open on left side. Here you will find all your
    lab-specific access information like the **Session ID**, **DNS
    Domain** name, **PSTN Numbers,** etc., You will need all this
    information throughout this lab session. All this information is
    captured and put in a text file called ***Lab_info.txt*** file on
    **Workstation 1'**s Desktop. Once you have connected to
    **Workstation 1** using one of the methods mentioned above, open the
    text file ***Lab_info.txt*** located on Desktop and review it. Keep
    this file open and handy as you will need this information
    throughout the lab.

    ![A screenshot of a computer Description automatically
  generated](lab_access_and_tenant_config_media/media/image6.png)
 
  ***Below information is just for reviewing purpose only.***
 
  **Session ID**: you will find it under the details tab, as sho­wn above
  (Example **1041368**)
 
  **Control Hub password**: dCloud**1368**! (**dCloud** + last four
  digits of **session ID** + ***!***)
 
  **Domain Name**: Go to the **Info** tab of your session and scroll
  down to see the **DNS** section. It will be in the **cbXXX.dc-YY.com**
  format.
 
  **Expressway -- E Password**: Same as **AnyConnect password**, found
  under **Info** tab \  **AnyConnect Credentials**.
 
![A screenshot of a computer Description automatically generated](lab_access_and_tenant_config_media/media/image7.png)