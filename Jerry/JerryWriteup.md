### Larry Liu's Box Writeup | Jerry

Jerry was the first box I attacked and introduced me to the basic mindset and process of pentesting.

## Enumeration

To begin, I ran the following command to quickly scan to ports of the box (its IP was **10.10.10.95**):
- nmap -Pn -n -vv --open -T4 10.10.10.95
The command returned one open tcp port at 8080
![Image1](/Images/Image1)
I then got more detailed information about the port by running:
- nmap -Pn -n -p 8080 -vv --open -sV -sC -T4 10.10.10.95
![Image2](/Images/Image2)
From this, I found that the box was running Apache Tomcat, which I realized was a web application server upon further research.
Since the port was an open port that services http connections, I connected to it directly by putting http://10.10.10.95:8080 in my browser.
![Image3](/Images/Image3)
From here, I clicked on the manager webapp link, which took me to the following screen after I couldn't log in.
![Image4](/Images/Image4)
Due to the box's difficulty, I assumed that the manager login was information was the were the defaults, and used them to log into the manage webapp.
![Image5](/Images/Image5)
In the management screen, there was a WAR file deployment area. This led me to assume that there were exploits available using this functionality to give attackers remote shells.
I searched up "tomcat reverse shell exploit," and found the **exploit/multi/http/tomcat_mgr_upload exploit**.
![Image6](/Images/Image6)
Using the exploit and putting in the credentials from earlier, I gained access to the machine. From there, I navgated to the Desktop of the admin user and found the flags.
![Image7](/Images/Image7)
![Image7](/Images/Image8)
