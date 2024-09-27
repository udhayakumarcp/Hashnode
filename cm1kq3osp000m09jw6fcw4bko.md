---
title: "HAProxy Basic Authentication"
seoTitle: "HAProxy: Enabling Basic Authentication"
seoDescription: "Secure private sites with HAProxy basic authentication by following simple steps to create hashed passwords and update configuration files"
datePublished: Fri Sep 27 2024 12:52:38 GMT+0000 (Coordinated Universal Time)
cuid: cm1kq3osp000m09jw6fcw4bko
slug: haproxy-basic-authentication
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1727440200676/23fdd59e-1875-43d7-9611-4f2acc216327.jpeg
tags: proxy, haproxy, devops, webserver, ha, basic-authentication, high-availability

---

We can secure the acess to private or producted siters by enabling the basic authentication. It will display the login prompt to the users for username and password.

Enabling the basic authendicartion willl required the following steps. Let’s see one by one.

### Creating the user details

Add the following user list in the `haproxy.cfg` file which will be avilable in the `/etc/haproxy` directory if you are using linux based system.

```bash
userlist listofuser
  user udhay insecure-password udhayspassword
  user optionalAnotherUser insecure-password unsafepassword
```

Replace the username and passwords as per your requirement. Storing the plain password in the file as shown above is not secured. Any oine who hacve access to the system may able to view the password. So, to created the Hased passwords follow below steps

**Creating the hashed passwords**

1. Install the `mkpasswd` tool:
    
    ```bash
    sudo apt install whois
    ```
    
2. Has the password
    
    ```bash
    mkpasswd -m sha-256 mypassword        
    ```
    
    The above will command will prove the hashed password as output like below,
    
    ```bash
    $5$s6Subz0X7FSX2zON$r94OtF6gOfWlGmySwvn3pDFIAHbIpe6mWneueqtBOl/
    ```
    
    So you can replace the plain text password by hashed password. Then, the userlist will be
    
    ```bash
    userlist listofuser
      user udhay insecure-password $5$s6Subz0X7FSX2zON$r94OtF6gOfWlGmySwvn3pDFIAHbIpe6mWneueqtBOl/
    ```
    

### Adding the basic auth

Update the `haproxy.cfg` file as below, to use the basic auth

```nginx
# Other config goes here
frontend example_frontend
  # Other config goes here....
  bind :443 ssl crt /etc/haproxy/ssl/udhay.dev.pem
  use_backend private_site if { hdr(host) -i udhay.dev }
  # Other backends will go here..

backend private_site
  # Add your other configs
  http-request auth unless { http_auth(listofusers) }
  server web_server 127.0.0.1:80
```