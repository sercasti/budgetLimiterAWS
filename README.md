# budgetLimiterAWS
CloudFormation template to limit spend on AWS resources based on a tag, optionally stop compute instances at threshold

Creates an AWS budget and notifies you when you exceed thresholds, optionally, stop compute instances from a specific tag. Remember billing data is updated daily just once, so no guarantees.

* Enter your budget in USD
* Enter your first Threshold for notification
* Enter your second hreshold for notificationh and optionally shutdown EC2 instances
* Enter your Email for notifications
* Enter the Tag to use as filter for billing
* choose if you want to "StopResources": Automatically stop EC2 instances with this tag at SecondThreshold percentage


If you choose to stop the EC2 instances, this template will create an SNS topic, a lambda, a role for that lambda, and execute the lambda at the second threshold, which will filter all ec2 instances by that tag, and send a "stop" action to all of them.

**Disclaimer 1**: AWS billing data, which Budgets uses to monitor resources, is updated at least once per day. Keep in mind that budget information and associated alerts are updated and sent according to this data refresh cadence.

**Disclaimer 2**: CF template for AWS::Budget doesn't support Forecasted costs yet, and AWS requires approximately 5 weeks of usage data to generate budget forecasts. If you set a budget to alert based on a forecasted amount, this budget alert isn't triggered until you have enough historical usage information.
