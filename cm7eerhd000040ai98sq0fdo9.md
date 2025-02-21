---
title: "How to Update the Node.js Version in a PM2 Instance"
seoTitle: "Update Node.js Version in PM2 Instance"
seoDescription: "Update Node.js for PM2 apps without losing state by following these essential steps for a smooth transition"
datePublished: Fri Feb 21 2025 06:46:49 GMT+0000 (Coordinated Universal Time)
cuid: cm7eerhd000040ai98sq0fdo9
slug: how-to-update-the-nodejs-version-in-a-pm2-instance
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1740120136391/fc011e1b-aa6b-4159-8ff3-e41de966a51e.webp
tags: nodejs, upgrade, devops, pm2, node-js, nodejs-developer

---

Updating the Node.js version in a PM2-managed application requires a few key steps to ensure a smooth transition without losing your process state. Follow these steps to update Node.js while keeping your PM2 processes intact.

# **Step 1: Save the Current PM2 State**

Before updating Node.js, save the current PM2 process list to restore it later. Run:

```bash
pm2 save
```

This ensures that your running applications and their configurations are backed up.

# **Step 2: Disable PM2 Auto-Start**

If PM2 is set up to start automatically on system boot, disable it before updating Node.js:

```bash
pm2 unstartup
```

This prevents conflicts during the update process.

# **Step 3: Update Node.js**

Use a version manager like **NVM (Node Version Manager)** to update Node.js.

Refer my Blogs to Update / Install

1. [Install / Update NVM in Ubuntu](https://udhayakumarc.medium.com/how-to-install-update-nvm-and-node-in-ubuntu-7dcedf321bf0)
    
2. [Install/ Upgrade Node in Windows](https://udhayakumarc.medium.com/how-to-install-upgrade-node-in-windows-5d27f4a7c070)
    

Verify the installation:

```bash
node -v
```

# **Step 4: Reinstall PM2**

Since PM2 is installed globally, updating Node.js may remove it. Reinstall PM2 using:

```bash
npm install -g pm2
```

# **Step 5: Update PM2**

Ensure PM2 is updated to the latest version to avoid compatibility issues:

```bash
pm2 update
```

# **Step 6: Restore the Previous PM2 State**

Reload the saved process list to restore your applications:

```bash
pm2 resurrect
```

# **Step 7: Re-enable PM2 Auto-Start**

If you want PM2 to start automatically on system reboot, reconfigure it with:

```bash
pm2 startup
```

Follow the on-screen instructions to complete the setup.

# **Step 8: Reload Applications with the New Node.js Version**

Finally, reload your applications with the updated environment variables:

```bash
pm2 reload <app-name or index> --update-env
```

# **Conclusion**

By following these steps, you can seamlessly update your Node.js version while ensuring that your PM2-managed applications continue running smoothly.

Let me know if you need further clarification! 🚀

### Refrences:

1. [PM2’s update documentation](https://pm2.keymetrics.io/docs/usage/update-pm2/)