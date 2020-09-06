---
layout: post
title:  "using aws, route53, lightsail to setup a wordpress blog"
date:   2020-09-27 12:00:00 -0000
tags: python aws textract
---

 My wife asked me to setup a travel blog for her.  I wanted to maximize our flexbility with look and feel, have no adds and be as cheap as possible.  We ended up with a wordpress instance on AWS Lightsail with the domain name from aws as well.  Found really good tutorials for this so I'll link those.  You can find the blog here [https://travel.nomadley.com](https://travel.nomadley.com)
<br>

### Created an AWS account and signed into console

### Get a domain using Route 53
Used this [link](https://console.aws.amazon.com/route53/home#DomainRegistration:) to create a new domain.

### Setup Lightsail with Wordpress

This [link](https://lightsail.aws.amazon.com/ls/docs/en_us/articles/amazon-lightsail-tutorial-launching-and-configuring-wordpress) was a really great walk through.  It was pretty plug and play.  One note was the `A` record for the `travel` subdomain, set that up in a DNS zoen in LightSail.

### Setup HTTPS

This [link](https://lightsail.aws.amazon.com/ls/docs/en_us/articles/amazon-lightsail-using-lets-encrypt-certificates-with-wordpress) was what I used to set up HTTPS.  Worked great

----
**resources:**
- [https://lightsail.aws.amazon.com/ls/docs/en_us/articles/amazon-lightsail-tutorial-launching-and-configuring-wordpress](https://lightsail.aws.amazon.com/ls/docs/en_us/articles/amazon-lightsail-tutorial-launching-and-configuring-wordpress)
- [https://lightsail.aws.amazon.com/ls/docs/en_us/articles/amazon-lightsail-using-lets-encrypt-certificates-with-wordpress](https://lightsail.aws.amazon.com/ls/docs/en_us/articles/amazon-lightsail-using-lets-encrypt-certificates-with-wordpress)
- [https://console.aws.amazon.com/route53/home#DomainRegistration](https://console.aws.amazon.com/route53/home#DomainRegistration)