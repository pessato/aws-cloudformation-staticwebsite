# aws-cloudformation-staticwebsite

A CloudFormation template to host a static websites securely.

Requires a Route 53 Hosted Zone and provisioned SSL certificate using AWS Certificate Manager.

Creates two S3 buckets, two CloudFront distributions, an ALIAS record and CNAME record.

Allows for HTTP and HTTPS request to either the root/apex or www&#46; subdomain which will be redirected to the HTTPS www&#46; subdomain.

i.e. 
- *http&#58;//example&#46;com* > *https&#58;//www&#46;example&#46;com*
- *https&#58;//example&#46;com* > *https&#58;//www&#46;example&#46;com*
- *http&#58;//www&#46;example&#46;com* > *https&#58;//www&#46;example&#46;com*
- *https&#58;//www&#46;example&#46;com* > *https&#58;//www&#46;example&#46;com*

## Set up instructions

Create a Route 53 hosted zone for 

## TODO 

ON WWW CLOUDFRONT

- General > Update Supported HTTP Versions  to HTTP/2, HTTP/1.1, HTTP/1.0
- Origins > Change origin to just origin domain name / origin id / origin type (not custom)
- Behaviours > change origin to new origin from previous step
- 

ON NON-WWW CLOUDFRONT

- General > Update Supported HTTP Versions  to HTTP/2, HTTP/1.1, HTTP/1.0
- Origins > Change origin id
- Behaviour > select new origin > select Viewer Protocol Policy to HTTP and HTTPS
- 

S3 Bucket NON-WWW

- redirect protocol - https

- bucket policy
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "[BUCKET_ARN]/*"
        }
    ]
}

- permission access control list everyone read read