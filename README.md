# Exploring Network Malware Infection


## TASK: Write an incident report based on the pcap and alerts. 

The incident report should contain the following: 

• Executive Summary 

• Details of the infected Windows host

• Indicators of Compromise (IOCs) 

• Analysis Findings

![](https://github.com/yvesstan/Detection-Lab/blob/main/images/1.png)

![](https://github.com/yvesstan/Detection-Lab/blob/main/images/2.png)

![](https://github.com/yvesstan/Detection-Lab/blob/main/images/3.png)

![](https://github.com/yvesstan/Detection-Lab/blob/main/images/4.png)

As i practice pcaps, i found out a way to make it more easier and relevant on which procedure to take first. I like to check for conversations IPv4 sort the bytes same thing with TCP and UDP. I immediately got interested with IP address of 192.168.1.216 and 2.56.57.108 because they have the most bytes even in Endpoints.

![](https://github.com/yvesstan/Detection-Lab/blob/main/images/5.png)

![](https://github.com/yvesstan/Detection-Lab/blob/main/images/6.png)

I found some malicious activity by sorting the destination port and i found port 80 INFO POST /osk//1.jpg up to 7. Checked the tcp stream and found interesting things.

![](https://github.com/yvesstan/Detection-Lab/blob/main/images/7.png)

I also checked out the CNameString to find the user and the Host. Since it has the most activity among every other IP address in this pcap file, In this case the name is steve.smith with DESKTOP-GXMYNO2$ the mac address i found was 95:5c:8e:32:58:f9.



![](https://github.com/yvesstan/Detection-Lab/blob/main/images/8.png)

![](https://github.com/yvesstan/Detection-Lab/blob/main/images/9.png)

With all the information i found, I wanted to check Wireshark's object list for http since we found some tcp stream indicating "POST" with ".JPG" and then i found downloadable files. I downloaded each file get their file hashes.

![](https://github.com/yvesstan/Detection-Lab/blob/main/images/10.png)

![](https://github.com/yvesstan/Detection-Lab/blob/main/images/11.png)

![](https://github.com/yvesstan/Detection-Lab/blob/main/images/12.png)

I found some info on the files using VirusTotal and checked the properties of each file to see if I can find more interesting things but in this case I just saved the sizes of each file.

![](https://github.com/yvesstan/Detection-Lab/blob/main/images/13.png)

I checked the IP address of 2.56.57.108 and VirusTotal showed me that it was malicious.

![](https://github.com/yvesstan/Detection-Lab/blob/main/images/14.png)


With more investigation in wireshark, I couldn't find the source of the malicious IP address so i went to google and luckily I found the website and what the malware is which is OskiStealer.


## Executive Summary

Date: 2024-03-25 at approximately 16:07 GMT, a Windows user named Anth Edwards was infected with OskiStealer Malware.

### Details of the Infected Host:

MAC address: 95:5c:8e:32:58:f9 Host name: DESKTOP-GXMYNO2

IP address: 192.168.1.216 Windows user account: anth.edwards

### Indicators of Compromise (IoC's)
#### Malicious Traffic:
2.56.57.108 port 80 - 2.56.57.108 - POST /osk//main.php HTTP/1.1

2.56.57.108 port 80 - 2.56.57.108 - POST /osk//1.jpg HTTP/1.1

2.56.57.108 port 80 - 2.56.57.108 - POST /osk//2.jpg HTTP/1.1

2.56.57.108 port 80 - 2.56.57.108 - POST /osk//3.jpg HTTP/1.1

2.56.57.108 port 80 - 2.56.57.108 - POST /osk//4.jpg HTTP/1.1

2.56.57.108 port 80 - 2.56.57.108 - POST /osk//5.jpg HTTP/1.1

2.56.57.108 port 80 - 2.56.57.108 - POST /osk//6.jpg HTTP/1.1

2.56.57.108 port 80 - 2.56.57.108 - POST /osk//7.jpg HTTP/1.1

2.56.57.108 port 80 - 2.56.57.108 - POST /osk/ HTTP/1.1 (zip)


### Analysis Findings

Files that are associated with the infection:

File location: http://2.56.57.108/osk//1.jpg

File size: 645,592 bytes

SHA256 hash: 16574f51785b0e2fc29c2c61477eb47bb39f714829999511dc8 952b43ab17660

File type: PE32 executable (DLL) (console) Intel 80386, for MS Windows

File description: sqlite3.dll 

File location: http://2.56.57.108/osk//2.jpg

File size: 334,288 bytes

SHA256 hash: a770ecba3b08bbabd0a567fc978e50615f8b346709f8eb3cfacf 3faab24090ba

File type: PE32 executable (DLL) (GUI) Intel 80386, for MS Windows

File description: freebl3.dll 

File location: http://2.56.57.108/osk//3.jpg

File size: 137,168 bytes

SHA256 hash: 3fe6b1c54b8cf28f571e0c5d6636b4069a8ab00b4f11dd842cfe c00691d0c9cd

File type: PE32 executable (DLL) (GUI) Intel 80386, for MS Windows

File description: mozglue.dll

File location: http://2.56.57.108/osk//4.jpg

File size: 440,120 bytes

SHA256 hash: 334e69ac9367f708ce601a6f490ff227d6c20636da5222f148b2 5831d22e13d4

File type: PE32 executable (DLL) (console) Intel 80386, for MS Windows


File description: msvcp140.dll 

File location: http://2.56.57.108/osk//5.jpg

File size: 1,246,160 bytes

SHA256 hash: e2935b5b28550d47dc971f456d6961f20d1633b489299875014 0e0eaa9ae9d78

File type: PE32 executable (DLL) (GUI) Intel 80386, for MS Windows

File description: nss3.dll 

File location: http://2.56.57.108/osk//6.jpg

File size: 144,848 bytes

SHA256 hash: 43536adef2ddcc811c28d35fa6ce3031029a2424ad393989db3 6169ff2995083

File type: PE32 executable (DLL) (GUI) Intel 80386, for MS Windows

File description: softokn3.dll

File location: http://2.56.57.108/osk//7.jpg

File size: 83,784 bytes

SHA256 hash: c40bb03199a2054dabfc7a8e01d6098e91de7193619effbd0f14 2a7bf031c14d

File type: PE32 executable (DLL) (console) Intel 80386, for MS Windows

File description: vcruntime140.dll


## Conclusion:
The IP address 2.56.57.108 is associated with an EXE sample tagged as OskiStealer at bazaar.abuse.ch, Having a pattern or learning where to start finding things in Network 

Analysis might be very helpful and crucial at times. The more you handle Pcap's the more easier to make that pattern, but of course it still depends/vary on the 

situation/scenario.



I found some info on the files using VirusTotal and checked the properties of each file to see if I can find more interesting things but in this case I just saved the sizes of each file.




