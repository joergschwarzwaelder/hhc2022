
# Objective 1: Wireshark Practice
**Location: Tolkien Ring**  
**Elf: Sparkle Redberry**

This objective is about getting familiar with the analysis of network packet captures using Wireshark.

1. What type of objects can be exported from this PCAP?
2. What is the file name of the largest file we can export?
By navigating to "File / Export Objects / HTTP" we can see, that **app.php** is the largest object.

3. What packet number starts that app.php file?
 
![Screenshot from Wireshark](https://github.com/joergschwarzwaelder/hhc2022/blob/main/Objective-2/objective%202-3.png)

Packet **687**

4. What is the IP of the Apache server?

![Screenshot from Wireshark](https://github.com/joergschwarzwaelder/hhc2022/blob/main/Objective-2/objective%202-4.png)

**192.185.57.242**

5. What file is saved to the infected host?

![Screenshot from Wireshark](https://github.com/joergschwarzwaelder/hhc2022/blob/main/Objective-2/objective%202-5.png)

**Ref_Sept24-2020.zip**

6. Attackers used bad TLS certificates in this traffic. Which countries were they registered to? Submit the names of the countries in alphabetical order separated by commas (Ex: Norway, South Korea).
The used certificates were registered to the following countries:
 - IL - Israel
 - SS - South Sudan
 - US - United States of America

** Israel, South Sudan, United States of America**

7. Is the host infected (Yes/No)?
**Yes**
 - 

**Achievement: Wireshark Practice**
