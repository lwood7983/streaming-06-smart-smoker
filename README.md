Loni Wood  

February 8, 2023
## Creating a Producer and Consumer

# Overview:
The purpose of this code is to take a csv file and create a producer with three queues.  Each column of the csv will be sent to individual queues.  You will also be creating 3 consumers.

# Before you begin
Before you being running, be sure you have the following installed and running.
- pika
- deque
- RabbitMQ:
    You can find additional information on how to set up RabbitMQ at: https://www.rabbitmq.com/download.html
- active conda environment
- open anaconda prompt terminal

# How to run this program:
## Files you will be using:
 - bbq_producer.py
     - You will need to review the following and make updates if needed:
        - Check your host.  If it is not the "localhost", update
        - Determine if you would like to have the RabbitMQ website prompt you to open. If you do, ensure that show_offer is set to True, otherwise set it to False.
 
 - smoker-temps.csv
     - There are 4 columns in this csv file
        - Time = Date-time stamp for the sensor reading
        - Channel1 = Smoker Temp
        - Channel2 = Food A Temp 
        - Channe3 = Food B Temp 

 - smoker_consumer.py
    - You will need to review the following ane make updates if needed:
      - Check your host.  If it is not the "localhost", update

 - food_a_consumer.py
    - You will need to review the following ane make updates if needed:
      - Check your host.  If it is not the "localhost", update

 - food_b_consumer.py
    - You will need to review the following ane make updates if needed:
      - Check your host.  If it is not the "localhost", update

- Additional Notes:  The bbq_producer.py has skipped over any blank rows so therefore there will be no blank rows sent to the consumers. 

# Assignment - Smart Smoker 

## Using a Barbeque Smoker
When running a barbeque smoker, we monitor the temperatures of the smoker and the food to ensure everything turns out tasty. Over long cooks, the following events can happen:

## The smoker temperature can suddenly decline.
The food temperature doesn't change. At some point, the food will hit a temperature where moisture evaporates. It will stay close to this temperature for an extended period of time while the moisture evaporates (much like humans sweat to regulate temperature). We say the temperature has stalled.
 

## Sensors
We have temperature sensors track temperatures and record them to generate a history of both (a) the smoker and (b) the food over time. These readings are an example of time-series data, and are considered streaming data or data in motion.

 
## Streaming Data
Our thermometer records three temperatures every thirty seconds (two readings every minute). The three temperatures are:

 - the temperature of the smoker itself.
 - the temperature of the first of two foods, Food A.
 - the temperature for the second of two foods, Food B.
 

## Significant Events
We want know if:

The smoker temperature decreases by more than 15 degrees F in 2.5 minutes (smoker alert!)
Any food temperature changes less than 1 degree F in 10 minutes (food stall!)
 
## Smart System
We will use Python to:

Simulate a streaming series of temperature readings from our smart smoker and two foods.
Create a producer to send these temperature readings to RabbitMQ.
Create three consumer processes, each one monitoring one of the temperature streams. 
Perform calculations to determine if a significant event has occurred.

## Consumer Requirements
We need to set up our consumers to account for the following:
- Alert to Send:
  - The smoker temperature decreases by more than 15 degrees F in 2.5 minutes (smoker alert!)
  - Any food temperature changes less than 1 degree F in 10 minutes (food stall!)

- Time Windows:
  - Smoker time window is 2.5 minutes
  - Food time window is 10 minutes

- Deque Max Length:
  - At one reading every 1/2 minute, the smoker deque max length is 5 (2.5 min * 1 reading/0.5 min)
  - At one reading every 1/2 minute, the food deque max length is 20 (10 min * 1 reading/0.5 min) 

- Condition To monitor:
  - If smoker temp decreases by 15 F or more in 2.5 min (or 5 readings)  --> smoker alert!
  - If food temp change in temp is 1 F or less in 10 min (or 20 readings)  --> food stall alert!

## Optional: Alert Notifications
Optionally, we can have our consumers send us an email or a text when a significant event occurs. 
You'll need some way to send outgoing emails. I use my main Gmail account - other options are possible. 

# Screenshots of Program Running:
## Screenshot in Anaconda Prompt
![smoker_on_anaconda](smoker_anaconda.png)

## Screenshot in RabbitMQ
![smoker_on_rabbitmq](smoker_rabbit.png)

# Screenshot of the Producer and 3 Consumers running:
Running producer and consumers.  Image below shows all 4 terminals running along with RabbitMQ running the queues.

![Consumers_running_with_rabbitmq](RabbitMQ_running.png)

Running producer and consumers. Image below shows all 4 terminals running with alert messages. Set time to 1/2 second in order to capture the images.
!
[Consumers_with_alerts](Producer&Consumers.png)

