# highestpaidITjobsIndia
# AWS to Snowflake Data Pipeline  

This project demonstrates how to upload files to an AWS S3 bucket and interact with Snowflake for scalable data analytics.  

## Prerequisites  
1. **Install Required Tools**:  
   - Install [Visual Studio Code (VSCode)](https://code.visualstudio.com/).  
   - Install Python (3.x) on your system and ensure it's added to your PATH.  

2. **Libraries to Install**:  
   Run the following command to install required Python libraries:  
   ```bash  
   pip install boto3 
AWS IAM Configuration:

Log in to your AWS Management Console.
Create an IAM user with programmatic access and S3 permissions.
Replace your AWS IAM Access Key ID and Secret Access Key in the script after creating the user.
Configure trust policies to allow the necessary actions. Refer to the AWS Documentation for guidance.
S3 Bucket Setup:

Create an S3 bucket where files will be uploaded.
Ensure the bucket policy allows necessary actions for the IAM user.
Snowflake Account Setup:

Create a Snowflake account here.
Open the Snowflake SQL Worksheet from your Snowflake dashboard.
Running the Project
1. Upload to S3
Ensure your Python script uses the boto3 library for uploading files to the S3 bucket. Replace the placeholders for AWS keys and bucket name in the script with your actual values.

2. Configuring AWS Access Keys
Run the following command to configure AWS credentials locally:


aws configure  
Provide the Access Key ID, Secret Access Key, region, and output format when prompted.

3. Running Snowflake Code
Copy the provided Snowflake SQL code into the SQL Worksheet in your Snowflake console and execute it. This will set up your database, schema, and tables.

4. Reference Material
For additional guidance, watch this YouTube video tutorial:



Notes
Ensure your S3 bucket name and Snowflake configurations match those in the code.
This project uses AWS and Snowflake for demonstrating a modern cloud data pipeline.
