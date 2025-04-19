# Exercise: Securing a Login Page Against Brute Force Attacks

[Return to Lab Contents](#lab-contents)

## Requirements

Before you begin, you need

- A BIG-IP Next instance 

- An application security policy applied to the BIG-IP Next instance

## Scenario

In this lab, you will secure the login page for the protected application from brute force attacks. 

## Objectives

At the end of this lab you will be able to:

- Define a Login URL for protection

- Understand and apply brute force protection options as desired

- Locate brute force mitigation activity in the event request log

## Lab

### A. Review brute force protection properties in the application security policy

1. In BIG-IP Next Central Manager, navigate to **SECURITY >> WAF > Policies**

1. On the resulting **Policies** page click your policy (The name is a link.)

1. In the **WEB PROTECTION** section select **Brute Force Protection** and then click **Create**

1. Your next task is to specify a login page. Click the **Create** link below **Login Page**

### B. Configure Login Page Properties

1. Click **Create** below the **Login Page** form.

1. In the **Login URL** field enter **/rest/user/login**

1. From the **Select Method** menu select **POST** and then click **Save**

1. From the **Authentication Type** menu select **AJAX/JSON**

   1. For the **Username Parameter** enter **email**

   1. For the **Password Parameter** enter **password**

1. From the **Condition** menu below **Login Conditions** select **Expected Response Status Code**

1. In the **Value** field enter **200**

1. Click **Save**

1. You are returned to the **Brute Force Protection Properties** page. In order to expedite the lab, let's reduce the maximum number of failed login attempts from an IP address before the blocking action will occur. In the **Maximum Failed Login Attempts** field enter **5**

1. Scroll down to the **Mitigate Brute Force Attacks** section and reduce the **Maximum Prevention Duration** period to **2** minutes in order to prevent yourself from being blocked for an hour after you trigger a violation.

1. Reduce the **Detection Period** to **2** minutes to prevent yourself from being blocked later in the lab.

1. Click **Save**

1. Click **Deploy** as needed.

### C. Register as a new user in Juice Shop

1. Browse to `http://10.10.1.102`

1. At the top right of the page select **Account > Login**

1. On the resulting page select **Not yet a customer?** at the bottom the form.

1. Register as a new user on the JuiceShop app with email **student1@f5.com** and password **password**

1. Pick a security question and provide an answer

1. Log in to the application (to prove that registration worked) and then log out.


### D. Trigger a brute force violation

1. Try logging back in to the application using the **correct username** and **wrong password** six or seven times.

1. What happens? The login page should fail to load. Some single page applications, including Juice Shop, do not display the default blocking response page. Instead, you should see some garbled text such as ** Object/object**

1. Go back to your BIG-IP Next Central Manager and select **Cancel** to return to the **Policies** page.

1. Refresh **WAF Dashboards**

1. Scroll to the bottom left of the dashboard and locate the **Violations/Sub-Violations (Top 20)** section. You should see **Maximum login attempts are exceeded** at the bottom of the list.

In order to prevent brute force protection from interfering with later labs lets remove the entire feature from your policy.

1. From the menu on the left, go to the **WAF** section and then click **Policies**

1. On the resulting page click the name of your security policy.

1. On the resulting page click **Brute Force Protection** near the bottom of the **WEB PROTECTION** settings on the left.

1. Select the checkbox to the left of your defined Login Page and then click the **Delete** icon near the top of the section.

1. Click **Yes, Delete** when prompted.

1. Click **Deploy** as needed and wait until you see **No Brute Force Protection** shown on the page.
