# Evidian SafeKit load balancing and failover cluster (farm application module)

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fd6p%2Fazure-quickstart-templates%2Fsafekit-cluster-farm%2Fsafekit-cluster-farm%2Fazuredeploy.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

## Description
This template deploys a ready-to-use load balancing and failover cluster between 2 and 4 Virtual Machines (Windows or Linux).

+ each VM has a public IP address
+ the free trial of <a href="https://www.evidian.com/products/high-availability-software-for-application-clustering/">Evidian SafeKit</a> is installed in each VM
+ a farm application module (name: "farm") is deployed and configured 
  + it includes the possibility to monitor a critical application
  + it includes the possibility to restart automatically a critical application
  + it includes a generic health probe for the load balancer
  + it includes the connector for the SafeKit web console
  + see <a href="https://www.evidian.com/products/high-availability-software-for-application-clustering/network-load-balancing-cluster/">this page</a> for more information
+ a public Virtual IP (VIP) is associated with a public load balancer and is configured with:
  +	the public VIP as frontend IP
  +	all the VMs in its backend pool
  + a health probe to check the farm application module state
  + a load balancing rule for external port 9453 / internal port 9453 to access the VIP via the test url

## How to use
After deployment, go to the output panel and
+ visit the credential url to get the client and CA certificates in your web browser 
+ after certificates installation, start the web console of the cluster
+ test the VIP address with the test URL in the output


Beware, work in progress ... :umbrella: :umbrella:
