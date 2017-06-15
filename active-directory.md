# Active Directory

To force replication of domain entries between multiple domain controllers,
use the following command on the domaincontroller which items you want to push:

``` cmd
repadmin /syncall /AdeP
```
