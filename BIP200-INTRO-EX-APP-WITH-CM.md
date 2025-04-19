# Exercise: Deploying Basic Application using Central Manager

[Return to Lab Contents](#lab-contents)

## Requirements

Before you begin you need

- A running BIG-IP Next Central Manager

- A running BIG-IP Next VE Instance with a valid license

## Scenario

In this lab, you will deploy the Juice Shop application using Central Manager. 

## Objectives

At the end of this lab you will be able to:

- Create a standard application containing a virtual server, pool, and pool member
- Deploy the application on your BIG-IP Next instance

## Lab

1. Click the Workspace menu (the 3x3 matrix of dots in the top left corner) and select **Applications**

1. On the new page, click **Start Adding Apps**

1. At this point, you have the option to create a new app or migrate one from an existing BIG-IP, but for this lab you will create a new app.

1. Name the app **juice-shop-app**, accept the default value of **Standard** and then select **Start Creating**

1. Add a description if you like and then select **Start Creating**

1. On the next page, select the **Pools** tab and then select **+ Create**

1. For the Pool Name, enter **juice-shop-pool**. Leave the default values in the other fields.

1. Select the **Virtual Servers** tab.

1. For the Virtual Server Name, enter **juice-shop-vs**

1. For the Pool, select **juice-shop-pool** and press **Review & Deploy**

1. Now you have to tell BIG-IP Next Central Manager where to deploy the app. In this circumstance there is only one BIG-IP instance, but that will normally not be the case.  Select **Start Adding**

1. Select **bigip1.f5trn.com** and then click **+ Add to List**

1. Enter **10.10.1.102** for the Virtual Address for BIG-IP Next.

1. Click the drop down button for Pool and then click **+ Pool Members**

1. In the new page, click **+ Add Row** once for a single pool member.

    1. For the Name, enter **juice-shop**

    1. For the IP Address, enter **172.16.20.160**

    1. Press **Save**

1. Press **Deploy Changes** and confirm by pressing **Yes, Deploy**

1. Now open a new tab in your Chrome browser on the jump box and navigate to `http://10.10.1.102`

1. Congratulations!

    - You configured BIG-IP Next Central Manager to manage a BIG-IP Next VE instance

    - You licensed a BIG-IP Next VE instance

    - You configured and ran an application on BIG-IP Next
