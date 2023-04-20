---
sidebar: reference
---

# Route53
Create the record in Amazon AWS [Route53](https://aws.amazon.com/route53/)

{% include plugin-seperate.md %}

## Setup
This requires either a user or an IAM role with the following permissions on the zone: 
`route53:GetChange`, `route53:ListHostedZones` and `route53:ChangeResourceRecordSets`. 
The IAM role method can only work from inside a current EC2 instance.

## Unattended 
- User:
`--validation route53 --route53accesskeyid x --route53secretaccesskey ***`
- IAM  role:
`--validation route53 --route53iamrole x`
