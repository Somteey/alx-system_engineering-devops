# 0x19-postmortem
![MasterHead](https://my.tradeinvalet.com/Content/Images/Error_Image.gif)
<br><br>
## Issue Summary:
On the 3rd of march between the hours of 1:00pm and 2:30pm, All requests to the payment gateway service container responded with a 500 server error, which affected more than 50% of the user of the application as more users couldn't process their payment for items added to their chart. The server error was caused by inadequate catch to error in a try/except block

## Timeline (West Africa Time)
* 1:00pm: Code pushed to production server
* 1:05pm: Code deployed
* 1:45pm: first error alert recived from monitoring team
* 1:47pm: HTTP request sent to the service and recived 500 error
* 1:50pm: Source Code was diagnosed and cause or error discovered by support engineer
* 1:51pm: Error fixed and code pushed for testing by backend team lead
* 1: 55pm: Code pushed to deployment server and deployed
* 2:00pm: Server up and running


## Root cause and resolution
![MasterHead](https://i.imgur.com/r1eVdVy.gif)
<br><br>

The root cause of the problem was that a try and except block was used but not all exceptions were captured, a value error occured which was initially missed and led to the server error, this was missed as a result of inadequate testing for all posibilities before deploying

## Corrective and preventative measures
The prevent future occurence of such incidence, more test cases have been added to cover a wider range of possibilities and test before being deployed to production.