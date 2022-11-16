# Infrastructure
## AWS Zones
Identify your zones here
## Servers and Clusters
### Table 1.1 Summary
| Asset      | Purpose           | Size                                                                   | Qty                                                             | DR                                                                                                           |
|------------|-------------------|------------------------------------------------------------------------|-----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| Ubuntu-web (EC2) | Web Application | t3.micro | 3 | Deployed DR to us-west-1 |
| Ubuntu-web for DR (EC2) | Web Application | t3.micro | 3 | DR for web app running in us-east-2 |
| EKS Cluster | Prometheus and Grafana | t3.medium | 1 cluster with 2 nodes | Deployed DR to us-west-1|
| EKS Cluster (DR) | Prometheus and Grafana | t3.medium | 1 cluster with 2 nodes | DR for monitoring tools running in us-east-2 |
| RDS Cluster | Database for web app | t3.medium | 2 nodes (writer+reader) | replicated with DR |
| RDS Cluster (DR) | Database for web app | t3.medium | 2 nodes (writer+reader) | replicated with DC |
### Descriptions
EC2 : Web App. Allows port 80 for internet access and port 22 for ssh.
EKS : Prometheus and Grafana cluster to monitor web app. 
RDS Cluster : Database for web app, we have 2 cluster, One master cluster (writer+Reader node). And the second cluster for DR (writer+reader node)
## DR Plan
### Pre-Steps:
List steps you would perform to setup the infrastructure in the other region. It doesn't have to be super detailed, but high-level should suffice.
Using Terraform to build 2 zones (us-east-2 and us-west-1)
Both zones will have same config.
We zones 1 down, will redirect to zones 2 with update route53.
## Steps:
You won't actually perform these steps, but write out what you would do to "fail-over" your application and database cluster to the other region. Think about all the pieces that were setup and how you would use those in the other region
Using Route53 to re-route traffic to DR zone.
With health check, when zone 1 down, route 53 will re-direct traffic from zone 1 to zone 2.
Traffic will go to ALB (EC2 group)
DB Cluster in zone 1 and zone 2 will replication.
With health checks, When DB zone 1 down, will force DB zone 2 to become primary.