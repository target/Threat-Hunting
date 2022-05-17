# Threat Hunting - Powershell Obfuscation
In this folder you will find several notebooks that can be used by cyber threat hunters to find obfuscated Powershell 
commands. Threat actors frequently use obfuscated Powershell to do things like download toolkits and run malicious 
payloads. Finding this can be a very big "needle in haystack" problem. This tool uses statistical techniques to 
reduce the size of the haystack, and can be very effective for finding obfuscated Powershell in your environment. 

# hunt_powershell_obfuscation

Begin by collecting Windows Event ID 800 from endpoints across your environment, and forwarding them to a central 
collection point like a SIEM. Pseudo-search for: 

```
  Event_id:800  
  AND UserID:<regex for your user ID format>  
  AND NOT commandline:*.ps1*
``` 

From this, filter the results down to contain commands run only by human usernames (rather than system or automated 
usernames), and NOT run from a .ps1 file on disk. Search this over some timeframe, de-duplicate the results, and 
export to a file called "pscommands.csv". Make sure the column that contains the commands run is labelled "commandline".

To run hunt_powershell_obfuscation, first install Jupyter Notebook on the machine you will use to analyze the data.
(See https://jupyter.org/install for instructions.) Start up Jupyter Notebook, and open the 
hunt_powershell_obfuscation.ipynb notebook file. Save your pscommands.csv file to the same directory as 
the notebook file. Then just execute each cell in the notebook. The output will be a list of commands found in your 
environment that are statistically most likely to contain obfuscation, if there is any to be found. This is output to 
a file called "regressionoutliers.csv". There will also be a graph of the data, helping to visualize any outliers that
may require further investigation. 

# hunt_powershell_obfuscation_with_classifier

This notebook will ingest a CSV file of Powershell commands, with all commandline arguments. This can be 
obtained from EID 1 (Sysmon) or 800. Specifically, look for Powershell commands run by a user (not an automated 
process), and did NOT run from a .ps1 script (meaning it ran direct from shell, which is more consistent with 
adversary activity). This should consist of benign, non-obfuscated commands. Concatenate and de-duplicate this 
list. The column name should be "commandline". This will be the basis for our training set.

Pseudo-search logic: `eventid:(800|1) userID: NOT commandline:.ps1`

Next: Create a list of obfuscated Powershell commands. You can collect these from public sources, or generate your
own with a tool like Invoke-Obfuscation (https://github.com/danielbohannon/Invoke-Obfuscation). Append this list 
to your existing list of (benign) Powershell commands.

Finally: append a new column called "isobfuscated" that takes a value of 1 for "obfuscated" and 0 for "not obfuscated".
The entries from the first (benign) list should all be 0, and the obfuscated list should all be 1.

This finalized list will be ingested as our testing/training dataset. We will use sklearn's fit() function for training,
and the predict() function for testing.
