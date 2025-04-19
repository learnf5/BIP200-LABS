# Exercise: Licensing BIG-IP Next VE Instance

[Return to Lab Contents](#lab-contents)

## Requirements

Before you begin you need

- A running BIG-IP Next Central Manager

- A running BIG-IP Next VE Instance 

- An F5 account for accessing trial licenses

## Scenario

In this lab, you will download a trial license for your BIG-IP Next VE instance and verify that you can pass traffic.

## Objectives

At the end of this lab you will be able to:

- Download and activate JSON Web Token for licensing purposes

## Read This Before You Begin

**You may choose to skip this lab.**  You will still be able to complete the lab series and build the app in the final lab.  Even though the unlicensed BIG-IP will not pass traffic, the configuration experience is the same.

## Lab

1. Using Chrome on the jump box, navigate to `https://my.f5.com`

1. **Sign In**.  You should have created an account in the previous lab, if you didn't already have one.

1. Click **Trials >**

1. Scroll to the bottom of the page and in **My Trials**, click **BIG-IP Next**

1. Click **Downloads and licenses** *or* **+ Instance (license)** to download a trial license.

1. On the resulting page click **Download JSON Web Token**

1. Open the downloaded file in a text editor.  You will need to copy and paste the token in just a moment.

1. Using Chrome on jump, navigate to `https://cm1.f5trn.com`

1. Log in using **admin** / **F5trn001!** credentials.

1. On the main CM page, click **Manage Instances** 

    !IMAGE[qb6krnx1.jpg](instructions261136/qb6krnx1.jpg)

1. Select the checkbox to the left of the BIG-IP that you just added.

1. Click the **Actions** button and select **License** from the drop down menu.

1. Read the page and click **Next**

1. Copy and paste the token into the **JSON Web Token** field.

1. Provide a name of this token, such as **trial-token** and then click **Activate**

    !IMAGE[6s6f71zi.jpg](instructions261136/6s6f71zi.jpg)

1. Click **Exit**
