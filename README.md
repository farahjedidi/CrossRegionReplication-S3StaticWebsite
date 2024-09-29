# Demo: Cross-Region Replication of an S3 Static Website

In this demo, I will demonstrate how to set up Cross-Region Replication (CRR) for an S3 static website. The demo involves creating two S3 buckets in different regions, enabling static website hosting, configuring replication rules, and verifying the replication between buckets.

## Pre-Requisites
- **AWS Account Setup**: I used the **management account** from my AWS Organizations setup to complete this demo.
- **Required Files**: The website files inside `website1` and `website2` folders, used to create and update the static website in the source bucket.


## Steps

### 1. Create and Configure Two S3 Buckets
- I created two S3 buckets using the **management account**:
  - **Source bucket**: `sourcebucketfarah` located in **N. Virginia (us-east-1)**.
  - **Destination bucket**: `destinatonbucketfarah` located in **N. California (us-west-1)**.
- In the **Properties** section, I enabled **static website hosting** for both bucketset the **Index Document** and the **Error Document** to `index.html` 
- In the **Permissions** section, I added a **public access policy** for both buckets, allowing public access to the website content.
- ![Screenshot](https://imgur.com/rRHOCzC.png)

### 2. Configure Cross-Region Replication (CRR)
- I accessed the **Management** tab of the source bucket (`sourcebucketfarah`) and created a replication rule named `staticwebsiteDR`.
  - Enabled **Bucket Versioning** for both the source and destination buckets.
  - The replication rule was configured to replicate **all objects**.
  - ![Screenshot](https://imgur.com/AytGTUG.png)
  
  - I selected the destination bucket (`destinatonbucketfarah`) within the same account.
  - ![Screenshot](https://imgur.com/AlqCMOG.png)
    
  - Created a new role for S3 to replicate from the source bucket and write to the destination bucket.
- ![Screenshot](https://imgur.com/KuqYcQN.png)
- ![Screenshot](https://imgur.com/YZ7GDIS.png)
- ![Screenshot](https://imgur.com/sXc3sDU.png)

### 3. Upload Files for the Static Website
- I uploaded the website files from the `website1` folder into the source bucket (`sourcebucketfarah`).
- I accessed the static website from the **source bucket's URL** to verify that it was working correctly.
- ![Screenshot](https://imgur.com/0Gpu6mi.png)
- ![Screenshot](https://imgur.com/tSWzKFE.png)

### 4. Verify Replication in the Destination Bucket
- I navigated to the destination bucket (`destinationbucketfarah`) and verified that the objects were replicated.
- I opened the static website from the **destination bucket's URL**, and it worked perfectly.
- ![Screenshot](https://imgur.com/Rxc0yui.png)
- ![Screenshot](https://imgur.com/02WqXA4.png)

### 5. Test Replication with Updated Files
- I uploaded new files (with the same names as the ones from the `website1` folder) from the `website2` folder into the source bucket (`sourcebucketfarah`).
- The static website in the source bucket was updated, and I verified the changes.
- After a short delay, the same changes appeared in the static website of the destination bucket (`destinationbucketfarah`), confirming successful replication.
- ![Screenshot](https://imgur.com/YeEQup6.png)
- ![Screenshot](https://imgur.com/PrheU9o.png)

### 6. Cleanup
- I emptied both the source and destination buckets to avoid unnecessary costs.
- Deleted both buckets from S3.
- Removed the `s3crr_role_for_sourcebucketfarah` role from IAM.

## Conclusion
In this demo, I successfully set up Cross-Region Replication (CRR) between two S3 buckets (in the same account) : `sourcebucketfarah` and `destinationbucketfarah`. I configured static website hosting and demonstrated how changes made in the source bucket replicated to the destination bucket. This setup ensures disaster recovery for static websites on AWS from one region to another AWS region.
