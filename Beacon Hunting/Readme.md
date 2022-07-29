# Threat Hunting - Beacon Detection
In this folder you will find  notebooks that can be used by cyber threat hunters to find processes that exhibit metronomic behavior, which may be consistent with malware beaconing.

## hunt_beacons_with_poisson
Attempts to find beacons, by finding processes that open network connection that are not independent of each other, and do not follow a Poisson distribution.  
Begin by collecting Sysmon Event ID 3 from endpoints across your environment, and forwarding them to a central collection point like a SIEM. Pseudo-search for:

  `event_id:3 (NOT DestinationIp:internal) (NOT process:<anything you'd like to exclude>) TABLE timestamp,SourceHostname,User,Process,SourceIp`

Gather this information into a consolidated CSV file, and supply it as input to the Jupyter notebook when prompted. 

Prerequisite: Jupyter Notebook (https://jupyter.org/install)
