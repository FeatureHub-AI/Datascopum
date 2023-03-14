# Number of Incoming SMS from Bank
 
The number of incoming SMS messages from a bank refers to the number of text messages received by a subscriber from alfa-numerical sender that can be identified as a bank.

## The idea behind

Interaction with banks and other financial institutions is an integral part of our everyday life. The number of SMS messages a subscriber receives will depend on the bank's messaging policy, the customer's account settings, and the type of account they have. The high number of incoming SMS from the bank also allows us to suggest an active, advanced, and modern user who uses his phone also to connect to external services in order to stay up-to-date. 

#### Example 

This is Michael. He is a progressive, tech-savvy user. He has a Netflix subscription and a Spotify subscription, and he has several apps for online shopping, news, and taxi on his phone. Michael has Apple Pay and bank services app. He values good and quality service that saves his time, he has a dynamic life, and likes to stay up-to-date. SMS from the bank allows him to track his expenses, adjust his budget and monitor his bank account state. His real life routine generates at least 1 SMS notification every day.  

## Key effects
 
#### 💡 Effect on churn prediction

Progressive and tech-savvy subscribers usually have more expectations for the services and features offered by their telecom provider. They tend to switch to a different provider if they feel that their current provider is not meeting their needs or is not keeping up with industry trends. They may also be more likely to be influenced by social media, online reviews, and the opinions of their peers when making a decision to switch providers.

#### 💡 Effect on usage patterns

Progressive subscribers are likely to be heavy users of technology and may have a higher demand for data-intensive services such as streaming video and music, online gaming, and social media. They may also be more likely to use multiple devices and to use their devices throughout the day, which can lead to higher data usage.

They may also be more likely to use their smartphones as their primary means of communication, which can lead to higher usage of voice and text services.

Progressive and young subscribers may also be more likely to use services like voice-over-IP (VoIP), instant messaging, and social media messaging instead of the traditional phone and SMS services.

#### 💡 Effect on LTV prediction

Progressive telecom subscribers may have a higher LTV because they are likely to be early adopters of new technology and services, and may be more likely to stick with a provider that is able to meet their evolving needs. They may also be more likely to pay a premium for advanced features or higher data allowances.

On the other hand, these subscribers may also have a lower LTV if they are more likely to switch providers if they feel their current provider is not meeting their needs, or if they are more price-sensitive and may be more likely to switch to a cheaper provider.

## Methodology 👨🏻‍💻

The number of incoming SMS messages from a bank is represented by a number of variables, called "SMS_INC_BANK_CNT_PERIOD". 
This feature can be calculated by counting the number of SMS messages sent by the bank to its customers over a period of time. To calculate this you need a dimension or dictionary table to identify which sender name refers to a bank. You will need to adapt such information to area of providing services. 

**Hint**: It's important to note that these calculations are based on the assumption that the subscriber has not opted out of receiving SMS messages from the bank for that feature and that the bank has the correct phone number for that subscriber. From time to time you will need to update actual information about sender name and actual bank. In this example we recommend to start with weekly and monthly trends, because telecom and banking industry are quite long term and you wont find much information in nois daily data. Anyway try to experiment.

#### Metacode example

Here is the example of SQL code to create SMS_INC_BANK_CNT_W1

```sql

SELECT
  COUNT(*) FILTER(
  WHERE
    sender_type = 'bank'
    AND DATE_DIFF(snapshot_date, event_date, day) BETWEEN -7
    AND -1) AS SMS_INC_BANK_CNT_W1
FROM
  sms_messages

```
Please note that this query is just an example, and you may need to adjust the table and column names to match the structure of your own SMS data table.
You can manipulate with filter to adjust date ranges.

It's important to note that this query assumes that the database has a table called "sms_messages" with column that identifies type of a sender.

#### Variables

We used the following variables

```sql
#it is on purpose that for weeks we use relative 7 days, while for months we use full calendar months

# sms_inc_bank_cnt_w1

# sms_inc_bank_cnt_w2 - 'w2' refers to the week that was 2 weeks ago, e.g. date_diff(day) between -15 and -8

# sms_inc_bank_cnt_w3

# sms_inc_bank_cnt_w4

# sms_inc_bank_cnt_4w - '4w' refers to consecutive 4 weeks ago, e.g. date_diff(day) between -29 and -1

# sms_inc_bank_cnt_m1

# sms_inc_bank_cnt_m2 - 'm2' refers to the month that was 2 calendar months ago, e.g. date_diff(month) = -2 

# sms_inc_bank_cnt_m3

# sms_inc_bank_cnt_3m

# sms_inc_bank_cnt_6m - '6m' refers to consecutive 6 calendar months ago, e.g. date_diff(month) between -6 and -1

```  

## Data source

An example of data source in the telecom industry that could be used to calculate the number of SMS messages sent by the bank would be the SMS gateway logs and dimension table, either combined or stored separately.

#### Datasets
Subscriber ID
SMS messages: the sender's number, and the recipient's number.
Sender information: This would include the sender's name or phone number, which you would use to filter the SMS messages sent by the bank.
Time sent: This would include the date and time the SMS was sent, which you could use to filter messages by a specific time range.
Additional information: This may include information such as the message's unique identifier, the sender's IP address, and the protocol used to send the message.


#### Minimum required data
Subscriber ID - this is your customer id to generate scoring

event_date - this is used to adjust time ranges for aggregation

sender - this is alfa-numerical name of a sender / recepient of SMS

sender_type - this is category, can be calculated by dimension or dictionary table for sender names in your country



#### Data example

| Subscriber ID | event_date    | sender | Sender_type  |
|---------------|-------------|-----------|--------------|
| 12345         | 2023-01-24    | sabadell        | bank      |
| 12345         | 2023-01-24    | 954491726         | personal       |
| 12345         | 2023-01-23    | santander         | bank       |
| 12345         | 2023-01-22    | 9172616382         | personal      |
| 12345         | 2023-01-22    | aliexpress         | e-com      |


## Additional info

#### Origin 🕵🏻‍♂️
Overall usage of this kind of dimension tables to determine sender type appeared when big data become popular, so data scientists started to search for extra information in raw data rather than generic aggregations.


#### Related articles 📚

If you found articles or pages with behavioral research, case studies, or experiments - feel free to contribute via the personal space panel.
