# AWS
AWS Big Picture ([Pluralsight](https://app.pluralsight.com/player?course=aws-developer-big-picture&author=ryan-lewis&name=aws-developer-big-picture-m0&clip=0&mode=live))

AWS Getting Started ([Pluralsight](https://app.pluralsight.com/player?course=aws-developer-getting-started&author=ryan-lewis&name=aws-developer-getting-started-m1&clip=0&mode=live)) - This is awesome!

On-prem vs cloud:
  - Similarity: same dependencies, frameworks, etc. just in a different place
  - Biggest difference: abstract away from local Db's, storage, to services for best results

## IAM
  - best practice to create user and use that account for administration instead of root account

## VPC (Virtual Private Cloud)
  - Private IPs in an isolated network with rules of how to access external networks
  - Routing Table - map attempted external IP to resolved IP, e.g. for using a proxy or redirecting to a local instance
  - Network Access Control List - IP filtering, who can talk to the internet, not used too frequently
  - Subnet - additional isolated area inside a VPC w/ own routing table and NACL, typical to use a private and public subnet where private is customer facing but talks to private instances

Steps
  1. Create a subnet
  2. Edit routing table to allow outgoing traffic to hit the internetPublic subnet: destination 0.0.0.0/0 (anything) resolves to igw-xxxx (internet gateway)
  3. Create another subnet with a different CIDR block to avoid IP conflicts

## Amazon Machine Image (AMI)

Operating System + Software installed on EC2 instance

Setup
  1. Create EC2 instance, add to subnet
  2. Create an Elastic IP
  3. Connect to EC2 instance
  4. Install requisite software
  5. Run

Time to scale!
  1. Create custom AMI (select instance > Actions > Image > Create Image)
  2. Create a load balancer w/ sticky instances
  3. Create an auto scaling group
  4. Create a launch configuration
  5. Note, make sure it automatically starts application in Launch Configuration > Advanced Details. Provide it with shell script to run the application
  6. Create an auto scaling group
  7. Add to load balancer
  8. Use DNS name for load balancer (Would use a CNAME record to assign a different domain here)

We're doing it (scaling) live!
  1. Create auto scaling policies to add/remove instances based on some criteria
  2. Set min/max instances to bound the appropriate amount
    
  
## S3
  - Storage is based on objects (file & metadata)
  - Bucket is a container for storing objects, referenced by a URL namespace
  - Within namespace, objects are referenced by key: folder name/file name
  - Can upload w/ SDK, CLI, or UI

Modify app to point to S3 resources

Enable CORS - cross-origin resource sharing

Move to EC2, create IAM role (like an account/permission for an EC2 instance)

---

AWS Introduction ([video](https://www.youtube.com/watch?v=N89AffsxS-g))
What is AWS? - IaaS - Infrastructure as a Service
  - Products for building a cloud infrastructure:
     - Compute
     - Storage
      § Glacier - large, low accessibility, storage
     - Network
     - Database
     - DNS
  - Global data centers
     - Cloud means "I don't know where the data is"
     - AWS gives option to pick a data center close to users
  - IaaS vs VPS
     - AWS & Azure = IaaS
     - Linode & Digital Ocean = VPS (Virtual private server)Only servers for renting, not an infrastructure
  - Benefits
     - Highly scalable, "How do you scale Amazon? Throw money at them."
     - Lower total cost of ownership (TCO) than on-premises
     - Highly reliable (for the price point)
     - Centralized billing and management
  - Issues
     - Lock in
     - Learning curve
     - Building correct infrastructure
     - Cost adds up
  - Pricing
     - Compute pricing
     - Storage pricing
     - Bandwidth pricing
     - Interaction pricing
  - Migrating
     - Can be as simple as a normal migration
     - Full benefits may require reimagining up to rebuilding entire architecture
  - Final Thoughts

---

AWS in 10 minutes | AWS tutorial for beginners ([video](https://www.youtube.com/watch?v=r4YIdn2eTm4))
  - What is AWS?
     - Hosting provider for running services on the cloud
     - Infrastructure, platforms, software and storage
  - Why it's such a hit?
     - Simple billing & signup
     - Stability
  - Service overview
     - EC2 (Elastic Compute Cloud) - bare servers
     - VPC (Virtual Private Cloud) - create cloud networks
     - S3 (Simple Storage Service) - file storage/sharing
     - RDS (Relational Database Service) - cloud DBs
     - Route 53 - DNS
     - ELB (Elastic Load Balancer) - load-balance traffic
      § Autoscaling
  - How much it costs?
     - Per-hour and per-GB pricing
  - How big is it?
     - Big… really big.
  - Future
     - Current focus on machine learning & SAAS

---

AWS Concepts: Understanding AWS ([video](https://www.youtube.com/watch?v=qcY-uiEHhn0))
  - Watch this if you need a model of what "the cloud" is incl.
     - High Availability
     - Fault Tolerant
  - Also covers enterprise server architecture and how to scale vs AWS
     - Scalability - as user-base grows you can add servers
     - Elasticity - you can both grow and shrink back down

  
