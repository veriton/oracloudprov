# oracloudprov
## Introduction
This repo started from an Oracle Stack Manager (CSM) SOACS template (oracloudprov-SOACS-IPNet) which I started playing with during the holidays at the end of 2017 (after the CSM soacs resource had just been released). At the time the Oracle-provided template was a useful starting point but was very basic, e.g. didn't support IP networks in OCI Classic and was an essential requirement for me.

## Cautionary note
Oracle's cloud platform is developing very quickly indeed, especially in areas like CSM. For the provisioning functionality all commercial customers, without any option to opt out, get the new releases every month. What this means is that provisioning code, like stack templates or PSM commands, need regular testing and fixing. Please bear this in mind if you need to provision environments in a hurry at the start of a month :p

## 1. oracloudprov-SOACS
### Origin
A stack template derived from Oracle's supplied Oracle-SOACS-DBCS-Template (version 1.1.11)

### High level summary of changes
- Removed trailing spaces on some lines (cosmetic)

*Improved documentation will follow (eventually ;) )*



