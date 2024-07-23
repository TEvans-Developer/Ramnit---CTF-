<h1>Ramnit</h1> Ramnit is a Endpoint Forensics CTF within CyberDefender which offers hands-on practical experience for SOC Analyst.

<br><h2>Scenario: </h2>
Our intrusion detection system has alerted us to suspicious behavior on a workstation, pointing to a likely malware intrusion. A memory dump of this system has been taken for analysis. Your task is to analyze this dump, trace the malware’s actions, and report key findings. This analysis is critical in understanding the breach and preventing further compromise.

<h3> Securirty tools used for this CTF and their purpose </h3>
  - Volatility 3 ( memory forensics framework to extract digital artifact from RAM dumps)
  * Download Voltaility3 by going to their offical website> Github> Follow their intructions. 
  
  <br>- VM (Kali Linux)
  <hr>
  <h3>Question 1:</h3>
  <i>We need to identify the process responsible for this suspicious behavior. What is the name of the suspicious process?</i>
  <h3>Approach:</h3>
  <br> The question is asking us to find the process cause the suspicious behavior. We first must understand that Volatility comes with plugins that can aid with listing all process ran in memory on our workstation.

<h3>Steps:</h3>
<b>Step 1:</b>
<br> After setting up our VM machine, installing Volatility3, Pyhton3 and our memory.dmp file provided to us from CyberDefender (password for extraction also provided). We will move our .dmp file into a folder that is also in the directory of our Volatility3 tool.

<br><b>Step 2:<b><br>
<br>We know that there was some type of suspicious behavior that alerted our system that a connection was being made to our workstation. Volatility3 has 2 two plugins that can provide us with network information about the system at the time the memory image was captured, <b>Netstat*</b> and <b>Netscan*</b> (netscan was used in the instance due to an issue with cloning volatility from Git). We will open our terminal and type:
<br><i> python3 vol.py -f NameOfImage.dmp netstat **(or netscan)</i>


<br> **Ideally we would want to input a the plugin <i>imageinfo</i> to obtain information to better understand the correct type of profile to use for our analysis prior to netstat or netscan in this instance. Profiles help specificy the OS and version for accurate parsing and examination of the memory image.**
the syntax would look like this: 

<br> <i>python3 vol.py -f NameofImage.dmp imageinfo</i>

<br>Step 3:<br>
The terminal should now show net information pertaining to the processes in the memory image. We want to pay particular attention the the <i>Owner</i> column. We will see a fair amount of process that are common for Windows, upon analysis we will see a process that is NOT windows related and that is <i> ChromeSetup.exe</i>

<br><b>Answer:</b><i> ChromeSetup.exe</i>
<hr>

<h3>Question 2:</h3>
<i>To eradicate the malware, what is the exact file path of the process executable? </i>
<h3>Approach:</h3>
<br> We understand that we need to eradicate the malware. In order to do so we must undertand our file path and the process execuatble <i> ChromeSetup.exe</i>. Taking into account of the word process  a command of some sort must be made. Volatility has a plugin <b>cmdline<b>* which we can use for our analysis to display the command line arguments for each process and what executed scripts were ran.
<h3> Steps</h3>
<b>Step 1:</b>
<br> We will input into the terminal the synax:
  
<br><i> python3 vol.py -f NameOfImg.dmp cmdline | grep "ChromeSetup.exe"

<br> we include  the pipe symbol "|" and <i>grep</i> linux command to emphasize we want to find ones particular to the proccess <i>ChromeSetup.exe</i>. 

<br><b>Answer:</b><i>C:\Users\alex\Downloads\ChromeSetup.exe</i>

<hr>

<h3>Question 3:</h3>
<i>Identifying network connections is crucial for understanding the malware's communication strategy. What is the IP address it attempted to connect to?</i>
<h3>Approach:</h3>

We want to find the logical address of that our attackers malware is trying to communicate to a potential (C2) for this particular process. We know from our previous question what the proccess is and with IP address being network based we can revisit our netstat ( or netscan)  to find the ip address. 

<h3>Steps:</h3>

<b>Step 1:</b>
<br> We want to renter our command or tab up on our keyboard until it reappears:
<br><i> python3 vol.py -f NameOfImage.dmp netstat **(or netscan)</i> 

<b>Answer: <b><i>58.64.204.181</i>

<hr>

<h3>Question 4:</h3>
<i>To pinpoint the geographical orgin of the attack, which city is associated with the IP address the malware communicated with</i>

<h3>Approach:</h3>
We understand knowing as much information about the attacker can aid us in understanding who they are, were they are, their TTPs and how sophisticated our attacker(s) is. This information will also help use block the attack, do further analysis for this specific IP address and even take legal actions against the attacker. Understanding that IP addresses are a logical address provided to indivduals to access the public internet as well as other networks and that their are websites such as "whatismyipaddress.com" that can help us look up the orgin of an IP address will aid us in our search. 

<h3>Steps</h3>
<b>Step 1:</b>
<br> This step is simple. We will simplely copy and paste the IP address we found from our potential attacker into the website "whatismyipaddress.com" and it will feed us back the orgin (City) of the IP address.


<b>Answer:</b><i> Hong Kong</i>

<hr>

