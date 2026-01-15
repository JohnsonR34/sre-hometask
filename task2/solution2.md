1. Top 5 IP addresses requests come from:
Answer: 0
Command:
awk '{print $1}' access.log | sort | uniq -c | sort -nr

---

2. Number of requests with '50X' and '200' HTTP response codes:

Answer:
    50X - 21
    200 - 53

Command:
 To find 200:
    awk '{print $11}' access.log | sort | uniq -c | grep 200 
 
 To find 50X:
    awk '{print $11}' access.log | sort | uniq -c | grep -e 50.
 
 To find count all the response codes"
    awk '{print $11}' access.log | sort | uniq -c


---

3. Number of requests per minute:

Answer: 
 1 Requests per minute, except on Jan 09 2026  22:04. Two requests on that time. 

Command"
 awk -F'[][]|[:,]' '{c[$2" "$3":"$4]++} END {for (m in c) print c[m], m}' access.log | sort -nr


---

4. Which method is the most frequent one?

Answer:
 GET - 91 times
Command: 
 awk '{print $8}' access.log | sort | uniq -c

---

5. Any other improvements you can recommend to server admin based on the access log

Answer: 
I would recommend the server admin to visualize the logs, to monitor them easily. 

Your thoughts on the last question:
The last question, is to analyze the scenario and fix it depending on the scenario.  A server admin is responsible for maintaining the webserver. By checking the access logs, I would suggest the server admin to visualize the data. It would be easier to check the logs, set alerts,  monitor the webserver.  For example, in case of a DDos attack it will be easier to locate when the breach started. 


 
    
