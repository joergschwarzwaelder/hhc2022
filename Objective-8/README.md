
# Objective 8: Boria PCAP Mining
**Location: Web Ring**  
**Hints (3x) from Alabaster Snowball**

This objective is about getting familiar with the analyzing an attack using a web server log and a PCAP network trace.

The data is provided in a ZIP file: https://storage.googleapis.com/hhc22_player_assets/boriaArtifacts.zip

### Objective: Naughty IP
According to the web server log, **18.222.86.32** is the naughty IP address.

### Objective: Credential Mining
The first username tried in the brute force attack is **alice** (from packet #7279, username: alice, password: philip)

### Objective: 404 FTW

The first successful URL path in the forced browsing attack is **/proc** (log entry #2322)

### Objective: IMDS, XXE, and Other Abbreviations

http://169.254.169.254/latest/meta-data/identity-credentials/ec2/security-credentials/ec2-instance (packet #32918)

**Achievement: Boria PCAP Mining**
