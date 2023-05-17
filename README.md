# Streamlining Small Business Private Dining Data Collection for Use In Analytics and Marketing

## Table of Contents

* [Background](#Background)
* [Data Questions](#Data-Questions)
* [Tools and Sources](#Tools-and-Sources)
* [Work Flow](#Flow)


## Background

The motivation for this project came from realizing a need within this small business to streamline data collection and visualization.  Prior to this project, data was pulled off individual tabs within the sales and event management platform and manually entered to make visualizations.  The goal was to make this process much leaner and more efficient while also presenting this small business with different ways of analyzing their data that was not previously available to them.  Allowing different, more complex questions to be asked and answered.

## Data Questions

When do clients inquire about booking an event for a certain month?  Out of those clients, how many of those clients end up booking an event?  What is the total revenue per month per restaurant location based on event type?  Based on previous years inquiry data, when should the business increase marketing and outreach efforts for a certain month?  

## Tools and Sources

Tools
* Python
  - requests
  - pandas
* Ubuntu
  - Via Linode
* SnowFlake
* Tableau

## Sources

* TripleSeat API
* OpenTable API

## Flow

1. Python script was created to call APIs, clean data, and push to cloud database in SnowFlake
2. Ubuntu used to create cronjob that will run the Python script at 09:00 CST daily
3. Tableau was then connected to the SnowFlake cloud database and scheduled to refresh at 10:00
4. Visualizations in Tableau were built to populate based on current date providing fresh, up-to-date metrics

## Next Steps

The next step in this project is to integrate a cloud based POS newly implemented by this small restaurant chain to visualize organic sales data and compare it with private dining sales data.


