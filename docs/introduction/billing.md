# \env{SYSTEM_NAME} billing

## Terminology

* Billing unit (BU): A unit used for billing at CSC - each resource consumes a given amount of BUs per hour.
* CSC computing project: A placeholder for the user's resources information - including: the number of BUs and the CSC 
services which are available for use.
* OpenShift project: A Kubernetes namespace with additional annotations.

## Billing model

------------------------------------------------------------------------------------------------------------------------

**NOTE**: Starting from 1.02.2020, using \env{SYSTEM_NAME} consumes **CSC Billing Units**.

------------------------------------------------------------------------------------------------------------------------


Billing units are calculated by scraping usage data from all of the OpenShift projects owned by the user. 
These calculations are based on:

* Pod core usage (per core hour)
* Pod memory usage (per RAM GB hour)
* Persistent volumes (per TiB hour)

The rate at which billing units are consumed depends on the size of the
resources. Billing units are consumed as follows:

| Resource         | Billing units |
|------------------|---------------|
| Pod core hour    | 0,5           |
| Pod RAM GB hour  | 1             |
| Storage TiB hour | 3             |

For example, let's say you create a pod with the following specs:

* 0.2 cores
* 512 MiB RAM

You also create a persistent volume of size 10 GiB and attach it to the pod. The
cost in BUs can be calculated as follows:

0.2*0.5 + (512/1024)*1 + (10/1024)*3 = 0,6293 BUs
