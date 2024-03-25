# Exploring Network Malware Infection


## TASK: Write an incident report based on the pcap and alerts. 

The incident report should contain the following: 

• Executive Summary 

• Details of the infected Windows host

• Indicators of Compromise (IOCs) 

• Analysis Findings

![](https://github.com/yvesstan/Detection-Lab/blob/main/1.png)

![](https://github.com/yvesstan/Detection-Lab/blob/main/2.png)

![](https://github.com/yvesstan/Detection-Lab/blob/main/3.png)

![](https://github.com/yvesstan/Detection-Lab/blob/main/4.png)

As i practice pcaps, i found out a way to make it more easier and relevant on which procedure to take first. I like to check for conversations IPv4 sort the bytes same thing with TCP and UDP. I immediately got interested with IP address of 192.168.1.216 and 2.56.57.108 because they have the most bytes even in Endpoints.

![](https://github.com/yvesstan/Detection-Lab/blob/main/5.png)

![](https://github.com/yvesstan/Detection-Lab/blob/main/6.png)

I found some malicious activity by sorting the destination port and i found port 80 INFO POST /osk//1.jpg up to 7. Checked the tcp stream and found interesting things.

![](https://github.com/yvesstan/Detection-Lab/blob/main/7.png)

I also checked out the CNameString to find the user and the Host. Since it has the most activity among every other IP address in this pcap file, In this case the name is steve.smith with DESKTOP-GXMYNO2$ the mac address i found was 95:5c:8e:32:58:f9.



![](https://github.com/yvesstan/Detection-Lab/blob/main/8.png)

![](https://github.com/yvesstan/Detection-Lab/blob/main/9.png)

With all the information i found, I wanted to check Wireshark's object list for http since we found some tcp stream indicating "POST" with ".JPG" and then i found downloadable files. I downloaded each file get their file hashes.

![](https://github.com/yvesstan/Detection-Lab/blob/main/10.png)

![](https://github.com/yvesstan/Detection-Lab/blob/main/11.png)

![](https://github.com/yvesstan/Detection-Lab/blob/main/12.png)


I found some info on the files using VirusTotal and checked the properties of each file to see if I can find more interesting things but in this case I just saved the sizes of each file.




