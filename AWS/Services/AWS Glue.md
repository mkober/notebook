**AWS Glue** is a fully managed ETL (extract, transform, and load) AWS service. One of its key abilities is to analyze and categorize data. You can use AWS Glue crawlers to automatically infer database and table schema from your data in Amazon S3 and store the associated metadata in the AWS Glue Data Catalog. Athena uses the AWS Glue Data Catalog to store and retrieve table metadata for the Amazon S3 data in your AWS account. The table metadata lets the Athena query engine know how to find, read, and process the data that you want to query.

![](https://media.tutorialsdojo.com/harmonize_glue_1.gif)

Finally, you can then visualize your Athena SQL queries in Amazon QuickSight, which lets you easily create and publish interactive BI dashboards by creating data sets.