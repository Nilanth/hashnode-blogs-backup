## Reduce AWS EC2 Development Instances Cost by 60%

We are all aware that Amazon Web Services is one of the most popular and used Cloud platforms. Most of us use AWS for hosting. When building apps, we might have different environments for development, staging, UAT, and production.

So if our app uses a web machine and a worker, then we have these same machines in all environments. For example, if we use a development and production environment, we will have 4 instances. But when compared to production instances, Our development environment will have low-end instances. But the low-end instance also adds cost to our billing.

We can reduce the development instance cost up to 60%. We can save this cost and use it in any other way. We will see how to cut down the cost.

The development environment instances are used only by the developers. So those instances are not required to run on Night-Time and Weekends. So we can down the instances on those times if your application dev team members are from the same timezone.

To make this change, AWS provides an Autoscaling group for each instance. Using Autoscaling groups, We can define scheduled calling using Cron. If you use Elastic Beanstack to launch your instances, Autoscaling groups are created by default. If you have launched your instances through the EC2 console, then you should create them manually. Check this [link](https://docs.aws.amazon.com/autoscaling/ec2/userguide/create-asg-from-instance.html) to create it manually.

## Steps to Configure Scheduled Scaling

1. Open the EC2 Autoscaling web console using this [link](https://console.aws.amazon.com/ec2autoscaling/).

2. Click the checkbox of the Autoscaling group to which you want to apply scheduled scaling from the list. A detailed view opens up from the bottom like the below image.
![1_jCxoSJxIQrm11NxSAsN7dw.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1632575684929/2HlFOM2as.png)
3. Now select the Automatic scaling tab from the detail view and choose **Create scheduled action** in the **Scheduled Actions** section, which open ups the below options
![1_d2LHuYoy0RW9UmiYQLGa0g.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1632575701001/6wxtXMS80.png)
4. Enter the name of the scheduled action. First, we create an action to stop the instance, So we can name it as Stop-Instance.

5. Next enter the **desired capacity** as **0**, **Min** as **0** and **Max** as **0**.

6. In Recurrence choose Cron and enter **`0 20 * * 1–5`** in the input next to Recurrence. This makes the instance stop at **8 PM** every day from Monday to Friday by scaling down the capacity to **0**.

7. To run the cron in your timezone, Choose your timezone. If required you can choose a start, the end time for this action and click **create**. 

Now we have configured to scale down the instance, Next to scale up the instance every day at 8 AM from Monday to Friday. Repeat the steps from 3.

8. Name the scheduled action as Start-Instance

9. Enter the **desired capacity** as **1**, **Min** as **1** and **Max** as **1**.

10. In Recurrence choose Cron and enter **`0 8 * * 1–5`** in the input next to Recurrence. This makes the instance start at **8 AM** every day from Monday to Friday by scaling up the capacity to **1**. 

11. Next, Choose the **timezone** and click **create**.

That all, Now our instance will run only on the weekdays from Monday to Friday and developers working hours. The created actions are listed below

![1_rbQz4mmIHp0waFF5L9LXng.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1632575725554/9fQQm0s_A.png)

> You can use [Crontab.guru](https://crontab.guru/) to create cron expression and you can also choose some examples from this [link](https://crontab.guru/examples.html)

Using this configuration we saved many running hour costs for a month and it surely will give us a good impact on our monthly bill. As our instance runs 12 hours per day and not runs on weekends.

---------
## Sample Cost Calculation

**September 2021**

* Total Days = 30 days
* Weekend Days = 8 Days
* Week Days = 22 Days

#### Considering our scheduled cron:

Total running hours: 12 hours per day * 22 days = 264 Hours

Cost for **t3.small** per hour is **$0.0208** (US East - Onhio)

#### Before Auto Scheduled Scaling Cost:

$0.0208 * 720Hours(24 Hours * 30 Days) = **$14.976**

#### After Auto Scheduled Scaling Cost:

$0.0208 * 264 Hours(12 Hours/Day * 22 Week Days) = **$5.4912**

**Cost Decrease Percentage = 63%**

---------

Based on the above sample cost calculation we have reduced **63%** per instance cost.

## Resources

1. https://aws.amazon.com/ec2/pricing/on-demand/
2. https://crontab.guru/
3. https://docs.aws.amazon.com/autoscaling/ec2/userguide/create-asg-from-instance.html

## Conclusion

This article addresses the steps to configure "Scheduled Auto Scaling" to reduce the AWS EC2 Development Environment instances cost. If your application nature suits serverless architecture, you can also try AWS [Lambda](https://aws.amazon.com/lambda/) or [Fargate](https://aws.amazon.com/fargate/) to reduce the cost. 

Thank you for reading.

Get more updates on [Twitter](https://twitter.com/Nilanth).