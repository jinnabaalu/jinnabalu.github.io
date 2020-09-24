---
title: Securing Elasticsearch Cluster - Part 1
description: Securing Elasticsearch Cluster
---

# Securing Elasticsearch Cluster Before and After 6.8/7.1

Elasticsearch is a popular, open-source distributed RESTful search engine. When used monitoring, These wide-open to attack instances are typically being deployed without much on Amazon Web Services (AWS) clouds. Perhaps the people deploying them are under the illusion that AWS is protecting them. Wrong.

AWS does tell you [how to protect your AWS Elasticsearch instances](https://aws.amazon.com/blogs/security/how-to-control-access-to-your-amazon-elasticsearch-service-domain/), but you still have to do the work. In short, RTFM. If its programmers had protected its instances with basic, well-known security measures.

## Before Elasticstack 6.8

By itself, Elasticsearch has no security. You must add it on if you are before Elastic stack 6.8. 

### Basic Protections
To prevent this, most security companies or researchers would suggest:

- Don’t expose your internal servers to the public, if this is required whitelist the IP as necessery. 
- Run the elasticsearch in VPN with private IPs if you are using the AWS EC2.
- Don't use default ports
- If containers are in place use the container network to make services interact with elasticsearch with more security.
- Apply good security practices like using strong passwords, proxies and network segmentation to have certain levels of isolation. Configure interface properly so you’re not using default ports. Disable HTTP, scripting and other interfaces if you don’t need them.
- Perform backups of your data to a secure location and consider using [Curator](/curatorlink) snapshots

> Warning: Don't be the fool who lets anyone invade their servers. After all, you could very well end up paying a lot more than just some petty-cash if a truly malicious hacker came by to raid your servers.

Reletaed security references are as follows

- [Don't be ransacked: Securing your Elasticsearch cluster properly](https://code972.com/blog/2017/01/107-dont-be-ransacked-securing-your-elasticsearch-cluster-properly)
- [Protecting Against Attacks that Hold Your Data for Ransom](https://www.elastic.co/blog/protecting-against-attacks-that-hold-your-data-for-ransom)
- [Elasticsearch ransomware attacks now number in the thousands](https://www.zdnet.com/article/elasticsearch-ransomware-attacks-now-number-in-the-thousands/)
- [MongoDB attackers hijacked ElasticSearch servers for ransom](https://blog.360totalsecurity.com/en/mongodb-attackers-hijacked-elasticsearch-servers-ransom/)

<div class="embed-responsive embed-responsive-16by9">
  <iframe class="embed-responsive-item" src="https://www.youtube.com/embed/c9O5_a50aOQ?rel=0" allowfullscreen></iframe>
</div>

## After Elasticstack 6.8/7.1

After Elastic Stack 6.8 and 7.1, made a number of Elasticsearch security features more widely available to everyone by making them free in the default distribution. Even after the security is open with XPack, new challenges now is to updating the security parameters to consider while configuring the cluster. Gone are the days of relying on just a proxy server in front of the Stack to secure it!

Security is now free, free, free.............

- Encrypt network traffic
- Create and manage users
- Define roles that protect index and cluster level access
- Fully secure Kibana with Spaces.

Everyone can now run a fully secure cluster, hassle free. First thing to do is upgrade your clusters to either 6.8 or 7.1
