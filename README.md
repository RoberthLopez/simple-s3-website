# Simple S3 Website + GH Actions
This is a simple s3 website deployment for a static site hosted on AWS S3. Also its configured with Github actions for automated deployment.

## Setup Your S3 Bucket
### Create an AWS Bucket for your project.
Go to the S3 service in the AWS Management Console and click on Create Bucket 
Then select General purpose and choose a name for your bucket.

![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/1.png)

Deselect _Block all public access_ and then select _I acknowledge that the current settings might result in this bucket and the objects within becoming public_.

![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/2.png)

Click on Create Bucket.

### Configure Your Bucket

Click on your bucket name and go to the Properties tab. Then scroll down and click on the Edit button in the _Static website hosting_ section.
![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/3.png)


Choose Enable and especify the default page of your website, it could be index.html. Save Changes.
![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/4.png)


Go to the Permissions tab, scroll down to Bucket policy, click on Edit and add a bucket policy so anyone can access. Copy and paste this code and change YOUR BUCKET NAME for your bucket name and then click on Save.
```
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::YOUR BUCKET NAME/*"
        }
    ]
}
```
![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/5.png)


## Setup Github + Github Actions
### Configure an IAM User 
Go to IAM in the AWS Management Console and then select Users.
Click on Create user.
![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/6.png)


Name the user, it could be "gh-user" and click next. Select _Attach policies directly_ then in the Permissions policies type AmazonS3 and select _AmazonS3FullAccess_ premade policy and click next.

![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/7.png)


Review and click on Create user.

Click on User and choose the tab _Security credentials_, scroll down and click on Create access key in the Access key section.

![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/8.png)


Select Other and click Next.

Describe the purpose of the key (optional) and click Create access key.

Then Save the Access key and Secret access key in a secure place and click Done.

### Create a Github Repository

Login in Github and create a repo, you can follow this [tutorial](https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories).

### Set up Github Actions

Go to Settings > Secrets and variables > Actions and click in New repository secret.

Create two secrets, one called  AWS_ACCESS_KEY_ID where you will paste the Access Key and AWS_SECRET_ACESS_KEY where you will put the Secret access key.

![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/9.png)


Go to the Actions tab in the top bar of the repository.

Click on _Create new workflow_ and _set up a workflow yourself_.
![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/10.png)


Copy and this code 
```
name: Upload Website

on:
  push:
    branches:
    - main

jobs:
  deploy-site:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: jakejarvis/s3-sync-action@master
        with:
          args: --delete
        env:
          AWS_S3_BUCKET: YOUR BUCKET NAME
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          SOURCE_DIR: ./src
```

Change the AWS_S3_BUCKET env variable for your bucket name and click Commit changes.

![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/11.png)


### Create a simple static website
Go to your code editor and create a simple static website using html and push it to your github remote repository.

![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/12.png)



# Congratulations!
Now github actions should atomatically deploy your website to AWS S3 on every push to your repository.

![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/13.png)

![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/14.png)
