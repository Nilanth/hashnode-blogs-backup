## How to Upgrade PostgreSQL in Amazon RDS

In this article, I will share how upgraded the PostgreSQL from 11.9 to 12.4 in AWS RDS.

Make sure that you thoroughly test after the upgrade in the testing environment to verify that your applications work correctly before applying the upgrade to your production DB instances. 

**Major version upgrades can contain database changes that are not backwards-compatible with existing applications.
**
## Checklist to follow before Major version upgrade

1. Take a Backup of the latest DB
2. If you are using a custom parameter group upgrade it to the latest version
3. Make sure that you have read release notes of the version you are going to upgrade

## Let's Start Upgrading

Steps to be followed are done in a testing environment, as I have created a new database using **Restore to point in time** from the existing testing DB, so others can use the application without downtime as the app is pointed to the testing DB.

1. Sign in to the AWS Console and open the RDS console at https://console.aws.amazon.com/rds/
2. Select the **DB identifier** which is to be upgraded in AWS RDS console and click **Modify**.
3. AWS will suggest the recommended upgrade PostgreSQL version for the current version, You can choose it from **DB engine version**.
4. Update the **DB instance identifier name**
5. Choose the **DB parameter group** from the **Additional configuration** section, by default it will be as **default.postgres12**, if you have a custom parameter group choose it.
6. Other details are auto-filled from the existing DB configuration.
7. Click **continue**, you will see the **Summary of modifications** verify the modification you have made.
8. Select **Apply immediately** from **Scheduling of modifications** and click **Modify DB instance**.


From here AWS will take care of the upgrade, based on DB size it will take some time to complete the upgrade. Once the upgrade is completed the status will be changed to **Available** in the RDS console. **But the upgraded database is not ready to use!!!**


After the Upgrade, if you connect the database to the app, you can see that some queries will take a long time and your app might become very very slow as compared to the previous performance, some APIs might fail due to query running for a long time! But we can fix these by doing the **After upgrade steps.**

## After Upgrade Steps

1. Run REINDEX, The [REINDEX](https://www.postgresql.org/docs/12/sql-reindex.html) command rebuilds one or more indices, replacing the previous version of the index.
> Recreate all indices in the database -> REINDEX DATABASE database_name
2. Once REINDEX is completed, Run ANALYZE.
[ANALYZE](https://www.postgresql.org/docs/12/sql-analyze.html) gathers statistics for the query planner to create the most efficient query execution paths. This command will help the planner to choose the most appropriate query plan, and thereby improve the speed of query processing.
> ANALYZE -> This will be run on available tables in the current schema that the user has access to.
3. Once the ANALYZE is completed, Upgrade your extensions. As PostgreSQL engine upgrade doesn’t upgrade most of the PostgreSQL extensions. Use the below command to upgrade your extensions.
> ALTER EXTENSION extension_name UPDATE TO ‘new_version’


## Issues

My application is hosted in Beanstalk (without a load balancer) was using SSL for connecting to the PostgreSQL DB instance, so it raised the following issue


```
SQLSTATE[08006] [7] SSL SYSCALL error: Connection reset by peer
```


After some hours of debugging, I found that the issue raised is due to **ssl_min_protocol_version** which is added in PostgreSQL 12 parameter group, by default it is set to **TLSv1.2**.

But the Apache HTTP Server used TLSv1 for connecting to PostgreSQL DB instance, so the connection was reset by peer due to a mismatch on TLS protocol, To fix this I created a custom parameter group and updated **ssl_min_protocol_version** to **TLSv1**. After this change, the connection issue was resolved!

Now we have upgraded to PostgreSQL 12 successfully.

Thank you for Reading.

Get more updates on [Twitter](https://twitter.com/Nilanth).