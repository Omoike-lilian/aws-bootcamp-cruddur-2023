# Week 0 — Billing and Architecture
Hi Project Bookcamp,
This has been a amazingly challenging feat.
Well, I had to start all over again as I ran into an error while trying to launch gitpod for week 1 task.
Spent some time trying to debug the error and eventually used Chatgpt to find the error.
Apparently, my gitpod.yml file was wrongly indented and that prevented the workspace from launching.
So, this is the new project.
On to ir...


Creating Lucid chart Diagram

I was able to recreate the Lucid chart cruddur diagram as instructed link to my work: https://lucid.app/lucidchart/f63c18e9-7182-4e59-a7f3-e07c4f317ee1/edit?viewport_loc=-350%2C-478%2C2443%2C947%2C0_0&invitationId=inv_ab3d98b2-0b89-4cc4-bf90-d6741630c957

![lucid diagram](https://user-images.githubusercontent.com/53332265/225341733-159483bc-1001-4a15-90a3-00a51cd3287e.png)


AWS Admin Account 

I created an admin account in AWS. However, I did not use my Admin account for thr homework.I instead created an I AM user account, added the user to a group and attached permissions to the group. I went ahead to create a buget and set up billing alarm

I was able to install the AWS CLi in gitpod I did install it in the aws-bootcamp=cruddur-2023 directory at first then I uninstalled followung the instructions: https://docs.aws.amazon.com/cli/latest/userguide/uninstall.html then change directory to workspace and did the install again
![image](https://user-images.githubusercontent.com/53332265/225347565-c8f85fba-dd9b-420e-b5d1-ea82e66f120e.png)


Create a Budget
I was able to create Aws Budget using the GUI as well as the CLi
![image](https://user-images.githubusercontent.com/53332265/225346761-957ca715-59aa-4be6-8b36-2d93d0e57e14.png)

Notes/Errors 
1. wrongly indented the gitpod.yml file..this necessitated starting over( well hope to catch up soon)
2. created the aws/json folder in the doc folder. As a result I was unable to create my billing alarm. Had to delete the folder and create another in Main using gitpod
3. Aws Cli was unable to read accound_Id as $ACCOUNT which was committed to the environment variable. Had to manually input the account Id for billing alarm to be created

My Code Example;
{
    "AlarmName": "DailyEstimatedCharges",
    "AlarmDescription": "This alarm would be triggered if the daily estimated charges exceeds 1$",
    "ActionsEnabled": true,
    "AlarmActions": [
        "arn:aws:sns:us-east-1:900645165270:billing-alarm"
    ],
    "EvaluationPeriods": 1,
    "DatapointsToAlarm": 1,
    "Threshold": 1,
    "ComparisonOperator": "GreaterThanOrEqualToThreshold",
    "TreatMissingData": "breaching",
    "Metrics": [{
        "Id": "m1",
        "MetricStat": {
            "Metric": {
                "Namespace": "AWS/Billing",
                "MetricName": "EstimatedCharges",
                "Dimensions": [{
                    "Name": "Currency",
                    "Value": "USD"
                }]
            },
            "Period": 86400,
            "Stat": "Maximum"
        },
        "ReturnData": false
    },
    {
        "Id": "e1",
        "Expression": "IF(RATE(m1)>0,RATE(m1)*86400,0)",
        "Label": "DailyEstimatedCharges",
        "ReturnData": true
    }]
  }

This has been a rewarding, amazing experience. Had to do a lot of self study.

Challenges Had to work all night to complete this due to work schedule.

Thank you for the opportunity!
