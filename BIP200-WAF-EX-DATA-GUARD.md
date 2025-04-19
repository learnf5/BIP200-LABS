# Exercise: Preventing Information Leakage Using Data Guard

[Return to Lab Contents](#lab-contents)

## Requirements

Before you begin, you need

- A BIG-IP Next instance 

- An application security policy applied to the BIG-IP Next instance

## Scenario

In this lab, you will review an information leakage vulnerability in the target application and then mitigate it using Data Guard. 

## Objectives

At the end of this lab you will be able to:

- Demonstrate an information leakage vulnerability

- Mitigate information leakage using Data Guard

- Locate information leakage mitigation activity in the event request log

## Lab

  ### Review current credit card number handling

1. Log in to the Juice Shop application with the user credentials you just created: `student1@f5.com` / `password` (If you get a pop up with a security message about changing the password, click **OK**)

1. Click the **Account** link, then select **Orders & Payment**, then select **My Payment Options**

1. Add a new card using these credit card digits: `4111 1111 1111 1111` and then select **Submit** (the application will strip out spaces between four digit groups)

1. At the top left, click on OWASP Juice Shop logo to load the main web page.

1. Click the **Account** link, select **Orders & Payment**, and then select **My Payment Options**

1. What happens? All but the last four digits of the credit card number are masked by the application. This is because the application was written to mask digits in /saved-payment-methods. This is is a good security practice. However, data leakage usually occurs in places where the application developers did not think to secure.

  ### Introduce a Data Leakage Problem

1. Click the side menu icon to the left of the Juice Shop logo.

1. Click **Customer Feedback**

1. Submit a comment that includes the credit card number `4111 1111 1111 1111` for example:

1. In your browser, go to `http://10.10.1.102/api/Feedbacks` and scroll to the bottom of the JSON text results. Note that the app is not masking credit card numbers in **/api/Feedbacks** because nobody ever thought that sensitive data could appear here. 

  ### Enable Data Guard for credit card numbers

1. In BIG-IP Next Central Manager, navigate to **SECURITY >> WAF > Policies**

1. On the resulting **Policies** page click your policy (The name is a link.)

1. In the **WEB PROTECTION** section select **Data Guard** near the bottom of the list and then select **Enable**

1. Accept the default values to detect credit card numbers and expose the last four characters of credit card numbers. 

1. Select **Save**

1. Select **Violations** at the top right of the page.

1. Note that the default action is to **Alarm** which means that credit card numbers appearing in responses will be masked and logged, but no blocking action will occur.

1. Select **Cancel & Exit**

1. Click **Deploy**

1. Select **Cancel** once more to return to the main **Policies** page.

  ### Verify that Data Guard is masking credit card digits

1. Reload http://10.10.1.102

1. Try submitting different customer feedback using `4111 1111 1111 1111` and reviewing the result.

1. Go to `http://10.10.1.102/api/Feedbacks` and scroll to the bottom of the results. Credit card data should be masked. 

  ### Review Event Logs

1. In BIG-IP Next Central Manager, navigate to **SECURITY >> Event Logs**

1. Select the event for **/api/Feedbacks** at the top of the list.

1. Scroll to the **Triggered Violations** section and review the violation data related to Data Guard.
