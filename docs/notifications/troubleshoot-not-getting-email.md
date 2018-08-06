# Not getting an email

An email is generated when an [event](oob-supported-event-types.md) occurs within VSTS which matches a notification subscription.  See [overview](./about-notifications) for more information about notification subscriptions.

If you're not receiving an expected notification email, it could be for one of the following reasons

* The email was delivered to an unchecked folder
* The subscription is disabled or opted-out
* The event does not match the specified subscription filter conditions
* The subscription is defined to not send emails to the initiator of an event
* The account level _do not deliver_ setting is impacting email delivery
* The team or group level _do not deliver_ setting is impacting email delivery
* You are not a member of the group or team receiving the email

Please perform the following step to determine if any of these resolve the issue.

## Step 1: Check other email folders including the junk folder
Ensure the email was not delivered to a differet email folder.

## Step 2: Locate the subscription in the user interface
Navigate to your personal subscriptions and locate the subscription which you feel should have produced an email, but didn't.  Click [here]() to learn how to navigate to your personal subscriptions.

## Step 3: Ensure the subscription is enabled
If the subscription is greyed-out in the user interface, then it is disabled.

Default subscription become disabled when an administrartor opts-out at the account or team level, or if an individual opts-out in their personal subscriptions. Custom subcriptions become disabled when an administrator disables the subscription at the account or team level, or an individual disables a personal custom subscription.  Click [here](howto-disable-subscriptions) to learn more about outing-out or disabling subscriptions.

## Step 4: Closely inpsect the subscription filter conditions
An email is only generated if a VSTS event matches all the filter conditions of the subscription. View the filter conditions by clicking the subscription link in the subscription user interface.  You should be able to view the filter conditions even if you don't have permision to change them.  Closely instect all filter conditions to see if they matched the VSTS event.

## Step 5: Check the "Skip initiator" option on the subscription
The `Skip initiator` checkbox option on a subscription will cause the initiator of the VSTS event to be excluded from the recipient list of an email generated, while all others will receive the event.  For example, consider a subscription for a work item changed event.  You can choose `Skip initiator` to avoid being emailed for changes you make to the work item.  Click [here](howto-exclude-self-from-email.md) to learn more about this option.

## Step 6: Check "Do not deliver" setting for the account
Navigate to the account level notifications hub and click the `Settings` tab (click [here](howto-manage-account-notification-settings.md) to learn how).  If delivery setting is set to `Do not deliver`, then all team or groups that don't have explicit delivery settings will inherit this value.  This setting alone doesn't necessarily indicate an email wasn't delivered but it could be.  Continue with the next step to determine if a group or team delivery setting is inheriting this value and blocking delivery to your group or team.

## Step 7: Check "Do not deliver" setting for your team or group
 If the team or group define a delivery setting for "Deliver to individual members", it's still possible that the team contains other groups which have a different delivery setting.  Click [here](concepts-group-expansion-for-email.md) to learn team membership is expaneded and how some members of the team could receive an email while others do not.

## Step 8: Ensure your email address is included as a recipient for this subscription
Click [here]() to learn more about how email recipients are determined.

## Contact customer support
If you're not able to resolve the issue with the steps above, consider contacting [customer support](troubleshoot-contact-support.md)



