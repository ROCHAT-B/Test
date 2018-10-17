## Architecture of the high availability cluster with real-time synchronous replication and failover

<center>![How the Evidian SafeKit mirror cluster implements real-time replication and failover in Azure?](https://www.evidian.com/safekit/images/azure-block-level-file-level-software-data-replication-mirror-cluster.png)</center>

On the previous figure,

*   the critical application is running on the PRIM server
*   users are connected to a primary/secondary virtual IP address which is configured in the Azure load balancer
*   SafeKit brings a generic health probe for the load balancer. On the PRIM server, the health probe returns OK to the load balancer and NOK on the SECOND server.
*   in each server, SafeKit monitors the critical application with process checkers and custom checkers
*   SafeKit restarts automatically the critical application when there is a **software failure** or a **hardware failure** thanks to restart scripts
*   SafeKit makes synchronous real-time replication of files containing critical data
*   a connector for the SafeKit web console is installed in each server. Thus, the real-time replication and failover cluster can be managed in a very simple way to avoid **human errors**

More information on Evidian SafeKit:

*   [Azure: The Simplest Load Balancing Cluster with Failover](https://www.evidian.com/products/high-availability-software-for-application-clustering/azure-load-balancing-cluster-failover/)
*   [Azure: The Simplest High Availability Cluster with Synchronous Replication and Failover](https://www.evidian.com/products/high-availability-software-for-application-clustering/azure-high-availability-cluster-synchronous-replication-failover/)
