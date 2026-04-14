## Regions
- Regions are a set of datacenters at certain location.
- Most services are region-scoped. Some are global.
#### How to choose a region?
- *Compliance* laws can mandate that data stay within the country.
- *Pricing* can be different in different regions.
- Low *latency* for users in the same region.
- *Availability of services* depends on the region.

## Availability Zones
- Region contains 3-6 availability zones. (Generally 3)
- One availability zone can contain multiple datacenters for redundancy, networking and connectivity.
- Availability zones are physically separated from each other, so in case one availability zone is destroyed, others can still serve the region
- They are connected with each other using ultra low latency network to work as a region.
- Example- Region: Mumbai(ap-south-1), Availability Zones: ap-south-1a, ap-south-1b

## Points of presence
- They make sure, content is delivered to user with low latency.
- They host services that need to be closer to the users.
	- Cloudfront (CDN for caching content)
	- Route 53 (DNS resolution)
	- AWS Global Accelerator (Optimized network routing)