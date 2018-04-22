# Project 8 - Pentesting Live Targets

Time spent: **20** hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:
* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each version of the site has been given two of the six vulnerabilities. (In other words, all six of the exploits should be assignable to one of the sites.)

## Blue

Vulnerability #1: SQLI Attack

<img src='SQLI Attack.gif' title= 'Sqli Attack' width='' alt='' />

This vunerability was investigated based on the ending of the url(.php?id=4) that was seen when a specific user was selected from under Salesperson.
This was first tested on the Red target by entering 'x=x'which presented no response but when this was attempted on the Blue Target specifically 
```' or 'x=x'``` which yielded a database query failed response which indicated the Blue target is vunerable to SQLI atatcks.

Vulnerability #2: Session Hijack

<img src='Session Hijacking.gif' title= 'Session Hijacking' width='' alt='' />

This vunerability was investigated by first opening the Blue target and trying to login with the provided username and password.
Utilizing the the PHP script provided ```public/hacktools/change_session_id.php``` the session was obtained. This was then copied and used in another
another browser with that was the login page for the Blue Target. The php script was used in this new browser used to open and show the current session id
on the new browser. The session in the first browser was then copied to the new browser and chnaged. Following this, an attempt was made to login on the new
browser. Upon hitting the login button the second browser was succefully logged in without having to provide a username or password.



## Green

Vulnerability #1: Cross Site Scripting

<img src='Cross Site Scripting.gif' title= 'Cross Site Scripting' width='' alt='' />

This vunerability was investigated based on looking through the content management system of the site once logged in. From the Green target main page click 
Contact, which brought to a page allowing you to enter text into three different fields namely, Your name, Your email and Feedback. When the following script
``` <script>alert('Jaydozrock found the XSS!!!');</script> ``` is entered both under name and feedback and submitted, upon returning to the login page and 
succesfully logging in, hitting the feedback button will display the message stored withing the script indicating an xss vunralbility.




Vulnerability #2: Username Enumeration

<img src='Username Enumeration.gif' title= 'Username Enumeration' width='' alt='' />

This vunerability was investigated by attempting different usernames and observing the response that was given on the page through burp. It was noticed that when 
an incorrect username was given the result given under span class was "failed" whereas when the correct username was used with an incorrect password, the result under 
span class was " failure". This observation is enough to indicate a vunerabilty and would support further investigation into finding a suitable attack to gain access.




## Red

Vulnerability #1: Cross Site Request Forgery

<img src='Cross Site Request Forgery.gif' title= 'Cross Site Request Forgery' width='' alt='' />

This vunerability was investigated by attempting to edit information seen under Salepeople, specifcally the generated csrd_token . When this was attemtpted on the Green target 
the result was an error specifically "Error:Invalid request". On the otherhand when this was done on the Red target, despite the csrd_token being changed edits were still
able to be made on Salesperson list in the Red Target.




Vulnerability #2: Insecure Direct Object Reference

<img src='Insecure Direct Object Reference.gif' title= 'Insecure Direct Object Reference' width='' alt='' />

This vunerability was investigated by changing the id index for individuals under the Salesperson list. Upon trying to change the the id index in the Green target by changing 
the A seen in the follwing text to 10 or 11``` public/salesperson.php?id=A ``` , returned/reloaded the page that had the intial salesperson list. On the otherhand when this was attempted
with Red target this presented two users that were not present on the Salesperson list page.



## Notes

Describe any challenges encountered while doing the work
