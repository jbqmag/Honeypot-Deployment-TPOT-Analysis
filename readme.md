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
- **Create a Server**: Launch a new virtual machine (VM) or server instance. I selected **Ubuntu** as the operating system for this project.
- **Server Specifications**: Choose server specifications based on your needs. A basic setup with 1-2 CPUs and 2-4 GB RAM is sufficient for running T-Pot.
- **Connect to Your Server**: Once the server is created, use an SSH client (like PuTTY or your terminal) to connect to the server using the provided IP address and credentials.

### 2. Install and Configure T-Pot
Once your Linux server is up and running, you can proceed to install T-Pot, a multi-honeypot platform that deploys several honeypot services simultaneously. Follow these steps:
- **Update Your Server**: Ensure your server is up to date by running the following commands:
  ```bash
  sudo apt update && sudo apt upgrade -y