# KPMG_Challenge

Challenge#1

**Solution:**

I have chosen Azure for designing a 3-tier architecture. I have designed a basic setup using only IAAS.

3 layers created

1. Web Layer for Public facing
2. Application layer have the business logic
3. DB layer for storing the data.

Resources used:

VM - Availability set
Vent
Subnets
Publicip
Application Load Balancer for external traffic.
Standard load balancer for routing between App and DB layer internal traffic.
Network security groups for restricting the traffic using inbound/outbound rules.

Created a design in Draw.io and saged as png by name - 3-Tier_Architecture.drawio.PNG


The solution can be more enhanced based upon the type of requirement, but i have just done a basic setup using IAAS services alone, We can utilize the wide range of PAAS services as well depends on a business requirements.





