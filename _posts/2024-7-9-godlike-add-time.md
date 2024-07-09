---
layout: post
title: "vps自动加时"
date: 2024-07-09
description: "vps自动加时"
tag: python
---  
白嫖了一款vps，是游戏服务器，但是得需要手动加时，且时间不能超过24小时，为了省心省力编制了一段JavaScript程序，自动点击加时按钮。

代码如下：

```
// ==UserScript==
// @name         godlike add time
// @namespace    http://tampermonkey.net/
// @version      1.0
// @description  自动点击特定网页上的按钮
// @author       Your Name
// @match        https://panel.godlike.host/server/*
// @grant        none
// ==/UserScript==

(function() {
    'use strict';

    // Function to click the first and second buttons with a 1-second delay between them
    function clickButtons() {
        // Select the first button
        const firstButton = document.querySelector('#app > div.App___StyledDiv-sc-2l91w7-0.fnfeQw > div.Fade__Container-sc-1p0gm8n-0.hcgQjy > section > div > div.ServerConsole___StyledDiv4-sc-13p0yj4-8.dHxIwk > div.ServerConsole___StyledDiv8-sc-13p0yj4-17.klSohe > div.ServerConsole___StyledDiv10-sc-13p0yj4-19.gGcgPZ.rightStack > div:nth-child(1) > div.ServerConsole___StyledDiv14-sc-13p0yj4-27.cGynSo > div > button');
        if (firstButton) {
            firstButton.click();
            console.log('First button clicked');

            // Delay 2 second before clicking the second button
            setTimeout(() => {
                const secondButton = document.querySelector('#modal-portal > div:nth-child(2) > div > div > div.Modal___StyledDiv2-sc-9vzni8-3.ekHIsr > button');
                if (secondButton) {
                    secondButton.click();
                    console.log('Second button clicked');
                } else {
                    console.log('Second button not found');
                }
            }, 2000);
        } else {
            console.log('First button not found');
        }
    }

    // Run the clickButtons function every 6 minutes (360000 milliseconds)
    setInterval(clickButtons, 6*60*1000);
    // Optionally, click buttons once when the script first runs
    //clickButtons();
})();

```
把以上程序，考入油猴运行，即可实现自动点击加时。
