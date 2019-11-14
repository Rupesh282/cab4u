# Cab4U

This is a project for SSL Lab CS213 at IIT Dharwad (Autumn 2019) by Team 14. Aim is to create website application for cab booking which handles the both driver and passenger.

## Core Team members
* Akhilesh Bharatwaj
* Brahmadevara Sai Yashwanth
* Paritosh Gavali
* Rupesh Kalantre

## Project Problem

**Passenger** should be allowed to login into the system. He/she should be allowed to book a cab. He/she should be notified wether the any driver has acccepted his/her request or else *no cab available* should be displayed. After the ride is completed he/she should have the option to verfy the same.

**Driver** should get all the requests from passenger near him along with information like Starting position,End position, Passenger name, and fare.He/She should have the option to choose or not choose a single passenger near him/her. As soon as driver has reached the end position he can end the ride. 

Both passenger and driver should have a mechanism of payment. And as soon the ride gets completerd fare should be deducted form the passenger and should be added to the driver.



## Project Implementation

This website application is being hosting it onto a server which runs on apache2. Rest of the users are clients of the server.
If a passenger books his/her ride from the locations provided. Fare of this ride is calculated if the fare is more than the money passenger has in wallet the request for cab is denied. In such a case passenger has to add money from in his wallet by credit card. After the fare check a open job query is generated in SQL table with list of all the drivers who are eligible (drivers who are near 1 km range from the starting point). This notification is given to the driver on which he can accept it or leave it open. It driver accepts the job, the job is marked as assigned so that it will be removed from other driver's list. Now, passenger will be given the information about the driver. Driver can confirm that he has reached the starting position. After we reach at the destination both driver and passenger have to confirm this information. After conformation fromn both sides we deduct money from passenger's wallet and add it into driver's wallet. Now the job query which was generated is marked as closed and is add to the history.

## How to use

### Passenger
* Passenger should make an account on our website providing details of his/her name, unique username, a password.
* Passenger dashboard has the following features : 
    * Profile - user can view his profile.
    * History - to view his past cab rides
    * Wallet - to add money to his wallet
    * Logout
    * Booking snippet
    * Visualisation of the journey

### Driver
* Driver should make an account on our website if he doesn't have any.
* Driver dashboard has the following features :
    * Profile - user can view his profile.
    * History - to view his past service
    * Logout
    * Notification page

## Setup
This website should be hosted on a apache2 server. The server should have some SQL table for appliacitons working.
Enter the following command in the SQL command line to make the required SQL table for the site.
    
        create database cab4u;
        create table driver (name varchar(120),username varchar(120),password varchar(120),isBusy tinyint(1),wallet int(4),online tinyint(1),x double,y double);
        create table passenger (name varchar(120),username varchar(120),password varchar(120),wallet int(4),online tinyint(1));
        create table location (location int(4),x double,y double,place varchar(120));
        create table notification(p_username varchar(120),d_username varchar(120),initial int(11),final int(11), fare int(11));
        create table history(p_username varchar(120),d_username varchar(120),initial int(11),final int(11), fare int(11));

* You need to add location maually to the *location table* in SQL.
* <br>Update cab4u/pari/database.php and cab4u/login_info.php according to your system.
