---
layout: post
title:  "QR Code Generator"
subtitle: "Lightning Web Component"
author: "@21rathishivani"
avatar: "https://pbs.twimg.com/profile_images/918403501729890304/ULEIJDfY_400x400.jpg"
image: "/img/d.jpg"
date:   2019-06-14 12:12:12
author_name: Shivani Rathi
category: 'Snippets'
tags: 'Salesforce QR-Code'
---
Lightning Web Component: QR Code in Salesforce
----------------------------------------------

As a developer, some of you might have needed to generate QR code for your Salesforce applications. Traditionally, we all have used APIs for this purpose as they are very simple and easy to implement. For a recent requirement, I used the same approach for generation of QR Code in my Lightning Web Component. But what if they get deprecated? So, I tried creating ES6 code for the generation of QR-Code in my Lightning Web Component.  
  
For this, you just need to pass a string for which the QR-Code will be generated and displayed on the UI of your component.  
  
There are 4 simple steps through which you can generate the QR-Code.  

1.  Create a Lightning Web Component
2.  Add a module to the component named **qrcode.js** in the same folder as your LWC. Paste the following code in qrcode.js file:  
    Copy the **qrcode.js** file from folder path [GitHub](https://github.com/shivanirathi21/LWC-QRCode)  
    (link to file can be found within [qrcode.js](https://github.com/shivanirathi21/LWC-QRCode/blob/master/qrcode.js)  
    
3.  Import the Module added in the **components.js** file to your components js file as shown in the snippet below:  
      
      
    ![JS Controller](https://www.eternussolutions.com/wp-content/uploads/2019/06/QR_code1.png)
    
    **Img2 – JS Controller Of The Component**  
      
    
      
    
4.  Now add the following code to your HTML file:  
      
      
    ![HTML markup of the controller](https://www.eternussolutions.com/wp-content/uploads/2019/06/QR_code2.png)
    
    **Img2 – HTML Markup Of The Controller**  
      
![Generated QR code](https://www.eternussolutions.com/wp-content/uploads/2019/06/QR_code3.png)

**Img2 – Generated QR Code**  
  
There you go… You have successfully created the QR-Code in your LWC!  
  
Here is the link to the code base for your reference: [https://github.com/shivanirathi21/LWC-QRCode](https://github.com/shivanirathi21/LWC-QRCode)  
  
Give it a shot and let me know all about it.  
  
  
  
Written by **Shivani Rathi**, Systems Executive at Eternus Solutions_
