## Export JMeter test results to CloudWatch Logs.

Code from the following blog post:
https://www.concurrencylabs.com/blog/publish-jmeter-test-results-to-cloudwatch-logs/


This repo contains the following:

* CloudFormation template for publishing JMeter test results to CloudWatch Logs
* Sample JMeter test plan to quickly validate that the stack was created properly and JMeter
test results are ultimately available as CloudWatch metrics.


### jmeter_server.json
This template performs the following tasks:
* Launches an EC2 instance with JMeter and the Flexible File Writer plugin installed. 
* Installs the CloudWatch Logs agent and it creates metric filters for converting log entries
into CloudWatch metrics. 
* The EC2 instance is launched with an EC2 Instance Profile, which gives permissions to the
the CloudWatch Logs agent for publishing log data to CLoudWatch Logs. 
* This template also downloads a sample JMeter test plan (included in this repo) that sends HTTP requests
to an S3 endpoint. This is only intended for validation purposes.

JMeter is installed in the following directory:

```
/home/ec2-user/jmeter/apache-jmeter-2.13
```

The JMeter test plan is downloaded to the following location: 

```
/home/ec2-user/jmeter/test-plans/basicHttpTest.jmx
```

The CloudWatch Logs agent expects the JMeter test result log in the following location:

```
/home/ec2-user/jmeter/test-results/results.log
```

To start the JMeter test just SSH to the EC2 instance launched by this template and execute:

```
nohup /home/ec2-user/jmeter/apache-jmeter-2.13/bin/jmeter -n -t /home/ec2-user/jmeter/test-plans/basicHttpTest.jmx &
```

Once you run the JMeter test, you should be able to see test results flowing into CloudWatch Logs
almost immediately.






