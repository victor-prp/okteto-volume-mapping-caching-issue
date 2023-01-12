# Intro 
This repo is the working example that reproduces the following issue:

When we define a service volume mapping in docker-compose, 
the data of the mapped volume is not updated even after we destroy the deployment.


#Step to reproduce
- Clone this repo
- Run `okteto deploy`
- Take a look at the logs of the deployed service. You expect to see the following log: `2023-01-12 10:07:54.86 UTCoriginal-localstack-5448d4ff79-h8rxsoriginal-localstackmake_bucket: original-bucket`. That means the service has created s3 bucket as defined in the s3Setup.sh file.
- Destroy the deployment
- Change the bucket name in  s3Setup.sh file, so it will look as following:  `awslocal s3 mb s3://updated-bucket `
- Run `okteto deploy`
- Take a look at the logs of the deployed service. You expect to see the following log: `2023-01-12 10:07:54.86 UTCoriginal-localstack-5448d4ff79-h8rxsoriginal-localstackmake_bucket: original-bucket`. That means the service has created the original s3 bucket and was not updated according to s3Setup.sh file.
- Destroy the deployment
- Change the name of the service in docker-compose to `updated-localstack`
- Run `okteto deploy`
- Take a look at the logs of the deployed service. You expect to see the following log: `2023-01-12 10:07:54.86 UTCupdated-localstack-5448d4ff79-h8rxsoriginal-localstackmake_bucket: updated-bucket`.
- That means the problem was solved by renaming the service




