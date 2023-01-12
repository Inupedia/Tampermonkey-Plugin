# Tampermonkey-Plugin

| Plugin                                                 | Function                             |
| ------------------------------------------------------ | ------------------------------------ |
| [Get Emails](#get-emails)                              | Scrape all emails from single page   |
| [Default Youtube PlaySpeed](default-youtube-playspeed) | Set you custom playspeed for YouTube |

#### Get Emails

```javascript
// ==UserScript==
// @name         Get Email
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  try to take over the world!
// @author       You
// @match        *://*/*
// @grant        none
// ==/UserScript==


function createMessageBoard(emails) {
	var messageBoard = document.createElement("p");
    messageBoard.innerHTML = emails;
    document.body.insertBefore(messageBoard, document.body.firstChild);
    // document.body.appendChild(messageBoard);
}

function createButton() {

	var y = document.createElement("BUTTON");
	y.onclick = function() {
	    var search_in = document.body.innerHTML;
	    var string_context = search_in.toString();
	    var array_mails = string_context.match(/([a-zA-Z0-9._-]+@[a-zA-Z0-9._-]+\.[a-zA-Z0-9._-]+)/gi);
	  	// console.log("you click get emails");
		// return array_mails;
	    return createMessageBoard(array_mails);
	};
	y.innerText = "Get Email";
	document.body.insertBefore(y, document.body.firstChild);
	// document.body.appendChild(y);

	var x = document.createElement("BUTTON");
	x.onclick = function() {
	    const elements1 = document.querySelectorAll(`[id^="adressSelector"]`);
	    for (let i = 0; i < elements1.length; i++) {
	      elements1[i].children[0].click()
	    }
	};
	x.innerText = "Unhide";
	document.body.insertBefore(x, document.body.firstChild);
	// document.body.appendChild(x);
};

createButton();
```

#### Default Youtube PlaySpeed

```javascript
// ==UserScript==
// @name         Youtube PlaySpeed Default
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  Allows you to set custom playspeed
// @author       Inupedia
// @match        https://www.youtube.com/*
// @grant        none
// ==/UserScript==

let defaultSpeed = 1;

function hasVideo() {
    return document.getElementsByClassName("ytp-right-controls").length != 0;
}

function setRate(n) {
        document.getElementsByClassName("html5-video-container")[0]
        .getElementsByClassName("video-stream html5-main-video")[0]
        .playbackRate = n;
    }

function main() {
    window.setInterval(function(){
        var controller = document.getElementById('spdctrl');
        if (controller === null && hasVideo()) {
            setRate(defaultSpeed);
        }
    }, 300);
}

main();
```

