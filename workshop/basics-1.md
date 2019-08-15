---
description: >-
  Node-RED is an awesome tool that makes prototyping a lot faster and easier!
  Node-RED is very easy to get started with and is a great tool for beginners
  who want to write and understand programming
---

# Basics

Node-RED provides lot of tools and plugins which supports almost everything related to programming. It can be used for APIs, DataBase, IOTIntro to IBM's Node-RED, WebSockets, Emails, Scripting, Image Processing, Cloud computing, edge computing, creating websites and lot more one can think of doing it based on NodeJS. 

Once you have Node-RED set up on your IBM Cloud Account you can create your first flow

### Steps to Create Flows  <a id="steps-to-create-flows"></a>

#### Step 1. Add an Inject node  <a id="step-1-add-an-inject-node"></a>

The Inject node allows you to inject messages into a flow, either by clicking the button on the node, or setting a time interval between injects.

Drag one onto the workspace from the palette.

Open the sidebar \(Ctrl-Space, or via the dropdown menu\) and select the Info tab.

Select the newly added Inject node to see information about its properties and a description of what it does.

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LhCRb6QNiVWF6s9FafQ%2F-LhID4xrr3l4mDQPbc5X%2F-LhIL7C8zoOV4kYjfSZG%2Fimage.png?alt=media&token=6b403d0c-be36-41b0-80cf-63dfe84a2cab)

#### Step 2. Add a Debug Node  <a id="step-2-add-a-debug-node"></a>

The Debug node causes any message to be displayed in the Debug sidebar. By default, it just displays the payload of the message, but it is possible to display the entire message object.

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LhCRb6QNiVWF6s9FafQ%2F-LhID4xrr3l4mDQPbc5X%2F-LhIMBAiM_zP_3nBdJCH%2Fimage.png?alt=media&token=63340221-ad6f-40b0-a6d5-9e9c4603bf8d)

#### Step 3. **Wire the two together** <a id="step-3-wire-the-two-together"></a>

Connect the Inject and Debug nodes together by dragging between the output port of one to the input port of the other.

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LhCRb6QNiVWF6s9FafQ%2F-LhID4xrr3l4mDQPbc5X%2F-LhIMQmrM1FYJ-QYZD5W%2Fimage.png?alt=media&token=ac12acea-c040-4b9e-b50c-c8e755d7fd3b)

#### **Step 4. Deploy**  <a id="step-4-deploy"></a>

At this point, the nodes only exist in the editor and must be deployed to the server.

Click the Deploy button. Simple as that.

With the Debug sidebar tab selected, click the Inject button. You should Hello World Selected in the Side Bar. Let’s do something more useful with that.

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LhCRb6QNiVWF6s9FafQ%2F-LhID4xrr3l4mDQPbc5X%2F-LhIMsIr2IClUnuHXHPb%2Fimage.png?alt=media&token=547d0c5a-e74b-4f2f-bdd6-8240de2adb17)

#### Step 5. **Add a Function node** <a id="step-5-add-a-function-node"></a>

The Function node allows you to pass each message though a JavaScript function.

Wire the Function node in between the Inject and Debug nodes. You may need to delete the existing wire \(select it and hit delete on the keyboard\).

Double-click on the Function node to bring up the edit dialog. Copy the follow code into the function field:

```text
var newString = msg.payload.replace("World","Everyone , I hope you enjoy Node Red ");return {payload : newString};
```

![](https://blobscdn.gitbook.com/v0/b/gitbook-28427.appspot.com/o/assets%2F-LhCRb6QNiVWF6s9FafQ%2F-LhID4xrr3l4mDQPbc5X%2F-LhINKFNoVX6YYnjfmEH%2Fimage.png?alt=media&token=af1d0197-9c2e-451c-874f-d372f1cecff5)



