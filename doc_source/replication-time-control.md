# Meeting compliance requirements using S3 Replication Time Control \(S3 RTC\)<a name="replication-time-control"></a>

S3 Replication Time Control \(S3 RTC\) helps you meet compliance or business requirements for data replication and provides visibility into Amazon S3 replication times\. S3 RTC replicates most objects that you upload to Amazon S3 in seconds, and 99\.99 percent of those objects within 15 minutes\. 

S3 RTC by default includes S3 Replication metrics and S3 event notifications, with which you can monitor the total number of S3 API operations that are pending replication, the total size of objects pending replication, and the maximum replication time\. Replication metrics can be enabled independently of S3 RTC, see [Monitoring progress with replication metrics](https://docs.aws.amazon.com/AmazonS3/latest/dev/replication-metrics.html)\. Additionally, S3 RTC provides `OperationMissedThreshold` and `OperationReplicatedAfterThreshold` events that notify the bucket owner if object replication exceeds or replicates after the 15\-minute threshold\. 

With S3 RTC, Amazon S3 events can notify you in the rare instance when objects do not replicate within 15 minutes and when those objects replicate successfully to their destination Region\. Amazon S3 events are available through Amazon SQS, Amazon SNS, or AWS Lambda\. For more information, see [Amazon S3 Event Notifications](NotificationHowTo.md)\.

**Topics**
+ [Enabling S3 Replication Time Control](#enabling-replication-time-control)
+ [Replication metrics with S3 RTC](#using-replication-metrics)
+ [Using Amazon S3 event notifications to track replication objects](#using-s3-events-to-track-rtc)
+ [Best practices and guidelines for S3 RTC](rtc-best-practices.md)

## Enabling S3 Replication Time Control<a name="enabling-replication-time-control"></a>

You can start using S3 Replication Time Control \(S3 RTC\) with a new or existing replication rule\. You can choose to apply your replication rule to an entire S3 bucket, or to Amazon S3 objects with a specific prefix or tag\. When you enable S3 RTC, replication metrics are also enabled on your replication rule\. 

If you are using the latest version of the replication configuration \(that is, you specify the `Filter` element in a replication configuration rule\), Amazon S3 does not replicate the delete marker by default\. However you can add delete marker replication to non\-tag\-based rules\.

**Note**  
 Replication metrics are billed at the same rate as Amazon CloudWatch custom metrics\. For information, see [Amazon CloudWatch pricing](https://aws.amazon.com/cloudwatch/pricing/)\. 

For more information about creating a rule with S3 RTC, see [Replicating objects with S3 Replication Time Control \(S3 RTC\)](replication-walkthrough-5.md)\.

## Replication metrics with S3 RTC<a name="using-replication-metrics"></a>

Replication rules with S3 Replication Time Control \(S3 RTC\) enabled publishes replication metrics\. With replication metrics, you can monitor the total number of S3 API operations that are pending replication, the total size of objects pending replication, and the maximum replication time to the destination Region\. You can then monitor each dataset that you replicate separately\.

Replication metrics are available within 15 minutes of enabling S3 RTC\. Replication metrics are available through the [Amazon S3 console](https://console.aws.amazon.com/s3/), the [Amazon S3 API](https://docs.aws.amazon.com/AmazonS3/latest/API/), the AWS SDKs, the [AWS Command Line Interface \(AWS CLI\)](https://docs.aws.amazon.com/cli/latest/reference/), and [Amazon CloudWatch](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/)\. For more information, see [Monitoring metrics with Amazon CloudWatch](cloudwatch-monitoring.md)\.

For more information about finding replication metrics via the Amazon S3 console, see [Viewing replication metrics using the Amazon S3 console](viewing-replication-metrics.md)\.

## Using Amazon S3 event notifications to track replication objects<a name="using-s3-events-to-track-rtc"></a>

You can track replication time for objects that did not replicate within 15 minutes by monitoring specific event notifications that S3 Replication Time Control \(S3 RTC\) publishes\. These events are published when an object that was eligible for replication using S3 RTC didn't replicate within 15 minutes, and when that object replicates to the destination Region\. 

Replication events are available within 15 minutes of enabling S3 RTC\. Amazon S3 events are available through Amazon SQS, Amazon SNS, or AWS Lambda\. For more information, see [Amazon S3 Event Notifications](NotificationHowTo.md)\.