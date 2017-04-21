## Base Config for Cloudflare with App Engine Flexible PHP
When using Cloudflare in-front of App Engine, we need a way to enforce all traffic coming in via Cloudflare, so visitors or malicious actors can't bypass the WAF and DDoS protection.

We also need to re-write the $_SERVER['REMOTE_ADDR'] variable in PHP to reflect the actual visitor IP, not Cloudflare's IP.

This repository contains an base config for an App Engine Flex PHP app, that includes an nginx config that'll do all of those things.

It will serve 403s to anyone not coming in via Cloudflare, which means the appspot.com domain, plus any of your custom domains.

### What is this trying to solve?
When Cloudflare is active, visitors can still see your site is hosted on App Engine based on the response headers.

Once they know this, they can change their local DNS, or edit their hosts file, to locally point your address directly to ghs.googlehosted.com

Without these protections in place, they would then be able to bypass the WAF, DDoS protection and/or caching.
