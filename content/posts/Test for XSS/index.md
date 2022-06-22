---
title: "Interesting XSS by changing the Username of socialmedia handle"
date:  2022-05-02 01:47:04 +0800
description: 
menu:
  sidebar:
    name: Stored XSS by Instagram username
    identifier: SSTI
    weight: 10
tags: [ "XSS"]
categories: ["bugbounty"]
---



Hello everyone, I hope you're doing well and staying healthy. I was working on a target a few days ago when I discovered an interesting stored XSS with a link account functionality in the target web application.

## How the application works ?

The application is based on the medical e-commerce model, and it sells medicinal products and medical supplies. The application provides several roles, including shop owner, buyer, and manager. The shop owner has a separate panel to evaluate when creating a static web application to sell their products. The manager role has only two steps, such as the seller creating static sites for their products to sell and the manager role people validating the products and doing background checks on the seller in order to provide a better platform to avoid people being scammed or cheated by the fake seller.

## How I found this Vulnerability ?

Initially, I began looking for vulnerabilities as a high-privileged user such as a seller or manager, looking for IDORs, broken access controls, and authentication-related issues, but I had little success, literally nothing. But I questioned myself. There is file upload functionality available, and I can upload any type of file, but the image loads in blob storage and does not execute. Later on, as a normal user, I began looking around and discovered that there is functionality in this application that allows us to link approximately 5 to 7 third-party applications such as Facebook, Twitter, LinkedIn, Instagram, and so on.

> What comes next? , Initially, when the application connects to a third-party application. The thirty-party application username will be rendered in the target application.

So, everyone's spider sense has been activated, haha, and you've figured out what the problem is? Yes, let's talk about it further.

![](https://media.giphy.com/media/clspXK4twFiGjTwxOZ/giphy.gif)

## How I exploited this Vulnerability ?

* As previously stated, when a user links a third-party account, such as Instagram, I'm going to link my Instagram account to the current application. Once the link between the current application and the third-party applicant has been established. The third-party applicant's user name will now be reflected in the current application.

> As an example, If my Instagram username is nithissh and I have linked my Instagram account to my current app. Now, when I view the profile, the application will display my Instagram username in the user profile.

* Now, whenever the text is reflected in the response page, we will always consider testing for XSS. So I came up with the idea of changing my Instagram username to an XSS payload and re-linked the instagram.

> To clarify, my current Instagram handle is nithissh. So, I changed the username from **nithissh** to **<img src=x onerror=confirm(document.location)>** to see what happens.

* After changing the username of my Instagram account to an XSS payload and linking the account to my current application, the application executed the code and the XSS was triggered.

![](https://media.giphy.com/media/1kTO4jMLAF08AEIaSl/giphy-downsized-large.gif)

> What exactly is the thought process here? , Everyone will have the same thought, right? Whenever the application displays a value or text on the response page. Always check the source code to see where it was reflected. Is it being sterilised? If not, try an XSS. It will undoubtedly work; however, do not rely on bypass payloads xD.


## Conclusion

This vulnerability, like a site-wide stored XSS, affects other users, administrators, sellers, and managers. The irony is that it was fired in the internal admin panel. 
The vulnerability is strange and intriguing to me; if you were previously aware of it, that's fantastic.

**Thanks for reading my writeup and I hope you have learned something new**

![](https://media.giphy.com/media/3o7TKr0sYduhblYBgY/giphy.gif)
