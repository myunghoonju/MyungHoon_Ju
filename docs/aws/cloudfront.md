_CloudFront_  
 - 정적, 동적, 실시간 웹사이트 컨텐츠를 전달
 - edge location
 - content delivery network
 - distributed network  

policy sample
> {  
 		"Version": "2008-10-17",  
  "Id": "PolicyForCloudFrontPrivateContent",  
  "Statement": [  
			{  
      "Sid": "AllowCloudFrontServicePrincipal",  
      "Effect": "Allow",  
      "Principal": {  
        "Service": "cloudfront.amazonaws.com"  
      },  
      "Action": "s3:GetObject",  
      "Resource": "arn:aws:s3::.../*",  
      "Condition": {  
        "StringEquals": {  
          "AWS:SourceArn": "arn:aws:cloudfront:..."  
        }}}]}  
