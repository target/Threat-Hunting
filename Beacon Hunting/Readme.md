# Threat Hunting - Beacon Detection
In this folder you will find  notebooks that can be used by cyber threat hunters to find processes that exhibit metronomic behavior, which may be consistent with malware beaconing.

## hunt_beacons_with_poisson
Attempts to find beacons, by finding processes that open network connection that are not independent of each other, and do not follow a Poisson distribution.  
Begin by collecting Sysmon Event ID 3 from endpoints across your environment, and forwarding them to a central collection point like a SIEM. Pseudo-search for:

  `event_id:3 (NOT DestinationIp:internal) (NOT process:<anything you'd like to exclude>) TABLE timestamp,SourceHostname,User,Process,SourceIp`

Gather this information into a consolidated CSV file, and supply it as input to the Jupyter notebook when prompted. 

Prerequisite: Jupyter Notebook (https://jupyter.org/install)

## find_beacons_by_fourier
Looks for machines opening periodic HTTP GET connections, by doing a Fourier transform at multiple sampling intervals, and identifying any strong signals consistent with periodic/metronomic activity.  Pseudo-search network security monitoring tools for:
  
  `type:http SourceIP:<internal IP range> method:GET status:200 DestIP:<not internal range>`

Save to CSV and ingest into this notebook.  

Prerequisite: Jupyter Notebook (https://jupyter.org/install)
