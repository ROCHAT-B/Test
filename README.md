## <a name="step1"></a>How the Evidian SafeKit software simply implements high availability with real-time synchronous replication and failover in Azure?

![How the Evidian SafeKit mirror cluster implements real-time replication and failover in Azure?](/safekit/images/azure-block-level-file-level-software-data-replication-mirror-cluster.png)

On the previous figure,

*   the critical application is running on the PRIM server
*   users are connected to a primary/secondary virtual IP address which is configured in the [Azure load balancer](https://docs.microsoft.com/en-us/azure/load-balancer/)
*   SafeKit brings a generic health probe for the load balancer. On the PRIM server, the health probe returns OK to the load balancer and NOK on the SECOND server.
*   in each server, SafeKit monitors the critical application with process checkers and custom checkers
*   SafeKit restarts automatically the critical application when there is a **software failure** or a **hardware failure** thanks to restart scripts
*   SafeKit makes synchronous real-time replication of files containing critical data
*   a connector for the SafeKit web console is installed in each server. Thus, the real-time replication and failover cluster can be managed in a very simple way to avoid **human errors**

On the previous figure, the server 1/PRIM runs the critical application. Users are connected to the virtual IP address of the mirror cluster. SafeKit replicates files opened by the critical application in real time. Only changes in the files are replicated across the network, thus limiting traffic ([byte-level file replication](https://www.evidian.com/products/high-availability-software-for-application-clustering/file-replication-byte-level-with-failover-mirror-cluster/)). Names of file directories containing critical data are simply configured in SafeKit. There are no pre-requisites on disk organization for the two servers. Directories to replicate may be located in the system disk. SafeKit implements [synchronous replication with no data loss on failure contrary to asynchronous replication](/safekit/synchronous-replication-vs-asynchronous-replication.htm).

In case of server 1 failure, there is an [automatic failover](https://www.evidian.com/products/high-availability-software-for-application-clustering/file-replication-byte-level-with-failover-mirror-cluster/#step2) on server 2 with restart of the critical application. Then, when server 1 is restarted, SafeKit implements [automatic failback with reintegration of data without stopping the critical application on server 2\. Finally, the system returns to](https://www.evidian.com/products/high-availability-software-for-application-clustering/file-replication-byte-level-with-failover-mirror-cluster/#step3) [synchronous replication between server 2 and server 1](https://www.evidian.com/products/high-availability-software-for-application-clustering/file-replication-byte-level-with-failover-mirror-cluster/#step4). The administrator can decide to swap the role of primary and secondary and return to a server 1 running the critical application. The swap can also be done automatically by configuration.
