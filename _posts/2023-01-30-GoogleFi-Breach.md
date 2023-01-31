---
layout: post
title: GoogleFi Limited Date Breach
author: Phillip Kittelson
categories: cybersecurity
tags: GoogleFi Google cybersecurity data breach
date: 2023-01-30
intro: 
image: assets\images\featured-image\googlefi.png
---
__Updated @ 21:26 EST__

GoogleFi sent out an email on 30 Jan 2023, informing its users of suspicious activity on the network of a "primary network provider."

The system in question, a 3rd party used for "GoogleFi customer support purposes" contains limited customer data including the following:

- Phone number
- When accounts were activated
- Data about a user's mobile service plan
- SIM card serial number
- Account status, active or inactive

GoogleFi stated the potentially limited data breach does not include information such as name, date of birth, email addresses, and payment card information.

While the email does not include the name of the 3rd party, the site [9to5Google.com](https://9to5google.com/2023/01/30/google-fi-data-breach-tmobile/){: .hover-underline-animation target="_blank"} suspects the 3rd party could be T-mobile, which recently release news of their own [data breach](https://9to5mac.com/2023/01/19/t-mobile-data-breach-customer-info/){: .hover-underline-animation target="_blank"}.


## Google's Email
> Dear Google Fi customer,
>
>We’re writing to let you know that the primary network provider for Google Fi recently informed us there has been suspicious activity relating to a third party system that contains a limited amount of Google Fi customer data.
>
> There is no action required by you at this time.
>
> This system is used for Google Fi customer support purposes and contains limited data including when your account was activated, data about your mobile service plan, SIM card serial number, and active or inactive account status.
>
> It does not contain your name, date of birth, email address, payment card information, social security number or tax IDs, driver’s license or other form of government ID, or financial account information, passwords or PINs that you may use for Google Fi, or the contents of any SMS messages or calls.
>
> Our incident response team undertook an investigation and determined that unauthorized access occurred and have worked with our primary network provider to identify and implement measures to secure the data on that third party system and notify everyone potentially impacted. There was no access to Google's systems or any systems overseen by Google.
>
> If you are an active Fi user, please note that your Google Fi service continues to work as usual and was not interrupted by this issue.
>
> What does this mean for me?
>
>The accessed information included your phone number and limited technical information. This includes information about when your account was activated, SIM card serial number, account status (for example, whether your plan is active or inactive), and limited details about the mobile service plan and options provided by your Google Fi service (such as unlimited SMS or international roaming).
>
> For more information
>
> As always, be alert for phishing attempts. For more about best practices, see our advice on [how to avoid phishing](https://support.google.com/mail/answer/8253#zippy=%2Cpay-attention-to-warnings-from-google%2Cnever-respond-to-requests-for-private-info%2Cbeware-of-messages-that-sound-urgent-or-too-good-to-be-true%2Cstop-think-before-you-click%2Cuse-gmail-to-help-you-identify-phishing-emails%2Cuse-safe-browsing-in-chrome%2Ccheck-for-unsafe-saved-passwords%2Chelp-protect-your-google-account-password%2Clearn-about--step-verification%2Cdont-enter-your-password-after-clicking-a-link-in-a-message){: .hover-underline-animation target="_blank"}.
>
> Read more about [keeping your Google Fi information safe](https://support.google.com/fi/answer/13274172?visit_id=638107279937551347-538348395&p=January2023&rd=1){: .hover-underline-animation target="_blank"}.
>
> We’re always here for our customers and available to offer support. If you have any questions or require assistance, please see this Help Center [article](https://support.google.com/fi/answer/13274172?visit_id=638107279937551347-538348395&p=January2023&rd=1){: .hover-underline-animation target="_blank"} for contact options and reference issue ID 267187948.
Sincerely,
>
>Google Fi Team


## What does this mean for me, as a user?
If you are GoogleFi user, while at this point there is no reason to believe other information about your has been copied. For the most part, this breach could potentially just lead to more SMSishing attacks (a form of phishing using text messages) since subscriber phone number was included in the breach. As always, users should be cautious when clicking on links from unknown numbers.

Other general security steps a users can take include:
- Enabling 2-Factor Authentication (2FA) on Google accounts
- Adding a recovery email and phone number to GoogleFi accounts
- Ensure strong passwords are used for their account