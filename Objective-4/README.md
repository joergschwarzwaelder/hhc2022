
# Objective 4: Suricata Regatta
**Location: Tolkien Ring / Suricata Regatta Terminal**  
**Hints from Dusty Giftwrap**

This objective is about getting familiar with the [Suricata](https://suricata.io/) open source network analysis and threat detection software.


1. First, please create a Suricata rule to catch DNS lookups for adv.epostoday.uk.

Whenever there's a match, the alert message (msg) should read **Known bad DNS lookup, possible Dridex infection**.

```alert dns any any -> any any (msg:"Known bad DNS lookup, possible Dridex infection"; dns.query; content:"adv.epostoday.uk"; nocase; sid:1;)```

  

2. Develop a Suricata rule that alerts whenever the infected IP address 192.185.57.242 communicates with internal systems over HTTP. 

When there's a match, the message (msg) should read **Investigate suspicious connections, possible Dridex infection**

```alert http 192.185.57.242 any <> any any (msg:"Investigate suspicious connections, possible Dridex infection"; sid:242342;rev:1;)```

  

3. We heard that some naughty actors are using TLS certificates with a specific CN.

Develop a Suricata rule to match and alert on an SSL certificate for heardbellith.Icanwepeh.nagoya. 

When your rule matches, the message (msg) should read **Investigate bad certificates, possible Dridex infection**

  

```alert tls any any <> any any (msg:"Investigate bad certificates, possible Dridex infection"; tls.cert_subject; content: "CN=heardbellith.Icanwepeh.nagoya"; nocase; sid:242343;rev:1;)```

  

4. Let's watch for one line from the JavaScript: let byteCharacters = atob 

Oh, and that string might be GZip compressed - I hope that's OK!
Just in case they try this again, please alert on that HTTP data with message Suspicious JavaScript function, possible Dridex infection  

```alert http any any <> any any (msg:"Suspicious JavaScript function, possible Dridex infection"; http.response_body; content:"let byteCharacters = atob"; sid:242345;rev:1;)```

**Achievement: Suricata Regatta**
