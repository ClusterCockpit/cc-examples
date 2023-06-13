# ClusterCockpit at NHR@FAU

NHR@FAU provides a production instance of ClusterCockpit for support personel
and users. Authentication is via an LDAP directory as well as via our HPC Portal
(homegrown account management platform) using JWT tokens.

You can find an overview about all clusters
[here](https://hpc.fau.de/systems-services/documentation-instructions/).

Some systems run with exclusive nodes, others have node sharing enabled.
There are CPU systems (Fritz, Meggie, Woody, TinyuFat) as well as GPU enabled
clusters (Alex, TinyGPUs).

NHR@FAU uses the following stack:
* `cc-metric-collector` as node agent
* `cc-metric-store` as temporal metric timeseries cache. We use one instance for all clusters.
* `cc-backend`
* A homegrown python script running on the management nodes for providing job meta data from Slurm
* Builtin sqlite database for job meta and user data (currently 11GB)
* Job Archive without retention using compressed data.json files (around 700GB)

We also push the metric data to an InfluxDB instance for debugging purposes.

The backend and metric store run on the same dedicated Dell server running
Ubuntu Linux:
* Two Intel Xeon(R) Platinum 8352Y with 32 cores each
* 512 GB Main memory capacity
* A NVMe Raid with two 7TB disks

This configuration is probably complete overkill, but we wanted to be on the
safe side.
