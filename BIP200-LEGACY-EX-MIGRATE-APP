# Exercise: Migrating Application from Version 17.1 to BIG-IP Next

[Return to Lab Contents](#lab-contents)

## Requirements

Before you begin:

- You will need the configuration (archive) file from 

- You will need an BIG-IP Next VE instance that has been configured in BIG-IP Next CM and has been licensed

## Scenario

Now that you have a BIG-IP Next VE instance configured in BIG-IP Next CM that is licensed, you need to create an application using the configuration from an older version of BIG-IP and pass traffic through the BIG-IP.

## Objectives

At the end of this lab you will be able to:

- Configure an application on BIG-IP Next VE instance using the configuration from an older version of BIG-IP

## Lab

1. Click the Workspace menu (the 3x3 matrix of dots in the top left corner) and select **Applications**

1. In the new page, click **Start Adding Apps**

1. Click the blue **New Migration** button follow the wizard

    - Session Name: **legacy-app**

    Click **Next**

1. Click in the box where it says *Drag and Drop... or click to select*

1. In the file browser dialog box that opens, click the **Downloads** folder, then double-click the **bigip2.ucs** file

1. You should see the file selected for the Source BIG-IP System

1. Next, you need the Master Key from the BIG-IP.  On the Ubuntu Desktop Dock, open the terminal app and connect to **bigip2** with `ssh root@bigip2.f5trn.com` and `f5trn002` password

1. At the prompt, enter `f5mku -K`.  Copy the resulting response and paste in to browser window in the **Master Key** field

1. While you're on **bigip2**, disable the virtual server because the app migrating to **bigip1** aka BIG-IP Next, will share the same IP address.  At the type, enter

    ```
    tmsh modify ltm virtual legacy-app-vs disabled
    ```

1. The next part doesn't really matter because the UCS archive only has a single app, but you have to choose something.  Select **Group by IP Addresses (Recommended)** and click **Next**

    >[!Note] **Note:** This step may take a minute

1. On the next page, click the **Add Application** button

1. Click the drop down for **application_1** and then select **Common_legacy-app-vs** and click **Add**]

1. Review the next screen and click **Next**

1. In the **Deploy Location** drop down, select **bigip1.f5trn.com** and press **Deploy**

1. On the next page, click the **Finish** button

1. Open a new tab on the Chrome browser and navigate to your new application running on BIG-IP Next, `http://10.10.1.103`

    !IMAGE[5cgmm1p7.jpg](instructions261771/5cgmm1p7.jpg)
