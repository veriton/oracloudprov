# oracloudprov
## Introduction
This repo started from an Oracle Stack Manager (CSM) SOACS template (oracloudprov-SOACS-IPNet) which I started playing with during the holidays at the end of 2017 (after the CSM soacs resource had just been released). At the time the Oracle-provided template was a useful starting point but was very basic, e.g. didn't support IP networks in OCI Classic and was an essential requirement for me.

Please see the __Disclaimer__ at the bottom of this page.

## Cautionary Note
Oracle's cloud platform is developing very quickly indeed, especially in areas like CSM. For the provisioning functionality all commercial customers, without any option to opt out, get the new releases every month. What this means is that provisioning code, like stack templates or PSM commands, need regular testing and fixing. Please bear this in mind if you need to provision environments in a hurry at the start of a month :p

## 1. oracloudprov-SOACS
### Origin
This stack template was last derived from Oracle's supplied Oracle-SOACS-DBCS-Template (version 18.2.3-1804130567) in May 18.

### Summary of Changes
- Removed trailing spaces on some lines (cosmetic)
- Made DB 12.2 as default and removed 11g option
- Backup storage container is created by default
- Practical sizes on DB usable space with default as 25GB for dev/test
- DB PDB name is service name (in case you want to move it later)
- DB SID is service name with dbs suffix (can't be same as PDB) & removed redundant SID parameter
- Cloud stack name has to be 5 chars, part of my naming standard
- `stackRegion` changed from `RegionConfig` to `String` - see note 1
- Added `provisionOTD` to the SOA parameter group
- SOA instance suffix is now 3-letter acronym of soa (not SOACS) and DB is dbs (not DBCS)
- Added SOA cluster size parameter
- Changed the backup storage container from DBaaS to the stack name (to make easier segregation of backup between stacks) - see note 2
- Added `allowPublicAdmin` for initial testing, defaulted to false

### Known Issues
1. A single backup container is shared between DBaaS and SOACS. This important for DB Backup Cloud consumption (which I think is charged at the container level)

### Notes
#### 1. RegionConfig
A parameter type of `RegionConfig` is provided in the original Oracle template, but is not allowed in custom templates. In interactive operation it is quite nice as it gives a Region drop-down list and then optional drop-down list for IP networks - instead in a custom template you need to provide region as a JSON string.

#### 2. Backup storage containers
There's something funny about the backup storage containers in either the original script or how CSM currently handles them. Segregation of SOA from DBaaS backup worked on my v1 template but now there are some extra parameters. In the stock template its "JaaS" backup container is not used at all (soacs resource uses `dbBackupStorageContainer`) but also the dbcs resource depends on `backupContainer` which looks like the SOA one, even though the DBaaS one is created (possibly because it is the last?). Work in progress.

### Approximate Run-times
Step                        | Step Run-time | Overall
--------------------------- | ------------- | -------
Single node database        | 30 mins       | n/a
Single node SOA without OTD | 70 mins       | 1h 40 mins
Single node SOA with OTD    | ** mins       |
Two node SOA with OTD       | ** mins       |

These run-times will vary slightly depending on congestion in the data centre or your cloud account. However, if a stack is taking an unusually long time (e.g. +50%) at one stage it is likely to be in the process of failing.

Note the `postCreateService_2` custom action at the end of SOA instance creation, introduced in May 18, typically takes 45-50 mins.

Deleting a single node stack takes around 30 minutes.

### Test Environments
This code has been tested on the following environments (commit messages should say which):
* (a) a metered traditional-ID Oracle Cloud account (OCI Classic) provided to Oracle ACE Directors, courtesy of the [Oracle ACE Program](http://www.oracle.com/technetwork/community/oracle-ace/index.html) __[@oracleace](https://twitter.com/oracleace)__ - thanks :) )
* (b) a non-metered IDCS-backed Oracle Cloud account (OCI Classic)
* (c) a Universal Credits IDCS-backed Oracle Cloud account (OCI Classic)
* (d) NOT YET: I don't have an OCI Oracle Cloud account with spare credits - if anyone would like to lend me one I would be able to test with it ;)

Note that some things can behave differently between these environments so check the commit log and preferrably use a version that I have tested with the same type of account as you.

## Disclaimer - Use at Your Own Risk!
__This code is provided for free (under the [Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0) licence) but any use of it is entirely at your own risk.__ In particular most Oracle Cloud services are billed by the hour so should you use this code, or modified versions of it, __you may incur substantial charges from Oracle if you provision the wrong thing__.




