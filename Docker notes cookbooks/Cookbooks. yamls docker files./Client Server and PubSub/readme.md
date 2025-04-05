Long tasks such as file upload or too many requests to web server causes issues such as package drops and delays.  
We can place a intermediate broker between the client(browser) and the server(s).  

![diagram](<Broker and worker server.drawio.svg>)  
<br>

- Usually the *Browser* would send a *Req* to *WebServer*. But here it will communicate with the *Broker* and '*Publish*' the request to the broker.
- Broker will send the message it has received to all everyone who has subscribed to it. Here the WebServer has Subscribed to the broker.
- After getting the task and finishing it, *WebServer* will Publish(*Pub*) a reply to the broker. Or, it can also **send** a reply to the client browser via another *Notify* API which the client Browser will keep listening to in order to know if the task has been completed or not.

