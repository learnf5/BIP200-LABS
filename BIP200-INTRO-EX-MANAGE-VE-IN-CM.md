# Exercise: Managing BIG-IP Next VE Instance in Central Manager

[Return to Lab Contents](#lab-contents)

## Requirements

Before you begin you need

- A running BIG-IP Next Central Manager

- A running BIG-IP Next VE Instance

## Scenario

In this lab, you will add an instance of BIG-IP Next to your Central Manager in preparation for licensing. 

## Objectives

At the end of this lab you will be able to

- Verify that BIG-IP Next is running

- Add an instance of BIG-IP Next to your Central Manager

## Lab 

1. Log into the **jump** box using the credentials **student** / **student**

1. Open a Terminal app and confirm BIG-IP is running

    `curl --insecure --silent --user admin:F5trn001! https://bigip1.f5trn.com:5443/api/v1/health/ready | jq --monochrome-output .`

    >[!Note] **Remember** BIG-IP Next VE takes a few minutes to fully spin up.  You may have to try this command several times before you see **"ready": true**

    >[!Note] **Note:** You will not be able to ssh into **bigip1** until the box has completed running cloud-init, which also takes a few minutes, but you can connect to the console, like you did in the previous lesson, and watch the individual containers start up

1. Using Chrome, connect to CM at `https://cm1.f5trn.com`

1. Sign in using `admin` / `F5trn001!` credentials.

1. On the main CM page, click **Manage Instances** 

1. On the new page, click **Start Adding Instances**

1. You have an instance that is already up and running.  Enter `192.168.1.31` for the IP address and click **Connect**

1. Use the `admin` / `F5trn001!` credentials and click **Next**

1. You are then instructed to *Provide a new username and password to manage this instance from BIG-IP Next Central Manager*.  It provides the suggested new username, **admin-cm**. You will reuse and then confirm the existing password `F5trn001!`

1. Click **Add Instance** and then **Add** in the dialog window.

1. You will be prompted to accept a new fingerprint. Accept it. 
    !IMAGE[accept-fingerprint.png](https://raw.githubusercontent.com/learnf5/BIP200-LABS/main/images/accept-fingerprint.png)

    >[!Note] **Note:** This step may take several minutes.  Wait for it to complete, **do not** click the OK button.

1. You now have a fully configured, CM-managed BIG-IP Next VE instance ready to be licensed.  Thanks to the **cloud-init** configuration, you won't have to configure the internal and external self IPs and VLANs, like you did in the previous lab.

    !IMAGE[bigip1-healthy.png](https://raw.githubusercontent.com/learnf5/BIP200-LABS/main/images/bigip1-healthy.png)
