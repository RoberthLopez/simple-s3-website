# Simple S3 Website + GH Actions
This is a simple s3 website deployment for a static site hosted on AWS S3. Also its configured with Github actions for automated deployment.

## Setup Your S3 Bucket
### Create an AWS Bucket for your project.
Go to the S3 service in the AWS Management Console and click on Create Bucket 
Then select General purpose and choose a name for your bucket.

![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/1.png?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEPr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJIMEYCIQCy%2B%2FSL0ghp2W0Tx8VqZCytZJBKWJ%2BxnHN89JPDCCkLQQIhAPHBeX5yZb1z3tdl6MjoA8myK5e8dpLpHXiO5t2C6%2FvWKvECCOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQBRoMMjA1NDU4MDU0OTcwIgxpiUE3ZvX6nFGnUxcqxQIrOgIpDa67E%2FDkIoOur37voNmRbfK1fU2hvWsZ2SXTbIQr%2BTQndhV9UjX9tMibNn8yuvB%2BFI9T9cMZt2OTvfVPb%2BVoRYdBA%2BPLnFd9LJ8pPHurdW4AIkT5QU1%2BX3YazcRB3mVUJzbeEnas45V%2BgkvtOmwpwSntqkFHvfTlf3nCZ3Jl0c%2BoyFcFQRJ7tO2xARXgpbkirl5R6JByTgFCmaZA%2B2HoMZ28XMx44SvzSEdwOcb9TnpvFJxTgLbtDkCe669vlSCEXfYSCM%2FYTlWG%2F6DSTSRIHLXVHNU4%2FwLUdZlDQKk3KNHhrjWsJon4hNn5%2FFP2OLEs%2B8Iq%2F1DUHbRGOI%2B2HZ5tydO%2B%2BLFyc2mawdk2NlAfxsHKTGYeKHYZJsKNmXap6KuwD%2FqLMY8lbOF1sFYLB1BUkbD9vz9WnDX1gg381vXNa8JnMN%2F5xbUGOrIC2sdf7DxirLf7pTUc5yu3Y3zfVVhZ2OqEDrvCLFlbAKmNUqQD5O87zo3BPm5xzO8%2FnT%2F2R7dp6jCb5vaRFBvftFb3mTPkJNWjaRQltasrypcBjt2gTI5Dwugz7%2FbgYSgMICNf6WngAqr9KAm9eZk2S%2BhdYTmP9x8y%2F%2FL1APEroLunW0iLnONYUR7Kuk%2FxJ9ruelct2j59RUXoFglf8HWdKB9sBguJqU6dFZM%2B1ZIlitGl8P%2FYDYc29Xe3V2YLnXId61I%2FDAMpdr11QnpFkb0T0td3AYBuagn%2BjNt9%2B7v6i2lE3xXsd9104Vwn0c9xXsOQ6N3c%2BeHjR9xvo8Nlmv46LsuSjFyc5lXrSI44qUE9hBbIpGOvu2sKSJJU4UkLWuc0S9cL5%2FRQVNgwbY6go%2BEouQzN&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240806T033957Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAS7VSBD45DIV7S66U%2F20240806%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=a72128bb4159faeb8b1936578901f3a1c9cab847bfdca5a20707ef161ee88789)

Deselect _Block all public access_ and then select _I acknowledge that the current settings might result in this bucket and the objects within becoming public_.

![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/2.png?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEPr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJIMEYCIQCy%2B%2FSL0ghp2W0Tx8VqZCytZJBKWJ%2BxnHN89JPDCCkLQQIhAPHBeX5yZb1z3tdl6MjoA8myK5e8dpLpHXiO5t2C6%2FvWKvECCOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQBRoMMjA1NDU4MDU0OTcwIgxpiUE3ZvX6nFGnUxcqxQIrOgIpDa67E%2FDkIoOur37voNmRbfK1fU2hvWsZ2SXTbIQr%2BTQndhV9UjX9tMibNn8yuvB%2BFI9T9cMZt2OTvfVPb%2BVoRYdBA%2BPLnFd9LJ8pPHurdW4AIkT5QU1%2BX3YazcRB3mVUJzbeEnas45V%2BgkvtOmwpwSntqkFHvfTlf3nCZ3Jl0c%2BoyFcFQRJ7tO2xARXgpbkirl5R6JByTgFCmaZA%2B2HoMZ28XMx44SvzSEdwOcb9TnpvFJxTgLbtDkCe669vlSCEXfYSCM%2FYTlWG%2F6DSTSRIHLXVHNU4%2FwLUdZlDQKk3KNHhrjWsJon4hNn5%2FFP2OLEs%2B8Iq%2F1DUHbRGOI%2B2HZ5tydO%2B%2BLFyc2mawdk2NlAfxsHKTGYeKHYZJsKNmXap6KuwD%2FqLMY8lbOF1sFYLB1BUkbD9vz9WnDX1gg381vXNa8JnMN%2F5xbUGOrIC2sdf7DxirLf7pTUc5yu3Y3zfVVhZ2OqEDrvCLFlbAKmNUqQD5O87zo3BPm5xzO8%2FnT%2F2R7dp6jCb5vaRFBvftFb3mTPkJNWjaRQltasrypcBjt2gTI5Dwugz7%2FbgYSgMICNf6WngAqr9KAm9eZk2S%2BhdYTmP9x8y%2F%2FL1APEroLunW0iLnONYUR7Kuk%2FxJ9ruelct2j59RUXoFglf8HWdKB9sBguJqU6dFZM%2B1ZIlitGl8P%2FYDYc29Xe3V2YLnXId61I%2FDAMpdr11QnpFkb0T0td3AYBuagn%2BjNt9%2B7v6i2lE3xXsd9104Vwn0c9xXsOQ6N3c%2BeHjR9xvo8Nlmv46LsuSjFyc5lXrSI44qUE9hBbIpGOvu2sKSJJU4UkLWuc0S9cL5%2FRQVNgwbY6go%2BEouQzN&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240806T034402Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAS7VSBD45DIV7S66U%2F20240806%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=5b8de9796d509f27a832e22626bda0478a9b19aa386d77324b7ad292133af393)

Click on Create Bucket.

### Configure Your Bucket

Click on your bucket name and go to the Properties tab. Then scroll down and click on the Edit button in the _Static website hosting_ section.
![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/3.png?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEPr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJIMEYCIQCy%2B%2FSL0ghp2W0Tx8VqZCytZJBKWJ%2BxnHN89JPDCCkLQQIhAPHBeX5yZb1z3tdl6MjoA8myK5e8dpLpHXiO5t2C6%2FvWKvECCOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQBRoMMjA1NDU4MDU0OTcwIgxpiUE3ZvX6nFGnUxcqxQIrOgIpDa67E%2FDkIoOur37voNmRbfK1fU2hvWsZ2SXTbIQr%2BTQndhV9UjX9tMibNn8yuvB%2BFI9T9cMZt2OTvfVPb%2BVoRYdBA%2BPLnFd9LJ8pPHurdW4AIkT5QU1%2BX3YazcRB3mVUJzbeEnas45V%2BgkvtOmwpwSntqkFHvfTlf3nCZ3Jl0c%2BoyFcFQRJ7tO2xARXgpbkirl5R6JByTgFCmaZA%2B2HoMZ28XMx44SvzSEdwOcb9TnpvFJxTgLbtDkCe669vlSCEXfYSCM%2FYTlWG%2F6DSTSRIHLXVHNU4%2FwLUdZlDQKk3KNHhrjWsJon4hNn5%2FFP2OLEs%2B8Iq%2F1DUHbRGOI%2B2HZ5tydO%2B%2BLFyc2mawdk2NlAfxsHKTGYeKHYZJsKNmXap6KuwD%2FqLMY8lbOF1sFYLB1BUkbD9vz9WnDX1gg381vXNa8JnMN%2F5xbUGOrIC2sdf7DxirLf7pTUc5yu3Y3zfVVhZ2OqEDrvCLFlbAKmNUqQD5O87zo3BPm5xzO8%2FnT%2F2R7dp6jCb5vaRFBvftFb3mTPkJNWjaRQltasrypcBjt2gTI5Dwugz7%2FbgYSgMICNf6WngAqr9KAm9eZk2S%2BhdYTmP9x8y%2F%2FL1APEroLunW0iLnONYUR7Kuk%2FxJ9ruelct2j59RUXoFglf8HWdKB9sBguJqU6dFZM%2B1ZIlitGl8P%2FYDYc29Xe3V2YLnXId61I%2FDAMpdr11QnpFkb0T0td3AYBuagn%2BjNt9%2B7v6i2lE3xXsd9104Vwn0c9xXsOQ6N3c%2BeHjR9xvo8Nlmv46LsuSjFyc5lXrSI44qUE9hBbIpGOvu2sKSJJU4UkLWuc0S9cL5%2FRQVNgwbY6go%2BEouQzN&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240806T034437Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAS7VSBD45DIV7S66U%2F20240806%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=35debe82dd1d85232e1a16f952250fd8138c24a6bc9baba032070caea53b9918)


Choose Enable and especify the default page of your website, it could be index.html. Save Changes.
![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/4.png?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEPr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJIMEYCIQCy%2B%2FSL0ghp2W0Tx8VqZCytZJBKWJ%2BxnHN89JPDCCkLQQIhAPHBeX5yZb1z3tdl6MjoA8myK5e8dpLpHXiO5t2C6%2FvWKvECCOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQBRoMMjA1NDU4MDU0OTcwIgxpiUE3ZvX6nFGnUxcqxQIrOgIpDa67E%2FDkIoOur37voNmRbfK1fU2hvWsZ2SXTbIQr%2BTQndhV9UjX9tMibNn8yuvB%2BFI9T9cMZt2OTvfVPb%2BVoRYdBA%2BPLnFd9LJ8pPHurdW4AIkT5QU1%2BX3YazcRB3mVUJzbeEnas45V%2BgkvtOmwpwSntqkFHvfTlf3nCZ3Jl0c%2BoyFcFQRJ7tO2xARXgpbkirl5R6JByTgFCmaZA%2B2HoMZ28XMx44SvzSEdwOcb9TnpvFJxTgLbtDkCe669vlSCEXfYSCM%2FYTlWG%2F6DSTSRIHLXVHNU4%2FwLUdZlDQKk3KNHhrjWsJon4hNn5%2FFP2OLEs%2B8Iq%2F1DUHbRGOI%2B2HZ5tydO%2B%2BLFyc2mawdk2NlAfxsHKTGYeKHYZJsKNmXap6KuwD%2FqLMY8lbOF1sFYLB1BUkbD9vz9WnDX1gg381vXNa8JnMN%2F5xbUGOrIC2sdf7DxirLf7pTUc5yu3Y3zfVVhZ2OqEDrvCLFlbAKmNUqQD5O87zo3BPm5xzO8%2FnT%2F2R7dp6jCb5vaRFBvftFb3mTPkJNWjaRQltasrypcBjt2gTI5Dwugz7%2FbgYSgMICNf6WngAqr9KAm9eZk2S%2BhdYTmP9x8y%2F%2FL1APEroLunW0iLnONYUR7Kuk%2FxJ9ruelct2j59RUXoFglf8HWdKB9sBguJqU6dFZM%2B1ZIlitGl8P%2FYDYc29Xe3V2YLnXId61I%2FDAMpdr11QnpFkb0T0td3AYBuagn%2BjNt9%2B7v6i2lE3xXsd9104Vwn0c9xXsOQ6N3c%2BeHjR9xvo8Nlmv46LsuSjFyc5lXrSI44qUE9hBbIpGOvu2sKSJJU4UkLWuc0S9cL5%2FRQVNgwbY6go%2BEouQzN&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240806T034559Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAS7VSBD45DIV7S66U%2F20240806%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=901e5b27e6728d81803d4dd057750b67b6bdbb25a418e9641c88612ac94c243d)


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
![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/5.png?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEPr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJIMEYCIQCy%2B%2FSL0ghp2W0Tx8VqZCytZJBKWJ%2BxnHN89JPDCCkLQQIhAPHBeX5yZb1z3tdl6MjoA8myK5e8dpLpHXiO5t2C6%2FvWKvECCOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQBRoMMjA1NDU4MDU0OTcwIgxpiUE3ZvX6nFGnUxcqxQIrOgIpDa67E%2FDkIoOur37voNmRbfK1fU2hvWsZ2SXTbIQr%2BTQndhV9UjX9tMibNn8yuvB%2BFI9T9cMZt2OTvfVPb%2BVoRYdBA%2BPLnFd9LJ8pPHurdW4AIkT5QU1%2BX3YazcRB3mVUJzbeEnas45V%2BgkvtOmwpwSntqkFHvfTlf3nCZ3Jl0c%2BoyFcFQRJ7tO2xARXgpbkirl5R6JByTgFCmaZA%2B2HoMZ28XMx44SvzSEdwOcb9TnpvFJxTgLbtDkCe669vlSCEXfYSCM%2FYTlWG%2F6DSTSRIHLXVHNU4%2FwLUdZlDQKk3KNHhrjWsJon4hNn5%2FFP2OLEs%2B8Iq%2F1DUHbRGOI%2B2HZ5tydO%2B%2BLFyc2mawdk2NlAfxsHKTGYeKHYZJsKNmXap6KuwD%2FqLMY8lbOF1sFYLB1BUkbD9vz9WnDX1gg381vXNa8JnMN%2F5xbUGOrIC2sdf7DxirLf7pTUc5yu3Y3zfVVhZ2OqEDrvCLFlbAKmNUqQD5O87zo3BPm5xzO8%2FnT%2F2R7dp6jCb5vaRFBvftFb3mTPkJNWjaRQltasrypcBjt2gTI5Dwugz7%2FbgYSgMICNf6WngAqr9KAm9eZk2S%2BhdYTmP9x8y%2F%2FL1APEroLunW0iLnONYUR7Kuk%2FxJ9ruelct2j59RUXoFglf8HWdKB9sBguJqU6dFZM%2B1ZIlitGl8P%2FYDYc29Xe3V2YLnXId61I%2FDAMpdr11QnpFkb0T0td3AYBuagn%2BjNt9%2B7v6i2lE3xXsd9104Vwn0c9xXsOQ6N3c%2BeHjR9xvo8Nlmv46LsuSjFyc5lXrSI44qUE9hBbIpGOvu2sKSJJU4UkLWuc0S9cL5%2FRQVNgwbY6go%2BEouQzN&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240806T034633Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAS7VSBD45DIV7S66U%2F20240806%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=7bbeee4c55affe74d3b4beb2056e008bb5c661494cda88899b2f3ace4d3ccc6d)


## Setup Github + Github Actions
### Configure an IAM User 
Go to IAM in the AWS Management Console and then select Users.
Click on Create user.
![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/6.png?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEPr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJIMEYCIQCy%2B%2FSL0ghp2W0Tx8VqZCytZJBKWJ%2BxnHN89JPDCCkLQQIhAPHBeX5yZb1z3tdl6MjoA8myK5e8dpLpHXiO5t2C6%2FvWKvECCOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQBRoMMjA1NDU4MDU0OTcwIgxpiUE3ZvX6nFGnUxcqxQIrOgIpDa67E%2FDkIoOur37voNmRbfK1fU2hvWsZ2SXTbIQr%2BTQndhV9UjX9tMibNn8yuvB%2BFI9T9cMZt2OTvfVPb%2BVoRYdBA%2BPLnFd9LJ8pPHurdW4AIkT5QU1%2BX3YazcRB3mVUJzbeEnas45V%2BgkvtOmwpwSntqkFHvfTlf3nCZ3Jl0c%2BoyFcFQRJ7tO2xARXgpbkirl5R6JByTgFCmaZA%2B2HoMZ28XMx44SvzSEdwOcb9TnpvFJxTgLbtDkCe669vlSCEXfYSCM%2FYTlWG%2F6DSTSRIHLXVHNU4%2FwLUdZlDQKk3KNHhrjWsJon4hNn5%2FFP2OLEs%2B8Iq%2F1DUHbRGOI%2B2HZ5tydO%2B%2BLFyc2mawdk2NlAfxsHKTGYeKHYZJsKNmXap6KuwD%2FqLMY8lbOF1sFYLB1BUkbD9vz9WnDX1gg381vXNa8JnMN%2F5xbUGOrIC2sdf7DxirLf7pTUc5yu3Y3zfVVhZ2OqEDrvCLFlbAKmNUqQD5O87zo3BPm5xzO8%2FnT%2F2R7dp6jCb5vaRFBvftFb3mTPkJNWjaRQltasrypcBjt2gTI5Dwugz7%2FbgYSgMICNf6WngAqr9KAm9eZk2S%2BhdYTmP9x8y%2F%2FL1APEroLunW0iLnONYUR7Kuk%2FxJ9ruelct2j59RUXoFglf8HWdKB9sBguJqU6dFZM%2B1ZIlitGl8P%2FYDYc29Xe3V2YLnXId61I%2FDAMpdr11QnpFkb0T0td3AYBuagn%2BjNt9%2B7v6i2lE3xXsd9104Vwn0c9xXsOQ6N3c%2BeHjR9xvo8Nlmv46LsuSjFyc5lXrSI44qUE9hBbIpGOvu2sKSJJU4UkLWuc0S9cL5%2FRQVNgwbY6go%2BEouQzN&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240806T034709Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAS7VSBD45DIV7S66U%2F20240806%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=5047d1aef6cdf84ab7471230b9a189c6e7bb4c13f94fc7cd2ec94f3f92fdbe03)


Name the user, it could be "gh-user" and click next. Select _Attach policies directly_ then in the Permissions policies type AmazonS3 and select _AmazonS3FullAccess_ premade policy and click next.

![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/7.png?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEPr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJIMEYCIQCy%2B%2FSL0ghp2W0Tx8VqZCytZJBKWJ%2BxnHN89JPDCCkLQQIhAPHBeX5yZb1z3tdl6MjoA8myK5e8dpLpHXiO5t2C6%2FvWKvECCOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQBRoMMjA1NDU4MDU0OTcwIgxpiUE3ZvX6nFGnUxcqxQIrOgIpDa67E%2FDkIoOur37voNmRbfK1fU2hvWsZ2SXTbIQr%2BTQndhV9UjX9tMibNn8yuvB%2BFI9T9cMZt2OTvfVPb%2BVoRYdBA%2BPLnFd9LJ8pPHurdW4AIkT5QU1%2BX3YazcRB3mVUJzbeEnas45V%2BgkvtOmwpwSntqkFHvfTlf3nCZ3Jl0c%2BoyFcFQRJ7tO2xARXgpbkirl5R6JByTgFCmaZA%2B2HoMZ28XMx44SvzSEdwOcb9TnpvFJxTgLbtDkCe669vlSCEXfYSCM%2FYTlWG%2F6DSTSRIHLXVHNU4%2FwLUdZlDQKk3KNHhrjWsJon4hNn5%2FFP2OLEs%2B8Iq%2F1DUHbRGOI%2B2HZ5tydO%2B%2BLFyc2mawdk2NlAfxsHKTGYeKHYZJsKNmXap6KuwD%2FqLMY8lbOF1sFYLB1BUkbD9vz9WnDX1gg381vXNa8JnMN%2F5xbUGOrIC2sdf7DxirLf7pTUc5yu3Y3zfVVhZ2OqEDrvCLFlbAKmNUqQD5O87zo3BPm5xzO8%2FnT%2F2R7dp6jCb5vaRFBvftFb3mTPkJNWjaRQltasrypcBjt2gTI5Dwugz7%2FbgYSgMICNf6WngAqr9KAm9eZk2S%2BhdYTmP9x8y%2F%2FL1APEroLunW0iLnONYUR7Kuk%2FxJ9ruelct2j59RUXoFglf8HWdKB9sBguJqU6dFZM%2B1ZIlitGl8P%2FYDYc29Xe3V2YLnXId61I%2FDAMpdr11QnpFkb0T0td3AYBuagn%2BjNt9%2B7v6i2lE3xXsd9104Vwn0c9xXsOQ6N3c%2BeHjR9xvo8Nlmv46LsuSjFyc5lXrSI44qUE9hBbIpGOvu2sKSJJU4UkLWuc0S9cL5%2FRQVNgwbY6go%2BEouQzN&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240806T034740Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAS7VSBD45DIV7S66U%2F20240806%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=7d2fdcf82bce3ce1c21811d13d73423bd2e9aac2c4550da4b0a757568de8ee8b)


Review and click on Create user.

Click on User and choose the tab _Security credentials_, scroll down and click on Create access key in the Access key section.

![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/8.png?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEPr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJIMEYCIQCy%2B%2FSL0ghp2W0Tx8VqZCytZJBKWJ%2BxnHN89JPDCCkLQQIhAPHBeX5yZb1z3tdl6MjoA8myK5e8dpLpHXiO5t2C6%2FvWKvECCOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQBRoMMjA1NDU4MDU0OTcwIgxpiUE3ZvX6nFGnUxcqxQIrOgIpDa67E%2FDkIoOur37voNmRbfK1fU2hvWsZ2SXTbIQr%2BTQndhV9UjX9tMibNn8yuvB%2BFI9T9cMZt2OTvfVPb%2BVoRYdBA%2BPLnFd9LJ8pPHurdW4AIkT5QU1%2BX3YazcRB3mVUJzbeEnas45V%2BgkvtOmwpwSntqkFHvfTlf3nCZ3Jl0c%2BoyFcFQRJ7tO2xARXgpbkirl5R6JByTgFCmaZA%2B2HoMZ28XMx44SvzSEdwOcb9TnpvFJxTgLbtDkCe669vlSCEXfYSCM%2FYTlWG%2F6DSTSRIHLXVHNU4%2FwLUdZlDQKk3KNHhrjWsJon4hNn5%2FFP2OLEs%2B8Iq%2F1DUHbRGOI%2B2HZ5tydO%2B%2BLFyc2mawdk2NlAfxsHKTGYeKHYZJsKNmXap6KuwD%2FqLMY8lbOF1sFYLB1BUkbD9vz9WnDX1gg381vXNa8JnMN%2F5xbUGOrIC2sdf7DxirLf7pTUc5yu3Y3zfVVhZ2OqEDrvCLFlbAKmNUqQD5O87zo3BPm5xzO8%2FnT%2F2R7dp6jCb5vaRFBvftFb3mTPkJNWjaRQltasrypcBjt2gTI5Dwugz7%2FbgYSgMICNf6WngAqr9KAm9eZk2S%2BhdYTmP9x8y%2F%2FL1APEroLunW0iLnONYUR7Kuk%2FxJ9ruelct2j59RUXoFglf8HWdKB9sBguJqU6dFZM%2B1ZIlitGl8P%2FYDYc29Xe3V2YLnXId61I%2FDAMpdr11QnpFkb0T0td3AYBuagn%2BjNt9%2B7v6i2lE3xXsd9104Vwn0c9xXsOQ6N3c%2BeHjR9xvo8Nlmv46LsuSjFyc5lXrSI44qUE9hBbIpGOvu2sKSJJU4UkLWuc0S9cL5%2FRQVNgwbY6go%2BEouQzN&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240806T034812Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAS7VSBD45DIV7S66U%2F20240806%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=5900f9d62241aae892548994483f17ffe410e3ab6078aecad05b3de6fc8677d4)


Select Other and click Next.

Describe the purpose of the key (optional) and click Create access key.

Then Save the Access key and Secret access key in a secure place and click Done.

### Create a Github Repository

Login in Github and create a repo, you can follow this [tutorial](https://docs.github.com/en/repositories/creating-and-managing-repositories/quickstart-for-repositories).

### Set up Github Actions

Go to Settings > Secrets and variables > Actions and click in New repository secret.

Create two secrets, one called  AWS_ACCESS_KEY_ID where you will paste the Access Key and AWS_SECRET_ACESS_KEY where you will put the Secret access key.

![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/9.png?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEPr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJIMEYCIQCy%2B%2FSL0ghp2W0Tx8VqZCytZJBKWJ%2BxnHN89JPDCCkLQQIhAPHBeX5yZb1z3tdl6MjoA8myK5e8dpLpHXiO5t2C6%2FvWKvECCOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQBRoMMjA1NDU4MDU0OTcwIgxpiUE3ZvX6nFGnUxcqxQIrOgIpDa67E%2FDkIoOur37voNmRbfK1fU2hvWsZ2SXTbIQr%2BTQndhV9UjX9tMibNn8yuvB%2BFI9T9cMZt2OTvfVPb%2BVoRYdBA%2BPLnFd9LJ8pPHurdW4AIkT5QU1%2BX3YazcRB3mVUJzbeEnas45V%2BgkvtOmwpwSntqkFHvfTlf3nCZ3Jl0c%2BoyFcFQRJ7tO2xARXgpbkirl5R6JByTgFCmaZA%2B2HoMZ28XMx44SvzSEdwOcb9TnpvFJxTgLbtDkCe669vlSCEXfYSCM%2FYTlWG%2F6DSTSRIHLXVHNU4%2FwLUdZlDQKk3KNHhrjWsJon4hNn5%2FFP2OLEs%2B8Iq%2F1DUHbRGOI%2B2HZ5tydO%2B%2BLFyc2mawdk2NlAfxsHKTGYeKHYZJsKNmXap6KuwD%2FqLMY8lbOF1sFYLB1BUkbD9vz9WnDX1gg381vXNa8JnMN%2F5xbUGOrIC2sdf7DxirLf7pTUc5yu3Y3zfVVhZ2OqEDrvCLFlbAKmNUqQD5O87zo3BPm5xzO8%2FnT%2F2R7dp6jCb5vaRFBvftFb3mTPkJNWjaRQltasrypcBjt2gTI5Dwugz7%2FbgYSgMICNf6WngAqr9KAm9eZk2S%2BhdYTmP9x8y%2F%2FL1APEroLunW0iLnONYUR7Kuk%2FxJ9ruelct2j59RUXoFglf8HWdKB9sBguJqU6dFZM%2B1ZIlitGl8P%2FYDYc29Xe3V2YLnXId61I%2FDAMpdr11QnpFkb0T0td3AYBuagn%2BjNt9%2B7v6i2lE3xXsd9104Vwn0c9xXsOQ6N3c%2BeHjR9xvo8Nlmv46LsuSjFyc5lXrSI44qUE9hBbIpGOvu2sKSJJU4UkLWuc0S9cL5%2FRQVNgwbY6go%2BEouQzN&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240806T035215Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAS7VSBD45DIV7S66U%2F20240806%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=38213a013e2601b12a77e94676da28015c2971656d9fc2ad09edd6a6a5866600)


Go to the Actions tab in the top bar of the repository.

Click on _Create new workflow_ and _set up a workflow yourself_.
![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/10.png?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEPr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJIMEYCIQCy%2B%2FSL0ghp2W0Tx8VqZCytZJBKWJ%2BxnHN89JPDCCkLQQIhAPHBeX5yZb1z3tdl6MjoA8myK5e8dpLpHXiO5t2C6%2FvWKvECCOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQBRoMMjA1NDU4MDU0OTcwIgxpiUE3ZvX6nFGnUxcqxQIrOgIpDa67E%2FDkIoOur37voNmRbfK1fU2hvWsZ2SXTbIQr%2BTQndhV9UjX9tMibNn8yuvB%2BFI9T9cMZt2OTvfVPb%2BVoRYdBA%2BPLnFd9LJ8pPHurdW4AIkT5QU1%2BX3YazcRB3mVUJzbeEnas45V%2BgkvtOmwpwSntqkFHvfTlf3nCZ3Jl0c%2BoyFcFQRJ7tO2xARXgpbkirl5R6JByTgFCmaZA%2B2HoMZ28XMx44SvzSEdwOcb9TnpvFJxTgLbtDkCe669vlSCEXfYSCM%2FYTlWG%2F6DSTSRIHLXVHNU4%2FwLUdZlDQKk3KNHhrjWsJon4hNn5%2FFP2OLEs%2B8Iq%2F1DUHbRGOI%2B2HZ5tydO%2B%2BLFyc2mawdk2NlAfxsHKTGYeKHYZJsKNmXap6KuwD%2FqLMY8lbOF1sFYLB1BUkbD9vz9WnDX1gg381vXNa8JnMN%2F5xbUGOrIC2sdf7DxirLf7pTUc5yu3Y3zfVVhZ2OqEDrvCLFlbAKmNUqQD5O87zo3BPm5xzO8%2FnT%2F2R7dp6jCb5vaRFBvftFb3mTPkJNWjaRQltasrypcBjt2gTI5Dwugz7%2FbgYSgMICNf6WngAqr9KAm9eZk2S%2BhdYTmP9x8y%2F%2FL1APEroLunW0iLnONYUR7Kuk%2FxJ9ruelct2j59RUXoFglf8HWdKB9sBguJqU6dFZM%2B1ZIlitGl8P%2FYDYc29Xe3V2YLnXId61I%2FDAMpdr11QnpFkb0T0td3AYBuagn%2BjNt9%2B7v6i2lE3xXsd9104Vwn0c9xXsOQ6N3c%2BeHjR9xvo8Nlmv46LsuSjFyc5lXrSI44qUE9hBbIpGOvu2sKSJJU4UkLWuc0S9cL5%2FRQVNgwbY6go%2BEouQzN&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240806T035250Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAS7VSBD45DIV7S66U%2F20240806%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=caf2294d352583ce4437eb054c4b6f36642deb3292988fa38f681dbeb6da3d13)


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

![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/11.png?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEPr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJIMEYCIQCy%2B%2FSL0ghp2W0Tx8VqZCytZJBKWJ%2BxnHN89JPDCCkLQQIhAPHBeX5yZb1z3tdl6MjoA8myK5e8dpLpHXiO5t2C6%2FvWKvECCOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQBRoMMjA1NDU4MDU0OTcwIgxpiUE3ZvX6nFGnUxcqxQIrOgIpDa67E%2FDkIoOur37voNmRbfK1fU2hvWsZ2SXTbIQr%2BTQndhV9UjX9tMibNn8yuvB%2BFI9T9cMZt2OTvfVPb%2BVoRYdBA%2BPLnFd9LJ8pPHurdW4AIkT5QU1%2BX3YazcRB3mVUJzbeEnas45V%2BgkvtOmwpwSntqkFHvfTlf3nCZ3Jl0c%2BoyFcFQRJ7tO2xARXgpbkirl5R6JByTgFCmaZA%2B2HoMZ28XMx44SvzSEdwOcb9TnpvFJxTgLbtDkCe669vlSCEXfYSCM%2FYTlWG%2F6DSTSRIHLXVHNU4%2FwLUdZlDQKk3KNHhrjWsJon4hNn5%2FFP2OLEs%2B8Iq%2F1DUHbRGOI%2B2HZ5tydO%2B%2BLFyc2mawdk2NlAfxsHKTGYeKHYZJsKNmXap6KuwD%2FqLMY8lbOF1sFYLB1BUkbD9vz9WnDX1gg381vXNa8JnMN%2F5xbUGOrIC2sdf7DxirLf7pTUc5yu3Y3zfVVhZ2OqEDrvCLFlbAKmNUqQD5O87zo3BPm5xzO8%2FnT%2F2R7dp6jCb5vaRFBvftFb3mTPkJNWjaRQltasrypcBjt2gTI5Dwugz7%2FbgYSgMICNf6WngAqr9KAm9eZk2S%2BhdYTmP9x8y%2F%2FL1APEroLunW0iLnONYUR7Kuk%2FxJ9ruelct2j59RUXoFglf8HWdKB9sBguJqU6dFZM%2B1ZIlitGl8P%2FYDYc29Xe3V2YLnXId61I%2FDAMpdr11QnpFkb0T0td3AYBuagn%2BjNt9%2B7v6i2lE3xXsd9104Vwn0c9xXsOQ6N3c%2BeHjR9xvo8Nlmv46LsuSjFyc5lXrSI44qUE9hBbIpGOvu2sKSJJU4UkLWuc0S9cL5%2FRQVNgwbY6go%2BEouQzN&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240806T035316Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAS7VSBD45DIV7S66U%2F20240806%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=0ecb2b19f51374d6cdd4acacfcfc37a00eab304be2f06114c92247553082fd2f)


### Create a simple static website
Go to your code editor and create a simple static website using html and push it to your github remote repository.

![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/12.png?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEPr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJIMEYCIQCy%2B%2FSL0ghp2W0Tx8VqZCytZJBKWJ%2BxnHN89JPDCCkLQQIhAPHBeX5yZb1z3tdl6MjoA8myK5e8dpLpHXiO5t2C6%2FvWKvECCOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQBRoMMjA1NDU4MDU0OTcwIgxpiUE3ZvX6nFGnUxcqxQIrOgIpDa67E%2FDkIoOur37voNmRbfK1fU2hvWsZ2SXTbIQr%2BTQndhV9UjX9tMibNn8yuvB%2BFI9T9cMZt2OTvfVPb%2BVoRYdBA%2BPLnFd9LJ8pPHurdW4AIkT5QU1%2BX3YazcRB3mVUJzbeEnas45V%2BgkvtOmwpwSntqkFHvfTlf3nCZ3Jl0c%2BoyFcFQRJ7tO2xARXgpbkirl5R6JByTgFCmaZA%2B2HoMZ28XMx44SvzSEdwOcb9TnpvFJxTgLbtDkCe669vlSCEXfYSCM%2FYTlWG%2F6DSTSRIHLXVHNU4%2FwLUdZlDQKk3KNHhrjWsJon4hNn5%2FFP2OLEs%2B8Iq%2F1DUHbRGOI%2B2HZ5tydO%2B%2BLFyc2mawdk2NlAfxsHKTGYeKHYZJsKNmXap6KuwD%2FqLMY8lbOF1sFYLB1BUkbD9vz9WnDX1gg381vXNa8JnMN%2F5xbUGOrIC2sdf7DxirLf7pTUc5yu3Y3zfVVhZ2OqEDrvCLFlbAKmNUqQD5O87zo3BPm5xzO8%2FnT%2F2R7dp6jCb5vaRFBvftFb3mTPkJNWjaRQltasrypcBjt2gTI5Dwugz7%2FbgYSgMICNf6WngAqr9KAm9eZk2S%2BhdYTmP9x8y%2F%2FL1APEroLunW0iLnONYUR7Kuk%2FxJ9ruelct2j59RUXoFglf8HWdKB9sBguJqU6dFZM%2B1ZIlitGl8P%2FYDYc29Xe3V2YLnXId61I%2FDAMpdr11QnpFkb0T0td3AYBuagn%2BjNt9%2B7v6i2lE3xXsd9104Vwn0c9xXsOQ6N3c%2BeHjR9xvo8Nlmv46LsuSjFyc5lXrSI44qUE9hBbIpGOvu2sKSJJU4UkLWuc0S9cL5%2FRQVNgwbY6go%2BEouQzN&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240806T035347Z&X-Amz-SignedHeaders=host&X-Amz-Expires=299&X-Amz-Credential=ASIAS7VSBD45DIV7S66U%2F20240806%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=e7f597915effed50feb2ae328899861c65af347882902369ca030ee7539851d6)



# Congratulations!
Now github actions should atomatically deploy your website to AWS S3 on every push to your repository.

![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/13.png?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEPr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJIMEYCIQCy%2B%2FSL0ghp2W0Tx8VqZCytZJBKWJ%2BxnHN89JPDCCkLQQIhAPHBeX5yZb1z3tdl6MjoA8myK5e8dpLpHXiO5t2C6%2FvWKvECCOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQBRoMMjA1NDU4MDU0OTcwIgxpiUE3ZvX6nFGnUxcqxQIrOgIpDa67E%2FDkIoOur37voNmRbfK1fU2hvWsZ2SXTbIQr%2BTQndhV9UjX9tMibNn8yuvB%2BFI9T9cMZt2OTvfVPb%2BVoRYdBA%2BPLnFd9LJ8pPHurdW4AIkT5QU1%2BX3YazcRB3mVUJzbeEnas45V%2BgkvtOmwpwSntqkFHvfTlf3nCZ3Jl0c%2BoyFcFQRJ7tO2xARXgpbkirl5R6JByTgFCmaZA%2B2HoMZ28XMx44SvzSEdwOcb9TnpvFJxTgLbtDkCe669vlSCEXfYSCM%2FYTlWG%2F6DSTSRIHLXVHNU4%2FwLUdZlDQKk3KNHhrjWsJon4hNn5%2FFP2OLEs%2B8Iq%2F1DUHbRGOI%2B2HZ5tydO%2B%2BLFyc2mawdk2NlAfxsHKTGYeKHYZJsKNmXap6KuwD%2FqLMY8lbOF1sFYLB1BUkbD9vz9WnDX1gg381vXNa8JnMN%2F5xbUGOrIC2sdf7DxirLf7pTUc5yu3Y3zfVVhZ2OqEDrvCLFlbAKmNUqQD5O87zo3BPm5xzO8%2FnT%2F2R7dp6jCb5vaRFBvftFb3mTPkJNWjaRQltasrypcBjt2gTI5Dwugz7%2FbgYSgMICNf6WngAqr9KAm9eZk2S%2BhdYTmP9x8y%2F%2FL1APEroLunW0iLnONYUR7Kuk%2FxJ9ruelct2j59RUXoFglf8HWdKB9sBguJqU6dFZM%2B1ZIlitGl8P%2FYDYc29Xe3V2YLnXId61I%2FDAMpdr11QnpFkb0T0td3AYBuagn%2BjNt9%2B7v6i2lE3xXsd9104Vwn0c9xXsOQ6N3c%2BeHjR9xvo8Nlmv46LsuSjFyc5lXrSI44qUE9hBbIpGOvu2sKSJJU4UkLWuc0S9cL5%2FRQVNgwbY6go%2BEouQzN&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240806T035413Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAS7VSBD45DIV7S66U%2F20240806%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=bb4b60902919ef888ac1f709f22f0e50850af15653e12d2bee7b23481f020ee6)

![image](https://s3.us-east-1.amazonaws.com/simple-web-s3.com/images/14.png?response-content-disposition=inline&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEPr%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJIMEYCIQCy%2B%2FSL0ghp2W0Tx8VqZCytZJBKWJ%2BxnHN89JPDCCkLQQIhAPHBeX5yZb1z3tdl6MjoA8myK5e8dpLpHXiO5t2C6%2FvWKvECCOP%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQBRoMMjA1NDU4MDU0OTcwIgxpiUE3ZvX6nFGnUxcqxQIrOgIpDa67E%2FDkIoOur37voNmRbfK1fU2hvWsZ2SXTbIQr%2BTQndhV9UjX9tMibNn8yuvB%2BFI9T9cMZt2OTvfVPb%2BVoRYdBA%2BPLnFd9LJ8pPHurdW4AIkT5QU1%2BX3YazcRB3mVUJzbeEnas45V%2BgkvtOmwpwSntqkFHvfTlf3nCZ3Jl0c%2BoyFcFQRJ7tO2xARXgpbkirl5R6JByTgFCmaZA%2B2HoMZ28XMx44SvzSEdwOcb9TnpvFJxTgLbtDkCe669vlSCEXfYSCM%2FYTlWG%2F6DSTSRIHLXVHNU4%2FwLUdZlDQKk3KNHhrjWsJon4hNn5%2FFP2OLEs%2B8Iq%2F1DUHbRGOI%2B2HZ5tydO%2B%2BLFyc2mawdk2NlAfxsHKTGYeKHYZJsKNmXap6KuwD%2FqLMY8lbOF1sFYLB1BUkbD9vz9WnDX1gg381vXNa8JnMN%2F5xbUGOrIC2sdf7DxirLf7pTUc5yu3Y3zfVVhZ2OqEDrvCLFlbAKmNUqQD5O87zo3BPm5xzO8%2FnT%2F2R7dp6jCb5vaRFBvftFb3mTPkJNWjaRQltasrypcBjt2gTI5Dwugz7%2FbgYSgMICNf6WngAqr9KAm9eZk2S%2BhdYTmP9x8y%2F%2FL1APEroLunW0iLnONYUR7Kuk%2FxJ9ruelct2j59RUXoFglf8HWdKB9sBguJqU6dFZM%2B1ZIlitGl8P%2FYDYc29Xe3V2YLnXId61I%2FDAMpdr11QnpFkb0T0td3AYBuagn%2BjNt9%2B7v6i2lE3xXsd9104Vwn0c9xXsOQ6N3c%2BeHjR9xvo8Nlmv46LsuSjFyc5lXrSI44qUE9hBbIpGOvu2sKSJJU4UkLWuc0S9cL5%2FRQVNgwbY6go%2BEouQzN&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20240806T035425Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAS7VSBD45DIV7S66U%2F20240806%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=847513d9ccfc8e1b27f33a75b3c31d624fe405a48fbed49991f83f1a791a365b)
