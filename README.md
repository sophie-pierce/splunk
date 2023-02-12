# Splunk

## Scenario:

Our team of SOC Analysts received word that JobeCorp, the competitor to Virtual Space Industries (VSI), was going to launch a cyber attack attempting to disrupt the system and applications we run. As employees of VSI and being SOC Analysts, it’s our task to monitor the administrative webpage, Apache web server which hosts the webpage, and our Windows operating system which runs many of VSI’s back-end operations. It’s crucial that we protect VSI’s intellectual property, as Jobe Corp and other competitors may try to steal our ideas for next generation virtual-reality programs. 

In the past, VSI did not rely on strict policies to protect against attacks, and unfortunately we came to the conclusion that an attack was attempted and carried out. We pulled the logs and discovered a brute force attack from JobeCorp had occurred. After coming to this conclusion and hoping to avoid the same issues in the future, our team of SOC Analysts created tighter alerts and policies within Splunk. 

*Conducted in Vagrant VM*

## Add-On App: Website Monitoring 
  - Goal: Protect VSI's intellectual property
  
![addedsplunkapp](https://user-images.githubusercontent.com/109919882/217046246-5a288c51-50cb-45d7-be23-cf95173225ac.png)

## Logs Analyzed

Windows Logs:
- Signature field values over time
- User field values
- Count of different signatures 
- User stats
- Source by user

Apache Logs:
- Top 10 geostats
- HTTP methods over time
- ClientIP map
- Number of URI paths
- Stats count by status

## Windows Logs
### Reports

- Signature/ID Report
  - Details signatures and corresponding ID's along with a count for the current log
  ![SIGsreport](https://user-images.githubusercontent.com/109919882/218330728-f78b2178-eae6-4a60-a587-e17974460d55.png)

- Severity Levels Report
  - Displays the count and percentages of each severity level
  ![severitylevels](https://user-images.githubusercontent.com/109919882/218330743-f220841a-8537-4f81-ab59-4f54b35b3ca2.png)

- Windows Activites Report
  - Compares sucessful and failed Windows activites
![windows activites](https://user-images.githubusercontent.com/109919882/218330762-3519037d-0195-4e81-8d0d-2b64fc0ce53c.png)

### Windows Alerts

Name: Failed Windows Activity
  - Description: An alert designed to trigger an email when the designated threshold is reached
 - Baseline: 6
  - Threshold: 7
  - Justification: The average of all the hours, added up and diveded by the number of hours was 6. The alert is set at 7 to trigger unsusal activity, but avoid incessent alerting
  
  Name: Sucessful Logon
    - Description: Alert designed to trigger an email to the company when the hourly count of the signature "an account was sucessfully logged on" reaches designated threshold
    - Baseline: 13.5
    - Threshold: 15
    - Justification: The average successful login count is 13.5. The threshold is set at 15 to ensure an overwhelming amount of sucessful logons is alerted, but enough leniency is given to where the cybersecurity staff is not overwhelemed with sucessful login alerts. The urgency was set to normal
    
 Name: Deleted Account
  - Alert based on corresponding signature ID desinged to trigger an email when threshold is surpassed
  - Baseline: 13
  - Threshold: 14
  - Justification: The average deleted account number is 13. Any amount higher than the allotted threshold of 14 is considered abnormal and trigger an email to "go check" the situation. Priority set to normal
  
  ### Windows Dashboards
  
 ![windowsdifferentsignatures](https://user-images.githubusercontent.com/109919882/218331757-32682eea-3dbf-49c0-9579-f947ec512866.png)
 
 ![windowsdifferentusers](https://user-images.githubusercontent.com/109919882/218331775-0dcc28eb-8eaf-47bf-8203-c59caa600b8a.png)

![windowssourceusers](https://user-images.githubusercontent.com/109919882/218331814-9a4b3158-26c6-48ae-a7c3-c58ef1bcaef7.png)

![signaturevaluesovertime](https://user-images.githubusercontent.com/109919882/218331829-faecd67c-7317-418b-94a6-46153a1bc48f.png)

![uservaluesovertime](https://user-images.githubusercontent.com/109919882/218331902-d8c909ca-dcc8-4c08-8726-b4bd2282dd35.png)

## Apache Logs
### Reports

  - HTTP Methods Report
    - Displays a table of different HTTP Methods (GET, POST, HEAD, OPTIONS)
![HTTPmethods](https://user-images.githubusercontent.com/109919882/218333020-208bf61f-17f9-4b3a-ba78-07db21a16292.png)

  - Top 10 Referrers to VSI Report 
    - Provides the top 10 domains that refer to the VSI website
![Top10VSI](https://user-images.githubusercontent.com/109919882/218333034-fd92aefc-2582-48ae-ba13-c3601d10f8f8.png)

  - HTTP Response Codes Report
    - Details each HTTP Response code along with corresponding counts
![HTTPResponseCodes](https://user-images.githubusercontent.com/109919882/218333087-06d38ab9-f972-4b30-a3a8-2b5c7d2a4cec.png)

### Apache Alerts

Name: Foreign Activity
  - Description: Alert designed to trigger when the threshold is met for hourly activity from any other country other then the US
  - Baseline: 23
  - Threshold: 25
  - Justification: The average baseline is 23. The threshold is set to 25 becuase there is sizeable amount of traffic from foreign places, which should be allowed without triggering, however, anything above 25 is seen as excessive and triggers immediatley

Name: HTTP Post Method Baseline
  - Description: Alert created to trigger an email when the threshold of hourly count of the HTTP POST method is reached
  - Baseline: 1.5
  - Threshold: 3
  - Justification: The average activity is 1.5. The threshold is set at 3 to alert any excessive activity

### Apache Dashboards

![Apachedashboard1](https://user-images.githubusercontent.com/109919882/218333450-21edaf89-87a6-49c8-ade1-baecb94ec408.png)

![apachedashboard2](https://user-images.githubusercontent.com/109919882/218333454-0fc64e8e-e364-489f-99ba-2af3124b0d73.png)

![apachedashboard3](https://user-images.githubusercontent.com/109919882/218333463-31f548af-e307-414f-b721-71fa488dcfb7.png)

![apachedashboard4](https://user-images.githubusercontent.com/109919882/218333470-2bc98e3a-77aa-4e63-9b9a-bd062afa7b06.png)

## Windows Attack Analysis

### Reports

High severity levels increased by 15%. The attack occured at 8am on Wedensday, March 25th, 2020 with a volume increase of 35 events

### Alerts

Alerts indicated a suspiciously high volume increase (16 events, primary user "User_C") in logon attempts at 8am on March 25th, 2020

Vast increase in deleted accounts (17 in total) at 5am on Wednesday, March 25th, 2020

### Dashboards

Suspicious signatures on VSI Windows Server Dashboard
 - 12am to 3am on March 25th, 2020, user accounts were being locked out. The peak number of accounts being locked out hit 896
 - 8am to 11am on March 25th, 2020, account passwords were being reset. The peak number of passwords being reset was a staggering 1,258
 - 10am to 1pm on March 25th, 2020, many accounts were successfully logging in. The peak number of successful log ins totaled 196

Highly worth noting that User A, User K, and User J were the 3 main accounts to hit suspiciously high volumes.  User A’s activity peaked at 745 events between the hours of 1:40am to 2:50am. User K’s activity peaked at 397 between the hours of 9am to 11am, and User J’s activity peaked at 35 between the hours of 10:45am and 12:30pm

![windowsattackdashboard](https://user-images.githubusercontent.com/109919882/218333867-fcd3c59b-bf6e-4c21-a179-4391e784c3aa.png)

## Apache Attack Summary

### Reports

  - Brute force attempt on the VSI login page at 8am on March 25th, 2020
  - Large fluctuation of POST, GET, 404 response code, and the referred domains
  - Drastic increase in POST 404 response
    - Attacker attempted multiple times to use users potentially aquired via social engineering and brute forcing VSI login page

### Alerts

  - Recived an alert for high international activity

### Dashoboards

  - High increase in GET from 5pm to 7pm
    - Peak number: 729
  - High increase in POST from 7pm to 9pm
    - Peak number: 1,296

Brute force attack

![apacheattackdashboard1](https://user-images.githubusercontent.com/109919882/218334570-aaf3cb1c-6fd1-4cf1-b72a-50a43ee2cdc9.png)

![Apacheattackdashboard2](https://user-images.githubusercontent.com/109919882/218334578-6f6c17f4-44db-4a79-b7f6-fc4e1277d7fd.png)

## Summary

After thoroughly combing through VSI’s Window Logs and the Apache Web Server Logs, it was determined that JobeCorp carried out a Brute Force Attack on the log in page for VSI. 

The attack began at 8am on March 25th, 2020, and lasted until 9pm the same day. 

Two user accounts, User A and User K, were the main accounts that were spammed in order to shut down the Web Server and cause users to reach a 404 error code on the log in page

## Mitigations 

  - New alert system that syncs to new dashboards
  - New baselines
  - New policies for multiple failed log in attempts
    - Ex: Locking an account after 5 failed attempts
  - Two way authenticator to mitigate brute force attacks
    - Employees will be required to connect their phone number to the authenticator to strengthen securities 
