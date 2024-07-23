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
<br>We know that there was some type of suspicious behavior that alerted our system that a connection was being made to our workstation. Volatility3 has 2 two plugins that can provide us with network information about the system at the time the memory image was captured, <b>Netstat*</b> and <b>Netscan*</b>.

<br> **Ideally we would want to input a the plugin<b>imageinfo</b> to obtain information to better understand the correct type of profile to use for our analysis. Profiles help specificy  the OS and version for accurate parsing and xamination of the memory image. **
the syntax would look like this: 
<br> <i>python3 vol.py -f NameofImage.dmp imageinfo</i>
