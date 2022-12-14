
# Objective 12: Trufflehog Search
**Location: Cloud Ring**  
**Hints (2x) from Jill Underpole**

This objective is about getting familiar with the tool [Trufflehog](https://github.com/trufflesecurity/trufflehog) to find credentials in repositories, in this case specifically [this one](https://haugfactory.com/asnowball/aws_scripts.git).

```
Use Trufflehog to find credentials in the Gitlab instance at https://haugfactory.com/asnowball/aws_scripts.git.
Configure these credentials for us-east-1 and then run:
$ aws sts get-caller-identity
```
We are running Trufflehog against the repository:
```
joergen@northpole:~$ trufflehog --debug git https://haugfactory.com/asnowball/aws_scripts.git

🐷🔑🐷  TruffleHog. Unearth your secrets. 🐷🔑🐷

Found unverified result 🐷🔑❓
Detector Type: AWS
Decoder Type: PLAIN
Raw result: AKIAAIDAYRANYAHGQOHD
File: put_policy.py
Email: asnowball <alabaster@northpolechristmastown.local>
Repository: https://haugfactory.com/asnowball/aws_scripts.git
Timestamp: 2022-09-07 07:53:12 -0700 -0700
Line: 6
Commit: 106d33e1ffd53eea753c1365eafc6588398279b5

Found unverified result 🐷🔑❓
Detector Type: Gitlab
Decoder Type: PLAIN
Raw result: add-a-file-using-the-
Commit: 2c77c1e0a98715e32a277859864e8f5918aacc85
File: README.md
Email: alabaster snowball <alabaster@northpolechristmastown.local>
Repository: https://haugfactory.com/asnowball/aws_scripts.git
Timestamp: 2022-09-06 19:54:48 +0000 +0000
Line: 14

Found unverified result 🐷🔑❓
Detector Type: Gitlab
Decoder Type: BASE64
Raw result: add-a-file-using-the-
Commit: 2c77c1e0a98715e32a277859864e8f5918aacc85
File: README.md
Email: alabaster snowball <alabaster@northpolechristmastown.local>
Repository: https://haugfactory.com/asnowball/aws_scripts.git
Timestamp: 2022-09-06 19:54:48 +0000 +0000
Line: 14
```

Now we have an indication that the required credentials are in the file **put_policy.py** from commit 106d33e1ffd53eea753c1365eafc6588398279b5.

**Achievement: Trufflehog Search**
