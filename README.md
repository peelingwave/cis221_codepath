# Project 8 - Pentesting Live Targets

Time spent: **X** hours spent in total

> Objective: Identify vulnerabilities in three different versions of the Globitek website: blue, green, and red.

The six possible exploits are:

* Username Enumeration
* Insecure Direct Object Reference (IDOR)
* SQL Injection (SQLi)
* Cross-Site Scripting (XSS)
* Cross-Site Request Forgery (CSRF)
* Session Hijacking/Fixation

Each color is vulnerable to only 2 of the 6 possible exploits. First discover which color has the specific vulnerability, then write a short description of how to exploit it, and finally demonstrate it using screenshots compiled into a GIF.

## Blue

Vulnerability #1: __________________

Description:

<img src="blue-vuln1.gif">

Vulnerability #2: __________________

Description:

<img src="blue-vuln2.gif">

## Green

Vulnerability #1: XSS

Description: I'm able to post a script inside the Red Contact Form that executes a pop up. While the popup is harmless, its a proof of concept that can be leveraged to do malicious activity. The specific script I used was <script>alert('Greetings from Marvin@c0d3p4th!');</script> 

![SQLi_green_contact_form](https://user-images.githubusercontent.com/98624766/163739016-5ff69656-0cce-48a9-87be-b4147b2adc8f.gif)
![SQLi_green_contact_form](https://user-images.githubusercontent.com/98624766/163739032-ee499643-6f75-4464-9812-396b93429ab4.png)

<img src="green-vuln1.gif">

Vulnerability #2: 

Description: 

<img src="green-vuln2.gif">

## Red

Vulnerability #1:Username enumeration

Description: The developer created a different response for a username that exists in their database vs one that does not exists. This difference will allow bad actors to exploit the vuln, for ex. to be able to brute force username/passwords more efficiently. The developer should have created an identical response for both valid and invalid username input. 

![Username_enumeration_vuln_red](https://user-images.githubusercontent.com/98624766/163844373-8d2b64f3-eab2-43af-b0dd-f2d23f500a6c.gif)
<img src="red-vuln1.gif">

Vulnerability #2:  IDOR

The developer left anyone the ability to manipulate  a URL parameter, in this case id=x, in order to directly access a user that is only supposed to be accessed by a logged in authorized user/admin. The id=10 and id=11 references 2 users that are not listed on the public facing page and should not be accessible to the public. Access control in the session management was not implemented. 

![IDOR_vuln-red](https://user-images.githubusercontent.com/98624766/163856745-d51886ef-2ed1-4e7c-8c20-2c3ce23aa086.gif)

## Notes

Describe any challenges encountered while doing the work

