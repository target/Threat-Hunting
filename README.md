# Threat Hunting - Powershell Obfuscation
This is a tool that can be used by cyber threat hunters to find obfuscated Powershell commands. Threat actors frequently use obfuscated Powershell to do things like download toolkits and run malicious payloads. Finding this can be a very big "needle in haystack" problem. This tool uses statistical techniques to reduce the size of the haystack, and can be very effective for finding obfuscated Powershell in your environment. 

# Get Started Using 
Begin by collecting Windows Event ID 800 from endpoints across your environment, and forwarding them to a central collection point like a SIEM. Pseudo-search for: 

  Event_id:800  
  AND UserID:<regex for your user ID format>  
  AND NOT commandline:*.ps1* 

From this, filter the results down to contain commands run only by human usernames (rather than system or automated usernames), and NOT run from a .ps1 file on disk. Search this over some timeframe, de-duplicate the results, and export to a file called "pscommands.csv". Make sure the column that contains the commands run is labelled "commandline". 

To run hunt_powershell_obfuscation, first install Jupyter Notebook on the machine you will use to analyze the data. (See https://jupyter.org/install for instructions.) Start up Jupyter Notebook, and open the hunt_powershell_obfuscation.ipynb notebook file. Save your pscommands.csv file to the same directory as the notebook file. Then just execute each cell in the notebook. The output will be a list of commands found in your environment that are statistically most likely to contain obfuscation, if there is any to be found. This is output to a file called "regressionoutliers.csv". There will also be a graph of the data, helping to visualize any outliers that may require further investigation. 

# Contributor Instructions
The entire .ipynb file can be opened and edited directly with Jupyter Notebook.  Be sure to restart the kernel before any new commits, which will ensure that any data or output is committed with the code. 

# Contacts 
Joe Petroske, joe.petroske@target.com 
