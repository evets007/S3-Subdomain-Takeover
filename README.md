# Save the subdomains

Subdomain takeover vulnerabilities occur when a subdomain of a website (subdomain.example.com) is pointing to a service (e.g. AWS S3, GitHub pages, Heroku, etc.) that has been removed or deleted. This allows an attacker to set up a page on the service that was being used and point their page to that subdomain. For example, if subdomain.example.com was pointing to a Amazon AWS S3 Bucket and the user decided to delete their S3 bucket, an attacker can now create a S3 bucket with the same name, or add a CNAME file containing subdomain.example.com, and claim subdomain.example.com.

# S3 bucket hijack

As part of this project, I will be focusing on potential S3 buckets takeovers at the moment. I identified a bunch of buckets that no longer exist, but have a subdomain pointing towards it. I gathered these results by querying DNS dataset dumps for domains pointing to S3 services and then performing a curl request on them sequentially. The buckets which are configured privatly returned a 403 - Access Denied, the buckets which are public return a 200 and the ones that don't exist return a 404 - No such bucket. I wrote a script to automate this process and collect a list of subdomains that pointed to AWS S3 and returned a 404.

I collected around 200 subdomains that also consisted of a few top-level domains. Right now, I'm working on finding a way to disclose them properly to the website's team.
