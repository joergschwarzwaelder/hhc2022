
# Objective 11: AWS CLI Intro
**Location: Cloud Ring / AWS101 Terminal**  
**Hints from Jill Underpole**

This objective is about getting familiar with the AWS CLI and is a guided exercise.

1. `You may not know this, but AWS CLI help messages are very easy to access. First, try typing:
$ aws help`
```
aws help
```

2. `Next, please configure the default aws cli credentials with the access key AKQAAYRKO7A5Q5XUY2IY, the secret key qzTscgNdcdwIo/soPKPoJn9sBrl5eMQQL19iO5uf and the region us-east-1 .`

```
elf@4191a3131f45:~$ aws configure
AWS Access Key ID [None]: AKQAAYRKO7A5Q5XUY2IY
AWS Secret Access Key [None]: qzTscgNdcdwIo/soPKPoJn9sBrl5eMQQL19iO5uf
Default region name [None]: us-east-1
Default output format [None]:
```

3. `Excellent! To finish, please get your caller identity using the AWS command line. For more details please reference:
$ aws sts help`
```
elf@4191a3131f45:~$ aws sts get-caller-identity

{
    "UserId": "AKQAAYRKO7A5Q5XUY2IY",
    "Account": "602143214321",
    "Arn": "arn:aws:iam::602143214321:user/elf_helpdesk"
}
```

**Achievement: AWS CLI Intro**
