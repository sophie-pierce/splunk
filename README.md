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
- Severity Levels Report
  - Displays the count and percentages of each severity level
- Windows Activites Report
  - Compares sucessful and failed Windows activites

