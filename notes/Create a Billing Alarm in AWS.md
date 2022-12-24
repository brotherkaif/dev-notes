**ID:** 1202212240112
**STATUS:** #permanent-note
**TAGS:** #aws #cloud-platforms #dev-ops #tutorial

---

# Create a Billing Alarm in AWS

1. Log into the AWS console with the root user account
2. Navigate to _”[your name]” (top right)_ > _“My Billing Dashboard”_
3. Select _“Billing Preferences” (left menu)_
4. Click _“Receive Billing Alerts”_ (note: can’t be disabled once selected)
5. Click _“Manage Billing Alerts”_ (will redirect you to CloudWatch)
6. Click _“Alarms” (left menu)_
7. Click _“Create alarm”_
8. On _“Specify metric and conditions”_:
    - Click _“Select metric”_
    - Select _“Billing”_ > _“Total Estimated Charge”_ > Select your currency
    - Click _“Select metric”_
9. Under _“Conditions”_:
    - Define a threshold value
    - Click _“Next”_
10. Under _“Notification”_:
    - Here, we are specifying what action should take place when the alert is triggered
    - If you don’t have an existing SNS topic, select _“Create new topic”_, give it a name (e.g. `Billing-Alarm-Topic`) and set an email address
    - If this is a new SNS subscription, you will need to confirm the address after the alarm is created
    - Click _“Next”_
11. Under _“Add a description”_:
    - Give it a name (e.g. `Billing Alarm`)
    - Click _“Next”_
    - Review the details and click _“Create alarm”_

---
## References
