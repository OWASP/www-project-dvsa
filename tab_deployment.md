---
title: Deployment
layout:  null
tab: true
order: 1
tags: deployment
---

# Deployment

#### [Application Repository](AWS/VIDEOS/reo_deploy.mp4)
- Deploy DVSA from the [AWS Serverless Application Repository](https://serverlessrepo.aws.amazon.com/applications/arn:aws:serverlessrepo:us-east-1:674087993380:applications~OWASP-DVSA)

- After deployment is complete. Click on 'View CloudFormation Stack'

- Under 'Outputs' you will find the URL for the application (DVSA Website URL)


![](https://i.imgur.com/ZfjEyiM.png)
#### [Serverless Framework](AWS/VIDEOS/serverless_deploy.mp4)

You must run serverless deploy commands with an environment variable profile (e.g. `AWS_PROFILE=<aws-profile-name>`) instead of the serverless argument.

##### Clone Project
- `git clone git@github.com:OWASP/DVSA.git`

##### Install Serverless
- `npm install -g serverless`

##### Install AWS-CLI
- `pip install awscli --upgrade --user`

##### Verify AWS-CLI Installation
- `aws --version`

If you get a "command not found" error, see the "Steps to Take after Installation" section [here](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html#install-tool-pip).

##### Configure AWS-CLI for your Account
- `aws configure`

##### Install dependencies
- `npm i`

##### Deploy Backend
- `sls deploy`

##### Build Client
- `npm run-script client:build`

##### Deploy Client
- `sls client deploy`

- - -
## Running locally

#### Run Client
- `npm run-script client:start`

**_Note_**: This will only work if you previously deployed the backend. If this fails, confirm you still have a `be-stack.json` file at the root of this project.

#### Run Backend
- `npm start`

If you want to point your local client to your local backend, edit your `be-stack.json` and set `ServiceEndpoint` to `http://localhost:3000`. Note that you will still be using the Cognito pools in AWS.

- - -
## Email subscription

DVSA sends receipts in the email (which will help you in hacking it). You can use the built-in **Inbox** page within the application to get the emails and obtain the receipts.

**_Note_**: each user will be assigned an email from `mailsac.com` which will be automatically verified. Real emails will be sent to their account and will appear in the application Inbox page. All this is **transparent** to the user and the deployer).

**_Note_**: to make the email verification script work your default AWS region has to be "US East (N. Virginia)", for example by setting `region = us-east-1` in your ~/.aws/config file

**Alternatively**, if you want users to receive emails to their registered email account (e.g. gmail), use one of the followings:

- Send an email verification link to email address, by running the following command (after clicking on the received link, emails will **also** be sent to their actual email address):

`aws ses verify-email-identity --email-address <your_email>`

- [Request a sending limit increase](https://console.aws.amazon.com/support/v1#/case/create?issueType=service-limit-increase&limitType=service-code-ses). This will allow your entire cloud account to send emails to any address.
