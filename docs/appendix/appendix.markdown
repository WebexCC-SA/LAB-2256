# **Appendix**

**Updating SIP profiles manually**

1.  Continuing on Workstation 1. Minimize the putty session and find the
    file named SIP-Profiles_Direct-Routing.txt on Desktop. Right click
    on the file and choose Edit with Notepad++.

    ![A screenshot of a computer Description automatically
generated](appendix_media/media/image1.png)

2.  It will have 4 SIP profiles that we need to configure the Cube with.
    Before we configure on the cube, we need to update these SIP
    profiles with cube external ip (cube_ext_ip) & cube external DNS
    name (cbXXX.dc-YY.com).

3.  If not already done, go back to your dCloud session topology page.
    On the topology page go to Details tab and scroll down to the
    section where you see Network Address Translations and note/copy the
    **Public IP** address associated with **cube_ea** & copy the **A**
    name record for cube.

    ![A screenshot of a computer Description automatically
generated](appendix_media/media/image2.png)

4.  Go to Workstation 1 and Notepad++ where you have opened SIP Profiles
    file. We need to update cube external ip (cube_ext_ip) with
    64.100.11.125 (this IP is different for each lab, use the IP address
    from your own lab) & cube.XXX.dc-YY.com with cb205.dc-01.com (this
    DNS name also different for each lab, use DNS from your own lab).

5.  You can use find/replace feature of Notepad++ application to replace
    these values. Click anywhere on the notepad++ and press "Ctrl + F".
    It will bring up find pop-up window. Go to second tab (Replace) on
    the find pop-up window.

6.  In "**Find What:**" field enter cube.cbXXX.dc-YY.com & in "Replace
    with:" field enter cube. cb205.dc-01.com (this domain would
    different for you lab) & choose Replace each or select replace them
    all at once. Once all the values are replaced you will see "Replace:
    no occurrence was found." Message on the bottom left corner of the
    find window.

    ![A screenshot of a computer Description automatically
generated](appendix_media/media/image3.png)

7.  Once cbXXX.dc-YY.com values are replaced, Now replace "**Find
    What:**" field with "**cube_ext_ip**" & replace "**Replace with:**"
    field with **64.100.11.125** (Cube external IP, this would be
    different for your lab) & choose Replace each or select replace them
    all at once. Once all the values are replaced you will see "Replace:
    no occurrence was found." Message on the bottom left corner of the
    find window.

    ![A screenshot of a computer Description automatically
generated](appendix_media/media/image4.png)

8.  Once both values cbXXX.dc-YY.com & cube_ext_ip values for all
    SIP-Profiles in the file are updated. Copy all the content from
    **SIP-Profiles_Direct-Routing.txt** file and paste on the cube
    (putty window), make sure there are no errors generated.

    > **NOTE**: *If the login to Putty is timed out you may have to sign back in. Credentials are admin/dCloud123!.*

    ![A screenshot of a computer screen Description automatically
generated](appendix_media/media/image5.png)
