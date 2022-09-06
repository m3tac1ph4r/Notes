# Projects



### 1. Cowin Notifier

DIvided my project in three parts.
1. Helper.py
2. Vaccine.py
3. Main.py

**helper.py :** This was the file which was having all the functions which are used frequently.
* filter_message() : there I checked the message entered by the user is command or state or district or age otherwise he/she entered the wrong data.
* And there are functions which will send the message the command options or state list or district list using telegram api. 
* user_data() : saves user data in the json file and update the data if user is already added.
* get_chat_id(dname) : return all the user's chat_id who are of that district.
* get_vax_info(dname) : return the vaccine availability information of that district

**vaccine.py :** This file handles when to send vaccine information to all the users. Because of API limit we have to take pause and then send update about the vaccine to users.
And this send message to the user after every three hours. But I have seen that vaccines slots are updated by the goverment after 10:00AM before 12 noon. So this specifically checks at that time.

**main.py :** This files handles all the input send the by the user through telegram



### 2. iNoteBook

iNoteBook is a daily note taking application. It also has a functionality of USER LOGIN and SIGNUP. I created a REST API to interact client with server. I used hooks such as **useState**

##### Backend :
Created two paths i.e  auth.js and notes.js




### 2. Fitness Club
Fitness club is a web application for fitness inclined people . It includes various body part exercises also it provides youtube sample videos for that exercise. I used exerciseDB API for fetching the information about exercises. And Youtube API for fetching the sample videos of the exercises. 