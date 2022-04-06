# Amazon S3

- Amazon Simple Storage Service (Amazon S3) is an object storage service that offers scalability, data availability, security and performance.
- Users can store and protect any amount of data for a range of use cases (data lakes, webistes, mobile apps, backkup and restore, archive, enterprise apps, IoT devices and big data analytics)
- Provides management features to help organize, optimize and configure access to your data.

## Storage Classese

- S3 offers a range of storage classes desing for different use cases.
- store data with changing or unknown access patterns in S3 Intelligent-Tiering, which optimizes storage cost by auto moving your data between four access tiers when your access patterns change.
  - include two low-latency access tiers optimized for frequent and infrequent access
  - two opt-in archive access tiers designed for asynchronous accesss for rarely accessed data.

## Storage management

- S3 has storage management featues that you can use to manage costs, meet regulatory requirements, reduce letency and save multiple distant copise of your data for compliance requirements.

- Lifecycle- config lifecycle policy to manage yoru objects and store them cost effectively throughout their lifecycle.
- Object Lock- prevent S3 objects from being deleted or overwritten for a fixed amount of time or indefinitely.
- Replication- replicate objects and their respective metadata and object tags to one or more destination buckets in the same or different AWS regions for reduced latency, security, compliance, etc.
- Batch Operations- manage billions of objects at scale with a single S3 API request or a few click in the Amazon S3 console. Use batch operations such a Copy, Invoke AWS lambda function and Restore on millions of objects.

## Access Management

- provides featues for auditing and managing access to your buckets and objects.
- S3 buckets and objects in them are set to default.
- Only have access to S3 resources that you create.
- Use the following featuers to modify this behavior:
  - S3 Block Public Access- block public access to S3 buckets and objects (turned on by default)
  - AWS Identify and Access Management (IAM) - create IAM users for your AWS account to manage acceses to your S3 resources. Use IAM to control the type of access a user or group of users has to an S3 bucket that your AWS account owns
  - Bucket policies - use IAM-based policy language to configure resource-based permissions for you S3 buckets and objects.
  - S3 Access points- config named network endpoints with dedicated access policies to manage data access at scale for shared dataset in S3.
  - Access control list (ACLs)- grant read and write permissions for individual buckets and object for authorized users.
  - S3 Object Ownership- disable ACLS and take ownership for every object in your bucket, simplifying accesss management for data stored in Amazon S3. Have full control over every object in yoru bucekt as the owner.
  - Access Analyzer for S3- evaluate and monitor your S3 buectks access policies, ensuring that the policies provide only the intended access to yoru S3 resources.

## Data processing

- S3 offers the following features to transfrom data and trigger workflows to automate a variety of other processing activities at scale.
  - S3 Object Lamda- add your own code to S3 GET requests to modify and process data asa it is returned to an appl. Filter rows, resize images, redact data and more.
  - Event notifications- trigger workflows that use Amazon Simple Notification Service (A SNS), Amazon Simple Queue Service (SQS) and AWS Lambda when a chage is made to your S3 resources.

## Storage logging and monitoring

- S3 provides logging and monitoring tools that you can use to monitor and control how your S2 resources are being used.

### Automated monitoring tools

- CloudWatch metrics- track the operational health of your S3 resources and config billing alearts when estimated charges reach a user-defined threshold.
- CloudTrail- record actions taken by a user, a role, or an AWS service. CT logs provide you with detailed API trackign for S3 bucket-level and object-level operations.

### Manual monitoring tools

- Server access loggin- get detailed record for the requests that are made to a bucket. Use for security and access audit, learn about customer base and understanding your S3 bill.
- AWS Trusted Advisor- identify ways to optimize your AWS infrastructure, improve security and performance, reduce cost and monitor service quotas.

## Buckets

- A bucket is a container for objects stored in S3. 
- Can store any number of objects in a bucket and can have up to 100 buckets in your account.
- Every object (file) is contained in a bucket.
- create a bucket by choosing a name and region where the bucket will reside- after you create the bucket, you cannot change its name or region.

## Objects

- fundamental entities stored in S3. 
- consist of object data and metadata.
- metadata is a set of name-value pairs that describe the object.
- object is uniquely identified within a bucket by a key(name) and a version ID.

## S3 Access Points

- are named network endpoints with dedicated access policies that describe how data can be access using that endpoint.
- APs are attached to buckets that you can use to perform S3 object operations, such as GetObject and PutObject.
- simplify managing data access at scale for shared datasets in S3.

## Access control list (ACLs)

- use ACLs to grant read and write permissions to authorized users for individual buckets and objects (predates AIM).
- each bucket has its own ACL.
- defines which AWS account or groups are granted access and the type of access.

## Region

- choose region where you want S3 to store the buckets you create.
- optimize latency, minimize cost or address regulatory requirements.
- objects stored in AWS Region never leave the Region unless you explicity transter or replicate them to another Region.

## S3 data consistency model

- provdes strong read-after-write consistency for PUT and DELETE requests of objects in your buckets in all AWS Regions.
- updates to a single key are atomic.
- S3 achieves high availability by replicating data across multiple server within AWS data centers.

## Accessing Amazon S3

- AWS Management Console- web-based user interface
- AWS Command Line Interface - use CLI to issue command or build scripts at your system's command line to perform AWS tasks.
- AWS SDKs- consits of libraries and sample code for various programming languages and platforms. Provides a convenient way to create programmatic acces to S3 and AWS since S3 is a REST service. 
- Amazon S3 REST API- designed to be programming language-neutral, using AWS-supported interfaces to store and retrieve objects. The REST API is an HTTP interface to Amazon S3, use standard HTTP requests to create, fetcfh and delete buckets and objects.

### Sources

[AWS](https://docs.aws.amazon.com/AmazonS3/latest/userguide/Welcome.html)