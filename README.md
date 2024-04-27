In this instance we are tasked with dealing with an infiltrator using reverse shell to extract valuable data from our network. We will be using snort to sniff him out and create an IDS rule to stop him.

1. First things first we need to in snort on our ubuntu machine is sudo snort -v -l . to sniff our network and save a log of it.
2. I notice a frequent occurence of exfiltration from port 4444 a common reverse shell port, we use snort -r (packet file) -X | grep :4444 to show only packets where the the suspected port appears.
   
![1](https://github.com/BigTreeT/BigTreeT-Detecting-and-stopping-reverse-shell-with-Snort/assets/157978941/279907ec-1368-439d-a9fa-e9338e4f2461)

4. This many occurences is not common and more than likely malicious, lets create a rule to block all traffic leaving our network from port 4444.
   
![3](https://github.com/BigTreeT/BigTreeT-Detecting-and-stopping-reverse-shell-with-Snort/assets/157978941/e3ea803f-c433-40f1-b57e-e0934083c24e)

6. Our rule is set, we could have content:("ip address") blocked the specific IP but that can be easilly spoofed so we will block the port all together from leaving our network.
   
![4](https://github.com/BigTreeT/BigTreeT-Detecting-and-stopping-reverse-shell-with-Snort/assets/157978941/dae5012e-8f4c-4253-b29e-51b3c152335e)

Our rule is succesfully deployed on our network and no more of our data can be extracted from said port.
