# Helper stuff


## zsh-precmd

This snippet can be used to setup zsh-prompt to include information about assumed IAM role.

![Example](https://raw.githubusercontent.com/ristkari/assuming-role/master/example.png)

You must have the following environment variables defined:
- ASSUMED_ROLE = Name of the profile used to assume role
- CREDENTIALS_EXPIRATION = When your credentials expire. As seconds from Unix-epoch


## Setup AWS CLI for easy role assuming

You should have:

Source-account = This account is the one where you have IAM user
Example in 'credentials':
```
[source-account]
region=eu-west-1
aws_access_key_id=AKIsome-secret-key-id
aws_secret_access_key=and-its-secret-companion
```

Target-profile in 'config':
```
[profile example-role-on-target-account]
output=json
region=eu-west-1
role_arn=arn:aws:iam::210987654321:role/role-name-to-be-assumed
source_profile=source-account
mfa_serial=arn:aws:iam::123456789012:mfa/your-user-name
```

Once done like this you can call ```aws s3 ls --profile example-role-on-target-account ``` and AWS CLI will automatically do AssumeRole (and ask MFA if you have it enabledi, this example assumes you do as it is a best practice). 


