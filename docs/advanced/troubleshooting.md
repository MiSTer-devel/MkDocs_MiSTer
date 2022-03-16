---
hide:
  - toc
---

## Fixing missing certs

If you are unable to wget as instructed above, this might be because you are missing security certificate files. The default system comes with no security certificate files, which is a bit annoying, as you need to add --no-check-certificate on wget to download anything HTTPS. Lets fix that:

1. Open the linux terminal/command prompt with F9, use `root` as your username and `1` as your password.
2. Type `cd /etc/ssl/certs` and press enter.
3. Type `wget --no-check-certificate https://curl.haxx.se/ca/cacert.pem` and press enter

Assuming it downloaded correctly, you can _now_ use wget as nature intended!
