Incident report for 504 error / Site Outage
Summary
On the 17th of April, 2023 at 5:00PM,the server went down,and users were getting a 500 error as they were unable to get server resources

Timeline
17:00 WAT - 500 error 
17:05 WAT - Ensuring Apache and MySQL are up and running.
17:10 WAT - The website was not loading properly which on background check revealed that the server was working properly as well as the database.
17:12 WAT - After quick restart to Apache server returned a status of 200 and OK while trying to curl the website.
17:18 WAT - Reviewing error logs to check where the error might be coming from.
17:25 WAT - Check /var/log to see that the Apache server was being prematurely shut down. The error log for PHP were nowhere to be found.
17:30 WAT - Checking php.ini settings revealed all error logging had been turned off. Turning the error logging on.
17:32 WAT - Restarting apache server and going to the error logs to check what is being logged into the php error logs.
17:36 WAT - Reviewing error logs for php revealed a mistyped file name which was resulting in incorrect loading and premature closing of apache.
17:38 WAT - Fixing file name and restarting Apache server.
17:40 WAT - Server is now running normally and the website is loading properly.
Root Cause and Resolution
The issue was connected with a wrong file name being reffered to in the wp-settings.php file. The error was raised when trying to curl the server, wherein the server responded with 500 error. By checking the error logs it was found that no error log file was being created for the php errors and reading the default error log for apache did not result in much information regarding the premature closing of the server. Once understood that the errors for php logs were not being directed anywhere the engineer chose to review the error log setting for the php in the php.ini file and found that all error logging was turned off. Once turned on, the error logging the apache server was restarted to check if any errors were being registerd in the log. As suspected, the php log showed that a file with a .phpp extension was not found in the wp-settings.php file. This was clearly a misspelled error that resulted in the error to site access. As this was one server that the error was found in, this error might have been replicated in other servers as well. An easy fix by changing the file extension by puppet would result in the fix being made to other servers as well. A quick deployment of the puppet code replaced all misspelled file extensions with the right one and restarting of the server resulted in properly loading of the site and server.

Corrective and Preventive Measures
Servers were installed with NPM platforms, to monitor logs and alarms, making future troubleshooting easy, also facilitating efficient O&M
