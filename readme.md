# Honeypot Deployment

## Motivation
 This project was motivated by a desire to gain hands-on experience in setting up a honeypot environment and analyzing real-world attacks. By deploying a honeypot using T-Pot, I aimed to capture and study the behavior of attackers, understand their methods, and explore ways to secure vulnerable systems against similar threats. 

One specific motivation was to act as a cybersecurity analyst, focusing on identifying patterns in the attacks and hypothesizing why and how certain IP addresses were targeting my honeypot(s) by using TPOT for deployment and analysis through it's user-friendly web interface. Through this analysis, I aimed to better understand the nature of the threats and develop strategies to mitigate them.

## Project Overview
This project involved deploying a honeypot using [T-Pot](https://github.com/telekom-security/tpotce), a comprehensive honeypot platform that integrates multiple honeypot services. After setting up the honeypot on a cloud-based Linux server, I let it run for three days to capture data. During this period, I observed 26,000 attacks from a single IP address. The focus of this project was then to analyze this attacker's behavior, investigate their methods, and reason about potential motivations.

## Steps to Implement Your Own Honeypot

### 1. Set Up a Cloud-Based Linux Server
To get started, you'll need to set up a Linux server in the cloud. For this project, I used **Vultr**, but you can choose any cloud service provider (e.g., AWS, DigitalOcean, Google Cloud). Here’s how I did it:
- **Sign Up**: Create an account with your chosen cloud provider.
- **Create a Server**: Deploy a server on the top right and click "deploy new server" when shown the dropdown menu
  [here](https://github.com/jbqmag/Honeypot-Honeytrap-Analysis/blob/main/pngs/S1.png)
- **OS/ISO**- use  [T-Pot](https://github.com/telekom-security/tpotce) documentation to see what distros are available and compatible for use. In my case, I used an Ubuntu 22.04 LTS x64 to download tpot.
- **Server Specifications**: Choose server specifications based on your needs. A basic setup with 4 CPUs and 8 GB RAM is sufficient for running T-Pot. Make sure to select the "regular cloud compute" as this will most likely be enough for your use case of employing the honeypot.
- **Additional Features** : Disable Auto Backups and IPv6 as this is not necessary for our basic implementation. 



### 2. Firewall configuration + Installing and Configure T-Pot

#### a) Set up a firewall rule to prevent other ips from accessing your honeypot until it is fully configured:

- Create a firewall group within the settings of your virtual machine.
- Within it, you will create two Inbound IPv4 rules to temporarily only allow the owner (you) to configure and interact with your honeypot until it is set up:
  - Protocol: TCP & UDP
  - Port (or range): 1:65535
  - Source IP: Your host machine ip. *Note that this is NOT the ip of the server you just made*

![alt text](https://github.com/jbqmag/Honeypot-Honeytrap-Analysis/blob/main/pngs/S2.png)
*Click on the settings tab of your virtual machine to navigate to the firewall page. From here you should be seeing this, in which you will click the grey pen in order to add a firewall group.*

![alt text](https://github.com/jbqmag/Honeypot-Honeytrap-Analysis/blob/main/pngs/S3.pn)
*Click on the settings tab of your virtual machine to navigate to the firewall page. From here you should be seeing this, in which you will click the grey pen in order to add a firewall group.*
#### b) Download and set up TPOT server to run your very own honeypot: 
For more specific uidance on installation, please check the installation section on the readme file of the [T-Pot](https://github.com/telekom-security/tpotce) documentation.
Once your Linux server is up and running, you can proceed to install T-Pot, a multi-honeypot platform that deploys several honeypot services simultaneously. Follow these steps:
- **Update Your Server**: Ensure your server is up to date by running the following commands:
  ```bash
  sudo apt update && sudo apt upgrade -y
  ```

- Clone the github repository: 
```bash 
$ git clone https://github.com/telekom-security/tpotce
```
- Change into the tpotce/ folder and run the installer 
```bash 
./install.sh
```
- Follow the installer instructions and keep note of your login info. This will be used to aaccess your tpot server via SSH and web browser.
- If all is well, after rebooting your server you should be able to see that your tpot service is running by running the command
```bash
  sudo systemctl status tpot.service
  ```
- If you see that your service is active and running, then congrats: you just configured your very own honeypot!

#### c) Reconfiguring firewall
- Now that your TPOT honeypot platform is up, we should be able to track incoming attacker traffic that gets attracted to our honeypots via the TPOT service. 
- Enter http://{insert your virtual machine's ip}:64297 into your search bar and sign in to your tpot interface.
- Notice that if you are to access your attack map, it seems as if there is no traffic coming to your TPOT. What gives? Well, our firewall is still blocking inbound access (as a firewall should do), because of those inbound rules we created that only allowed our host ips into the firewall
- Similar to the process above, we will be replacing the two defensive firewall rules in order to have, not only us, but suspicious attackers fall for our honeytrap!

![alt text](S4.png)
*As you can see, we allow TCP and UDP connections from anywhere in the world, a rule for us to access our TPOT remotely ia SSH and our web server on ports 64294 and 64297 respectively.*


## Takeaways
You should now have a fully working and running TPOT service that you just configured! Multiple honeypots will be configured given you have downloaded the service and kept it up and running. The biggest thing to take away from this project is that Cyber Attacks are very much real and can happen all over the world- even to you! Just after running this service for only about a week, I have close to 24 million interactions from attackers all over the globe!
 This is your chance to really dig deep, ask questions, and seek out patterns of what  real world attacks might look like! Feel free to play around with the various tools and perhaps get your hands dirty in a deep dive investigation, perhaps record your findings like i have done! 

 ![alt text](S5.png)

 *Honeytrap dashboard via Kibana, shows the overview of the attacker interactions i get from my TPOT service*
