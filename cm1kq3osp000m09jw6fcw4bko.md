---
title: "HAProxy Basic Authentication"
seoTitle: "HAProxy: Setting Up Basic Authentication"
seoDescription: "Enable basic authentication in HAProxy by prompting users for credentials to secure access to protected sites"
datePublished: Fri Sep 27 2024 12:52:38 GMT+0000 (Coordinated Universal Time)
cuid: cm1kq3osp000m09jw6fcw4bko
slug: haproxy-basic-authentication
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1727440200676/23fdd59e-1875-43d7-9611-4f2acc216327.jpeg
tags: proxy, haproxy, devops, webserver, ha, basic-authentication, high-availability

---

You can secure access to private or protected sites in HAProxy by enabling basic authentication, which prompts users for a username and password.

### Steps for Setting Up Basic Authentication:

1. **Create User Details:** In `/etc/haproxy/haproxy.cfg`, add the user list:
    
    ```bash
    userlist listofuser
      user udhay insecure-password udhayspassword
      user optionalAnotherUser insecure-password unsafepassword
    ```
    
    Replace with your own credentials. However, using plain-text passwords is insecure. To create **hashed passwords**, follow these steps:
    
2. **Hash the Password:** Install the `mkpasswd` tool:
    
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
        
    3. Replace the plain password
        
        So you can replace the plain text password by hashed password. Then, the userlist will be
        
        ```bash
        userlist listofuser
          user udhay password $5$s6Subz0X7FSX2zON$r94OtF6gOfWlGmySwvn3pDFIAHbIpe6mWneueqtBOl/
          # Other users
        ```
        
3. **Add Basic Auth in HAProxy:** Update your HAProxy configuration:
    
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
    

By following these steps, you'll have basic authentication enabled to secure your site.