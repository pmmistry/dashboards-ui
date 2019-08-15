---
description: >-
  In this lab we will be working with Node-RED on the IBM cloud. This setup
  tutorial will show you how to install dashboard nodes in your cloud instance
  of Node-RED .
---

# Installing Dashboards into Node-RED Cloud Instance

## Installing Dashboard Nodes 

![](../.gitbook/assets/screen-shot-2019-08-07-at-7.15.16-pm.png)

**Step 1.** Search for the instance of the Node-RED starter kit you created on IBM Cloud 

![](../.gitbook/assets/screen-shot-2019-08-07-at-7.16.55-pm.png)

**Step 2.** Scroll down to Continuous delivery and click on View toolchain 

![](../.gitbook/assets/screen-shot-2019-08-07-at-7.17.31-pm.png)

**Step 3**.  Click on Git box under Code 

![](../.gitbook/assets/screen-shot-2019-08-07-at-7.18.11-pm.png)

**Step 4** . Once in Git click on package.json 

![](../.gitbook/assets/screen-shot-2019-08-07-at-7.19.41-pm.png)

**Step 5.** Edit package.json dependancies. Add : 

```text
"node-red-dashboard":"2.x" 
```

in the dependency list as so and commit changes 

![](../.gitbook/assets/screen-shot-2019-08-07-at-7.20.21-pm.png)

**Step 6.** Once change is committed, launch the App url once again. Click on the hamburger menu &gt;   Manage Palette section and then search for dashboard nodes. You should see  node-red-dashboard. Click install and you should successfully see dashboard pallet on your Node-RED editor



![](../.gitbook/assets/screen-shot-2019-08-07-at-7.21.02-pm.png)

![](../.gitbook/assets/screen-shot-2019-08-07-at-7.22.16-pm.png)



