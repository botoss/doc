Jenkins web-interface listens on port 8443. There is build job telegram-connector, which one may use as skeleton for other jobs.

**TODO**: add project template for easier job creation.

It would be really nice to have for every project (both connectors and modules) auto build-and-deploy on server job. For instance, what telegram-connector build job does do:
  1. On every update of telegram-connector repo's master branch job is started (GitHub hook trigger for GITScm polling checkbox) .There is special GitHub user for pulling changes from GitHub in Jenkins job, his nickname is `jenkins-botoss`. Though, we are still able to start it manually. If needed, branches to build can be specified (not only master, for example).
  2. Then it builds docker image using `sbt docker` (see Build using sbt step).
  3. Finally, it executes shell script, which deploys docker image.

**TODO**: run tests for every pull request and display its status on GitHub.

Jenkins SSL certificate update:

```
# certbot renew --force-renewal &&
    cd ~soft/keys &&
    cp /etc/letsencrypt/live/*/fullchain.pem fullchain.pem &&
    openssl rsa -in /etc/letsencrypt/live/*/privkey.pem -out privkey-rsa.pem &&
    systemctl restart jenkins
```
