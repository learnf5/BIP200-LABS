# Exercise: Creating and Testing Application on BIG-IP Version 17.1

[Return to Lab Contents](#lab-contents)

## Requirements

Before you begin you need:

- A running BIG-IP Next Central Manager

- A running BIG-IP Next VE Instance

## Scenario

In order to use a BIG-IP Next VE instance, that instance must be managed by BIG-IP Next Central Manager.  In this lab you will configure new BIG-IP VE instance running in the Skillable that has been provided to you.  

## Objectives

At the end of this lab you will be able to:

- Add a BIG-IP Next VE instance to BIG-IP Next Central Manager

## Lab

1. Log into the **jump** box using the credentials **student** / `student`

1. Open the Chrome browser to `https://bigip2.f5trn.com` and login using credentials `admin` / `f5trn002`

1. Navigate to **Local Traffic** >> **Monitors** and click the **Create...** button

1. Create a new monitor using the following paramaters

    - **Name:** `legacy-app-mon`

    - **Type:** HTTP

    - **Received String:** `If you see this`

    and click **Finished**

1. Navigate to **Local Traffic** >> **Pools** and click the **Create...** button

1. Create a new pool using the following parameters

    - **Name:** `legacy-app-pool`

    - **Health Monitors:** legacy-app-mon

    - **New Members Address / Port**

        - 172.16.20.161 / 80 and click **Add**

        - 172.16.20.162 / 80 and click **Add**

        - 172.16.20.163 / 80 and click **Add**

    and click **Finished**

    > [!Note] **Note:** Unlike BIG-IP Next, this version of BIG-IP does not require that you name each pool member.  Leave that field blank

1. Navigate to **Local Traffic** >> **Virtual Servers** and click the **Create...** button

1. Create a new virtual server using the following parameters

    - **Name:** `legacy-app-vs`

    - **Destination Address/Mask:** `10.10.1.103`

    - **Service Port:** `80`

    - **Source Address Translation:** Auto Map

    - **Default Pool:** legacy-app-pool

    and click **Finished**

1. Open a new tab in your Chrome browser on your jump box and navigate to `http://10.10.1.103`

1. You should see a page similar to

    !IMAGE[jemllx0g.jpg](instructions261771/jemllx0g.jpg)

1. You have successfully built a basic app on BIG-IP version 17.1

1. Save and download the configuration of the BIG-IP.  You will use the archive to migrate the app over to a BIG-IP Next VE instance.  Navigate to **System >> Archives** and click **Create...***

    - File Name: **bigip2.ucs**

    Click **Finished**

    >[!Note] **Note:** Creating an archive may take a few minutes

1. When the archive has been saved locally, click **OK**

1. On the **System >> Archives** page, click the filename link you just created, **bigip2.ucs**

1. Click **Download: bigip2.ucs** to download the archive file to the jump box
