---
layout: post
title: Removing the Server header from Azure websites
categories: azure
description: Removing the server response header from Azure websites
---
To remove the Server header from Azure websites add the following section to system.webServer in the web.config
Local IIS will complain!


    <security>
      <requestFiltering removeServerHeader ="true" />
    </security>`

[Response headers via @troyhunt](http://www.troyhunt.com/2012/02/shhh-dont-let-your-response-headers.html)