# Exercise: Deploying an Application Security Policy

[Return to Lab Contents](#lab-contents)

## Requirements

Before you begin, you need

- A BIG-IP Next instance 

- A deployed application ready to be secured

## Scenario

In this lab, you will first exploit a web application vulnerability to demonstrate pre-protection behavior.  Then you will deploy a security policy using the [Rating-Based template](https://clouddocs.f5.com/bigip-next/latest/waf_management/awaf_rating_based_overview.html) to mitigate the vulnerability.

## Objectives

At the end of this lab you will be able to:

- Use SQL injection to retrieve a list of all users and md5-hashed passwords from the target application

- Create an application security policy using the Ratings-Based template

- Verify web application protection on the  BIG-IP Next instance

- Demonstrate that protection is applied to requests

- Locate attack data in the WAF Dashboard and Event Log

- Review protection and event logging settings defined in the security policy

## Lab

 ### Exploit a SQL injection vulnerability

1. In your current browser connection to the virtual server IP address at 10.10.1.102, load `http://10.10.1.102/rest/products/search?q=qwert')) UNION SELECT id, email, password, '4', '5', '6', '7', '8', '9' FROM Users--`

1. Press **Enter** and then review the data returned by the injection. You can see user and password hash values near the top of the output.

 ### Create an application security policy

1. Go back BIG-IP Next CM, click the Workspace menu (the 3x3 matrix of dots in the top left corner) and select **Applications**

1. Click the **juice-shop-app** link near the bottom of the page (the name is a hypertext link).

1. At the top right of the resulting page click **Edit**

1. At the bottom of the resulting page click the icon associated with **Security Policies**:

1. Enable **Use a WAF Policy**

1. Click **+ Create**

1. Provide the name **my_policy**

1. At the top right of the page enable **Advanced View** so that you can see all protections that will be applied.

1. Note that **Bot Defense**, **Threat Campaigns**, and **IP Intelligence** are applied by default.

1. Directly below **Threat Intelligence** note that the **Enforcement Mode** of the policy is **Blocking**

1. Scroll down slightly and note that the **Rating-Based Template** will be applied. This template is used by default and offers a moderate level of security with minimal tuning and administrative work.

1. Note that the default **Application Language** is **Unicode (utf-8)** which is appropriate for the target application in this lab. Your real-world application may use a different Application Language which can be selected in this section.

1. Click **Save** as needed.

1. Click **Review and Deploy**

1. Click **Deploy Changes**

1. Click **Yes, Deploy**

 ### Verify and Review Protection Settings

1. In your browser, load `http://10.10.1.102/rest/products/search?q=qwert')) UNION SELECT id, email, password, '4', '5', '6', '7', '8', '9' FROM Users--`

1. What happens? The request should be blocked. Now let's check the event log.

1. In your BIG-IP Next Central Manager navigate to **Security** **> Event Logs**
 
1. Locate the blocked request and then click the URI **/rest/products/search** 

1. Take a few minutes to review the details regarding the violations causing the blocking event.

1. Click the **X** at the top right of the page to close the current window and return to the **Event Logs** page.

 ### Review Policy Protection Settings

1. In BIG-IP Next Central Manager, navigate to **SECURITY >> WAF > Policies**

1. On the resulting WAF policy list page, note the name of your policy, its Enforcement Mode, and the Application. On the far right you can see the date the policy was last modified.

1. Click the name of your policy (the name is a hypertext link.)

1. On the resulting Policy Settings page, click the **Advanced View** button at the top right to reveal more controls.

1. Scroll down to the middle section of the page and notice that the policy **Enforcement Mode** is **Blocking** 

1. Take a few minutes to review the other policy protection settings such as **Allowed Response Codes** 

1. Note that  **Log Events** which is currently set to **Illegal, include staging**. By default, only illegal requests (those requests which have violated a security policy rule) are logged. This is intentional in order to prevent a large number of requests from appearing in the Event Log. In a testing or training environment, you can log all requests to verify that the system is receiving requests. The "include staging" option will log requests which trigger violations on staged entities such as attack signatures, file types, parameters and other elements which can be subjected to a staging period in order to prevent false positives.
