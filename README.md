# miqTools - ansible roles for interacting with ManageIQ

This is a collection of roles that allow easy interaction with ManageIQ via persistent sessions and access to several collections for the purposes of creating/manipulating content in a programmatic fashion.

## Invocation

![alt text](https://i.imgur.com/XPJQ2IE.png)

miqTools has some reserved variables associated with the primaryAppliance inventory:

* ___miq_auth_User = the user id to authenticate with
* ___miq_auth_Pass = the password to authenticate with

miqTools also has two reserved inventory names which must be defined

* **primaryAppliance** - this is the manage IQ web portal address
* **primaryDb** - this should be the database the manage IQ web portal runs on

miqTools stores data collection in a dictionary defined by you.  When calling the role be sure to tell it where to place the data:

```
import_role:
  name: miq-auth
vars:
  reference: "myData"
```

The roles automagically define whatever dictionary name you specify with "reference" in the host collection of **primaryAppliance**

We can examine / access the collected data directly using native methods:

```
- debug: var=myData

----------------->8-----------------
  myData:
    configurationScriptSourceMap:
      Project1_DevOps: '1000000000012'
      Project1_VMS: '1000000000017'
      Demo Project: '1000000000014'
      PRJ_RELEASEMGMT: '1000000000011'
      thatThing: '1000000000010'
      inflight: '1000000000016'
      testing: '1000000000015'
    loginCookie: 74e3cad21af5f4ec700a3e3d65a4a773
----------------->8-----------------
```
Here we see that myData contains the key loginCookie (a product of miq-auth) and configurationScriptSourceMap (a product of miq-get-configuration_script_sources).  All roles automatitcally look for 'loginCookie' in whatever data structure you define via "reference".
