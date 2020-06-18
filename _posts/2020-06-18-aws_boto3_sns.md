---
title: "AWS SNS Topic Configuration and Handling with Boto3 on Python with a alert system project."
date: 2020-06-18
categories: [Python]
tags: [AWS]
header:
  image: "/images/aws_s3_boto3/header.png"
excerpt: "The objective of the post was to learn and understand importance of AWS SNS and configuration of this service using Boto3 on python. Further, we managed topics, subscribers and message bodies. Finally, we built an Alert System for a government trying to alert students to avoid coming to school on a heavy rain days using all the techniques we learned"
mathjax: "true"
---
## AWS SNS and Rekognition with Boto3

### Introduction:
**What is SNS ?**

Amazon Simple Notification Service is a notification service provided as part of Amazon Web Services since 2010. It provides a low-cost infrastructure for the mass delivery of messages, predominantly to mobile users.

### Key Terms:
**Publisher :** Publish messages from distributed systems, microservices, and other AWS services.

**SNS Topic :** Decouple messages published from subscribers with topics

**Message Filtering & Fanout :** Filter messages accoriding to subscription filter policies, queues, microservices, and more

**Subscribers :** Receive messages in subscribing serverless functions, queues, microservices, and more.

![png](\images\aws_sns_boto3\intro.png)

```python
import boto3
```


```python
# Build a client to access the service methods
sns = boto3.client('sns',region_name='us-east-1',
                  aws_access_key_id='AKIAQU6F5LRCKOWLDSTU',
                  aws_secret_access_key='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')
```

### Creating a Topic:
An Amazon SNS topic is a logical access point that acts as a communication channel. A topic lets you group multiple endpoints


```python
response = sns.create_topic(Name='post_alert')
```


```python
response['TopicArn']
```




    'arn:aws:sns:us-east-1:044975348804:post_alert'



Topic Arn is basically a Unique name for your topic

### Listing topics that already exist:


```python
sns.list_topics()['Topics']
```




    [{'TopicArn': 'arn:aws:sns:us-east-1:044975348804:post_alert'}]



It just returned one Arn that means we have just one Topic that we created a while back.

### Deleting topics:
This is where you will need your Arn to make changes to your created topics.


```python
sns.delete_topic(TopicArn='arn:aws:sns:us-east-1:044975348804:post_alert')
```




    {'ResponseMetadata': {'RequestId': '21ad4d77-c77d-5a41-a404-1a13bacab65f',
      'HTTPStatusCode': 200,
      'HTTPHeaders': {'x-amzn-requestid': '21ad4d77-c77d-5a41-a404-1a13bacab65f',
       'content-type': 'text/xml',
       'content-length': '201',
       'date': 'Wed, 17 Jun 2020 20:22:14 GMT'},
      'RetryAttempts': 0}}




```python
sns.list_topics()['Topics']
```




    []



An empty list means there are no topics in sns anymore.

### Create an SMS subscription.
**We have a topic but what about our subscriber?**

Subscribers would be entities within the topic groups who will receive the broadcast when a message is sent to the topic.




```python
# re creating the topic
sns.create_topic(Name='post_alert')['TopicArn']
```




    'arn:aws:sns:us-east-1:044975348804:post_alert'




```python
response = sns.subscribe(TopicArn ='arn:aws:sns:us-east-1:044975348804:post_alert',
                         Protocol='email',
                         Endpoint='sjk714@nyu.edu')
```

**You can have subscriber saved with their email as shown above or you can have it saved with their phone number as shown below.**
With email subscription the subscriber will be sent a confirmation email before they start receiving the broadcasted messages within their topics.

![png](\images\aws_sns_boto3\noti.png)



```python
response = sns.subscribe(TopicArn ='arn:aws:sns:us-east-1:044975348804:post_alert',
                         Protocol='SMS',
                         Endpoint='+13737373738')
```

### Listing subscriptions by Topic:


```python
sns.list_subscriptions_by_topic(TopicArn='arn:aws:sns:us-east-1:044975348804:post_alert')['Subscriptions']
```




    [{'SubscriptionArn': 'arn:aws:sns:us-east-1:044975348804:post_alert:3b4f0187-cdab-4750-88ff-da799067c423',
      'Owner': '044975348804',
      'Protocol': 'sms',
      'Endpoint': '+13737373738',
      'TopicArn': 'arn:aws:sns:us-east-1:044975348804:post_alert'},
     {'SubscriptionArn': 'PendingConfirmation',
      'Owner': '044975348804',
      'Protocol': 'email',
      'Endpoint': 'sjk714@nyu.edu',
      'TopicArn': 'arn:aws:sns:us-east-1:044975348804:post_alert'}]



**We can see both our added subscribers with their TopicArns**

### Deleting subscriptions:
**What if we need to remove someone from our subscription list?**

There is a simple `unsubscribe` function that lets us do that. All we need is that subscribers SubscriptionArn and that is it.
As we saw in the `list_subscriptions_by_topic` we get all the required details for the subscriber.


```python
sns.unsubscribe(SubscriptionArn='arn:aws:sns:us-east-1:044975348804:post_alert:3b4f0187-cdab-4750-88ff-da799067c423')
```




    {'ResponseMetadata': {'RequestId': 'fe1b9a58-b111-581e-bcd5-cd3c30700099',
      'HTTPStatusCode': 200,
      'HTTPHeaders': {'x-amzn-requestid': 'fe1b9a58-b111-581e-bcd5-cd3c30700099',
       'content-type': 'text/xml',
       'content-length': '201',
       'date': 'Wed, 17 Jun 2020 20:37:52 GMT'},
      'RetryAttempts': 0}}




```python
sns.list_subscriptions_by_topic(TopicArn='arn:aws:sns:us-east-1:044975348804:post_alert')['Subscriptions']
```




    [{'SubscriptionArn': 'PendingConfirmation',
      'Owner': '044975348804',
      'Protocol': 'email',
      'Endpoint': 'sjk714@nyu.edu',
      'TopicArn': 'arn:aws:sns:us-east-1:044975348804:post_alert'}]



#### Amazing!!! we have just one subscriber now withing out Post_alert topic

### Finally! Publishing messages in these Topic groups:


```python
response = sns.publish(TopicArn ='arn:aws:sns:us-east-1:044975348804:post_alert',
                       Message ='Body text of SMS or e-mail',
                       Subject ='Subject Line for Email')
```

**You can send personal messages as well, though sns is not meant for this purpose as it is time consuming and would turn out inefficient as well.**


```python
response = sns.publish(PhoneNumber ='+13121233211',Message ='Body text of SMS or e-mail')
```

### Deleting resources we do not need:


```python
# Deleting Topic:
sns.delete_topic(TopicArn ='arn:aws:sns:us-east-1:044975348804:post_alert')
```




    {'ResponseMetadata': {'RequestId': 'c8e51333-6c8e-5392-a3db-4457ef32dafc',
      'HTTPStatusCode': 200,
      'HTTPHeaders': {'x-amzn-requestid': 'c8e51333-6c8e-5392-a3db-4457ef32dafc',
       'content-type': 'text/xml',
       'content-length': '201',
       'date': 'Wed, 17 Jun 2020 20:47:56 GMT'},
      'RetryAttempts': 0}}




```python
#Will send empty list
sns.list_topics()
```




    {'Topics': [],
     'ResponseMetadata': {'RequestId': '17d5ec15-cc19-5289-a248-bb714fdcdd02',
      'HTTPStatusCode': 200,
      'HTTPHeaders': {'x-amzn-requestid': '17d5ec15-cc19-5289-a248-bb714fdcdd02',
       'content-type': 'text/xml',
       'content-length': '256',
       'date': 'Wed, 17 Jun 2020 20:48:05 GMT'},
      'RetryAttempts': 0}}




```python
sns.list_subscriptions()
```




    {'Subscriptions': [{'SubscriptionArn': 'PendingConfirmation',
       'Owner': '044975348804',
       'Protocol': 'email',
       'Endpoint': 'sjk714@nyu.edu',
       'TopicArn': 'arn:aws:sns:us-east-1:044975348804:post_alert'}],
     'NextToken': 'AAFE/yx/6PkPtthC8WRfZwZAVNlBYBPc7WvPN9pv0FC67w==',
     'ResponseMetadata': {'RequestId': 'ed93fba3-46be-57a6-92bd-acc7c55e8c2c',
      'HTTPStatusCode': 200,
      'HTTPHeaders': {'x-amzn-requestid': 'ed93fba3-46be-57a6-92bd-acc7c55e8c2c',
       'content-type': 'text/xml',
       'content-length': '671',
       'date': 'Wed, 17 Jun 2020 20:48:32 GMT'},
      'RetryAttempts': 0}}



We can see that this subscriber was registered over mail and is still under pending status.
**At this time, pending subscriptions cannot be explicitly deleted. Pending subscription will automatically be deleted after 72 hours.**

## Lets build a tiny project to make concepts much easier to remember:

**Problem Statement:**

Government in India realised how rains and flooding in rural areas occurs often and due to restrictive infrastructure due to availability of less staff and technologies ir becomes difficult to inform students and their parents to not leave for school before it is too late.

**Solution:**

We will build a system that will send alerts by districts to these students using AWS SNS. In our case we will check for inches of rain from our S3 bucket data that gets updated every minute by the live IOT sensors through Kinesis and configure our SNS accordingly.


#### Get the aggregated numbers:
- Check rain in inches every minute

#### Send Alerts:
- If rain increases 10 inches

**Resources:**

https://medium.com/swlh/real-time-data-streaming-with-python-aws-kinesis-how-to-part-1-cd56feb6fd0f
https://boto3.amazonaws.com/v1/documentation/api/latest/index.html


```python
# Build a client to access the service methods
sns = boto3.client('sns',region_name='us-east-1',
                  aws_access_key_id='******',
                  aws_secret_access_key='*********')
```


```python
import pandas as pd
import boto3
```


```python
#load contacts
contacts = pd.read_csv('http://RainAlert.s3.amazonaws.com/contacts_parent.csv')
contacts
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Name</th>
      <th>Email</th>
      <th>Phone</th>
      <th>District</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>John Smith</td>
      <td>js@fake.com</td>
      <td>11224567890</td>
      <td>D1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Fanny Mae</td>
      <td>fannyma3@fake.com</td>
      <td>11234597890</td>
      <td>D2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Janessa Goldsmith</td>
      <td>whoami@fake.com</td>
      <td>11534567890</td>
      <td>D1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Evelyn Monroe</td>
      <td>Evely@fake.com</td>
      <td>11234067890</td>
      <td>D3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Max Pe</td>
      <td>max@maksimize.com</td>
      <td>11234517890</td>
      <td>D3</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Build a client to access the service methods
sns = boto3.client('sns',region_name='us-east-1',
                  aws_access_key_id='****',
                  aws_secret_access_key='****')
```


```python

# making topics for each district
districts = contacts['District'].unique()
dict_arn={}
for a in districts:
    arn = sns.create_topic(Name=a+'_alert')['TopicArn']
    dict_arn[a] = arn
```
**There we have all our topics...**

![png](\images\aws_sns_boto3\topic.png)

```python
# Adding subscriber
for a in range(len(contacts)):
    if contacts['District'][a] in dict_arn:
        sns.subscribe(TopicArn = dict_arn[contacts['District'][a]], Protocol='sms', Endpoint=str(contacts['Phone'][a]))

```

Name|Email|Phone|District
-----|-----|-----|-----|
John Smith |js@fake.com |+11224567890 |D1
Fanny Mae |fannyma3@fake.com| +11234597890| D2
Janessa Goldsmith |whoami@fake.com |+11534567890 |D1
Evelyn Monroe |Evely@fake.com |+11234067890 |D3
Max Pe |max@maksimize.com |+11234517890 |D3

**Added the subscribers as per their districts**
![png](\images\aws_sns_boto3\subs.png)
```python
# Checking the length of rain
df = pd.read_csv('http://gid-reports.s3.amazonaws.com/2019/feb/final_report.csv')

for a in range(len(df)):
    if df['rain_inch'][a] >= 10:
        # Construct the message to send
        message ="Rain level has reached {}.Parents are requested to not send their kids to school".format{df['rain_inch'][a]}
        # Send message
        sns.publish(TopicArn = df['district'][a],Message = message,Subject = "Rain Alert")
```

**Amazing!!! This should get the work done**

This simple system should help the government keep students in each district safe and not coming to school when the chances of floods are high.

Our built system would work perfect on aws kinesis data stream which lets us stream live data from the sensors and process it.
You can further refer to below links to learn more
https://medium.com/swlh/real-time-data-streaming-with-python-aws-kinesis-how-to-part-1-cd56feb6fd0f
https://boto3.amazonaws.com/v1/documentation/api/latest/index.html

### That is about all the basic functions for SNS that you would need to get started.
# Happy Learning


```python

```
