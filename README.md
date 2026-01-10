# genai-aws-bedrock

Collection of notebooks that demonstrates AWS Bedrock usage.

IAM permissions:

To invoke a Bedrock model from a SageMaker Notebook Instance, you need to grant permissions to the Notebook Instance IAM role (the role SageMaker assumes when running your notebook). Example policy to attach is shown below:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "BedrockInvoke",
      "Effect": "Allow",
      "Action": [
        "bedrock:InvokeModel",
        "bedrock:InvokeModelWithResponseStream"
      ],
      "Resource": "*"
    }
  ]
}

IAM permissions required for an Amazon Bedrock Knowledge Base to access S3, attach IAM policy to the KB execution role. Example policy is shown below:

{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "AllowListBucketForKbPrefix",
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "arn:aws:s3:::my-bucket",
      "Condition": {
        "StringLike": {
          "s3:prefix": ["docs/*"]
        }
      }
    },
    {
      "Sid": "AllowGetObjectsForKbPrefix",
      "Effect": "Allow",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-bucket/docs/*"
    }
  ]
}

