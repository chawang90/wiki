# Registrars, DNS, and SSL, Oh My!

This documents all of our domain registration stuff.

## Registrar

We bought josephine.com through [Register.com](http://register.com), so that's where we renew the domain itself.

Since Register is kind of a crappy service, we decided to go with [DNSimple](http://dnsimple.com) as our DNS provider. This required pointing Register over to DNSimple's NAME servers so they could do all the heavy lifting.

## DNS

We use DNSimple. It's actually pretty awesome.

DNSimple has a nifty feature for wildcard subdomains, called the ALIAS record. Basically the ALIAS acts on your "root" or "apex" domain (ie, josephine.com) but behaves more like a CNAME (you can point it to another URL) than an ANAME (you point it to set of IPs).

This was necessary for us to use Heroku with just one wildcard SSL certificate at both the root domain level (josephine.com) and the subdomain level (staging.josephine.com, www.josephine.com). If this makes no sense, it's okay :)

## SSL

SSL is an incredibly confusing process, and has made Tal cry more than anything else throughout his career. We also happen to use wildcard SSL, which allows for wildcard domains (ie, `*.josephine.com` including the root itself) which was an even bigger pain in the neck to set up.

We bought the SSL certificiate on DNSimple and installed it using Heroku's `ssl` addon.

More on how this works here:
- https://devcenter.heroku.com/articles/ssl-certificate-dnsimple
- http://blog.dnsimple.com/2011/11/introducing-alias-record/

### How to renew SSL

##### Buy a new certificate.

[Follow this link to buy a new certificate on DNSimple](https://dnsimple.com/domains/josephine.com/certificates/10884/renewal/new). That's the easy part.

##### Validate the purchase

Once purchased, you should get an email within a day that tells you to validate your purchase.

> Dear admin@josephine.com,
>
> We have received a request to issue an SSL certificate for *.josephine.com.
> *** Please ignore this email if neither you nor a trusted colleague made this request for a certificate ***
> Otherwise, please browse here and enter the following "validation code":
> 7OQeloLv66VRJad7ve2bwRIVum4C26

Click on the link above and enter the validation code. You should get an email with the actual keys
entitled:
> ORDER #18957625 - Your EssentialSSL Wildcard Certificate for *.josephine.com"*.

The email will contain a zip file with your certificate files, but they also appear in the web console so [go straight to the web console](https://dnsimple.com/domains/josephine.com/certificates/17580/installation) once you've received the confirmation email.

Go down to the section on Heroku. You'll need to follow the following steps.

##### Download the pem file

You should get a file named `STAR_josephine_com.pem`

##### Download the key file
You should get another file named `STAR_josephine_com.key`

##### Add the certificate to Heroku.
Copy those files into the `josephine` directory and `cd` there.

Then run the following **(first on staging)**

```bash
$ heroku certs:update STAR_josephine_com.pem STAR_josephine_com.key -r staging

Resolving trust chain... done

 !    WARNING: Potentially Destructive Action
 !    This command will change the certificate of endpoint shiga-1550.herokussl.com on josephine-staging.
 !    To proceed, type "josephine-staging" or re-run this command with --confirm josephine-staging

> josephine-staging
Updating SSL Endpoint shiga-1550.herokussl.com for josephine-staging... done
Updated certificate details:
Common Name(s): *.josephine.com
                josephine.com

Expires At:     2016-12-22 23:59 UTC
Issuer:         /OU=Domain Control Validated/OU=EssentialSSL Wildcard/CN=*.josephine.com
Starts At:      2015-10-24 00:00 UTC
Subject:        /OU=Domain Control Validated/OU=EssentialSSL Wildcard/CN=*.josephine.com
SSL certificate is verified by a root authority.
```

Then verify the certificate.

```bash
$ heroku certs -r staging
Endpoint                  Common Name(s)                  Expires               Trusted
------------------------  ------------------------------  --------------------  -------
shiga-1550.herokussl.com  *.josephine.com, josephine.com  2016-12-22 23:59 UTC  True
```

Weee! Ensure that the certificate expires in the right year. Also visit staging.josephine.com and ensure that the SSL certificate is in use, and you get no red errors.

**If this all works, repeat these steps for production**
