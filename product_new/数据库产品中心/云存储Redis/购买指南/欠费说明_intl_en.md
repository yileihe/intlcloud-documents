

## Expiry Reminder for Pay-as-You-Go TencentDB Instances
 
![](https://mccdn.qcloud.com/img567f91951599d.png)
 
### Balance Reminder
We will estimate the number of days it takes your account balance to become negative based on the past 24 hours usage and current balance. If it's less than 5 days, we will send you a reminder message. The reminder message will be sent to the Tencent Cloud account creator and all the collaborators via email and SMS.

## Arrears Reminder
For pay-as-you-go resources, fees are deducted on the hour. When your account balance is in negative (Point 1 in the figure above), we will notify the Tencent Cloud account creator and all the collaborators via email and SMS.

## Arrears Processing
**Starting from the moment the account balance drops below zero:**
- You can continue to use your database for 2 hours from the moment your account becomes negative. We will also continue to bill you for this period..
- When your account is in arrears for 2 hours (Point 2 in the figure above), **your database instance will automatically shut down. We will also stop billing you for service**.

**After automatic shutdown:**
- Within 24 hours after automatic shutdown, if your account is not topped up to a positive balance, you will not be able to start your database; If your balance is positive, the billing continues, and you can start your database.
- If your account remains negative for 24 hours after shutdown (Point 3 in the figure above), the database will be repossessed, and **all data will be deleted and cannot be recovered**.

We will notify the Tencent Cloud account creator and all the collaborators via email and SMS when the database is repossessed.

>- When you do not use pay-as-you-go resources any longer, **terminate them as soon as possible** to avoid further fee deduction.
After the database is terminated or repossessed, the data will be deleted and cannot be recovered.
Since your actual resource consumption changes from time to time, some deviation may exist for the stated balance.
