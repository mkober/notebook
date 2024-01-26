### Point-in-time recovery (PITR)
**Point-in-time recovery (PITR)** is a useful feature that can protect your DynamoDB tables from accidental write or delete operations. With this feature, you can eliminate the need for manual backups, scheduling, and maintenance.

![](https://media.tutorialsdojo.com/public/pitr-062023.png)

PITR allows you to create continuous backups of your table and restore it to any specific point in time within a retention period of up to 35 days. In the scenario, you can use PITR to achieve the recovery point objective of one hour by restoring the table to a state just before any corruption occurs.