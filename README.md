# IsraelPassportBooking
A tool that allows users to choose a Ministry of the Interior Office to make a booking without a long waiting time


# Background
I discovered early in 2022 that one of my daughter's Israeli passport had expired. I wanted to renew it quickly, and at the time the only option to secure a reservation was on the [web application](https://myvisit.com/#!/home/signin/). I logged in with her details and selected our local office and discovered an unacceptable waiting time. 

After returning to the earlier page- I discovered that the flow was really bad. 
The first login required a two-factor authentication (Teudat Zehut / ID Number) and mobile phone number. 
I needed to log in each time I wanted to select a new office, each time requiring the entry of the same ID number (Teudat Zehut) and phone number from before. 
This flow was really frustrating and about 5 sites I decided to automate the process.

# Reverse engineering the booking application (Notes from after building the script. Verify and update)
The Engish language goverment site [Schedule an appointment to issue biometric documents](https://www.gov.il/en/Departments/news/schedule_appointment_for_biometric_docs) links to the web application to book an appointment [web application](https://myvisit.com/#!/home/signin/). 

The logging into the web application requires the creation of an account with phone number and a Capcha. A text message with a one-time password is sent, and you need to enter the one-time code 

A provider is selected and a location is selected. The service is selected. Enter ID Number. Enter Phone Number. Choose the service Darcon Biometri / biometric passport.

You then receive a list of Available Dates that show the Available times when you click on them.

# Initial Automation Solution
In the browser manually perform the first login and find your way the Available Date picker for one location.

(Google Chrome) Right click and press 'inspect' which should bring up the source and a few other options. Reload a date while observing the network traffic. Copy out the authorization from the "request headers" and save it in a text editor. 

Open up the [juypter notebook](http://todo) and paste in the token 'JWT lots_of_characters', your phone number and teudat zehut and run all the cells.
Optionally, update your home coordinates to sort by nearest office first. 
A table will print the next 10 days for each office, where appointments exist and how many appoinments exist.

Return to the web application and browse to the date of interest and make a booking.

