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
  - Justification: The average of all the hours, added up and diveded by the number of hours was 6/ The alert is set at 7 to trigger unsusal activity, but avoid incessent alerting
  
  Name: Sucessful Logon
    - Description: Alert designed to trigger an email to the company when the hourly count of the signature "an account was sucessfully logged on" reaches designated threshold
    - Baseline: 13.5
    - Threshold: 15
    - Justification: The average successful login count was 13.5. THe threshold was set at 15 to ensure an overwhelming amount of sucessful logons is alerted, but enough leniency is given to where the cybersecurity staff is not overwhelemed with sucessful login alerts. The urgency was set to normal
    
 Name: Deleted Account
  - Alert based on corresponding signature ID desinged to trigger an email when threshold is surpassed
  - Baseline: 13
  - Threshold: 14
  - Justification: THe average deleted account number was 13. Any amount higher than the allotted threshold of 14 is considered abnormal and trigger an email to "go check" the situation. Priority set to normal
  
  ### Windows Dashboards
  
 ![windowsdifferentsignatures](https://user-images.githubusercontent.com/109919882/218331757-32682eea-3dbf-49c0-9579-f947ec512866.png)
 
 ![windowsdifferentusers](https://user-images.githubusercontent.com/109919882/218331775-0dcc28eb-8eaf-47bf-8203-c59caa600b8a.png)

![windowssourceusers](https://user-images.githubusercontent.com/109919882/218331814-9a4b3158-26c6-48ae-a7c3-c58ef1bcaef7.png)

![signaturevaluesovertime](https://user-images.githubusercontent.com/109919882/218331829-faecd67c-7317-418b-94a6-46153a1bc48f.png)

![uservaluesovertime](https://user-images.githubusercontent.com/109919882/218331902-d8c909ca-dcc8-4c08-8726-b4bd2282dd35.png)
