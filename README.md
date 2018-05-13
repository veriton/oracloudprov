# oracloudprov
## Introduction
This repo started from an Oracle Stack Manager (CSM) SOACS template (oracloudprov-SOACS-IPNet) which I started playing with during the holidays at the end of 2017 (after the CSM soacs resource had just been released). At the time the Oracle-provided template was a useful starting point but was very basic, e.g. didn't support IP networks in OCI Classic and was an essential requirement for me.

## Cautionary note
Oracle's cloud platform is developing very quickly indeed, especially in areas like CSM. For the provisioning functionality all commercial customers, without any option to opt out, get the new releases every month. What this means is that provisioning code, like stack templates or PSM commands, need regular testing and fixing. Please bear this in mind if you need to provision environments in a hurry at the start of a month :p

## 1. oracloudprov-SOACS
### Origin
A stack template derived from Oracle's supplied Oracle-SOACS-DBCS-Template (version 1.1.11)

### Summary of changes
- Removed trailing spaces on some lines (cosmetic)
- Made DB 12.2 as default and removed 11g option
- Backup storage container is created by default
- Practical sizes on DB usable space with default as 25GB for dev/test
- DB PDB name is service name (in case you want to move it later)
- DB SID is service name with dbs suffix (can't be same as PDB) & removed redundant SID parameter
- Cloud stack name has to be 5 chars, part of my naming standard
- stackRegion changed from RegionConfig to String
- Added provisionOTD to the SOA parameter group
- SOA instance suffix is now 3-letter acronym of soa (not SOACS) and DB is dbs (not DBCS)
- Added SOA cluster size parameter

### Notes
#### 1. RegionConfig
A parameter type of RegionConfig is provided in the original Oracle template, but is not allowed in custom templates. In interactive operation it is quite nice as it gives a Region drop-down list and then optional drop-down list for IP networks - instead in a custom template you need to provide region as a JSON string.

### Test Environments
This code has been tested on the following environments (commit messages should say which):
(a) a metered traditional-ID Oracle Cloud account provided to Oracle ACE Directors (courtesy of the Oracle ACE Program http://www.oracle.com/technetwork/community/oracle-ace/index.html - thanks :) )
(b) a non-metered IDCS-backed Oracle Cloud account
(c) a Universal Credits IDCS-backed Oracle Cloud account
Note that some things can behave differently between these environments so check the commit log and preferrably use a version that I have tested with the same type of account as you.

*Improved documentation will follow... eventually ;)*



