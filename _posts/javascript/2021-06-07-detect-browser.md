---
title: "Detect Browser - 브라우저, 버전 감지하기"
categories: [Javascript]
tags: [javascript]
---

{:toc .large-only}

### 브라우저 구하기

```js
const detectBrowser = (reg) => {
  return reg.test(navigator.userAgent);
};

const isChrome = detectBrowser(/chrome|crios|crmo/i);
const isChromium = detectBrowser(/chromium/i);
const isSafari = detectBrowser(/^((?!chrome|android).)*safari/i);
const isFirefox = detectBrowser(/firefox|iceweasel|fxios/i);
const isOpera = detectBrowser(/opera|opios/i);
const isSamsung = detectBrowser(/SamsungBrowser/i);
```

### 브라우저 버전 구하기

```js
const detectBrowserVersion = function (reg) {
  if (!reg) reg = /version\/(\d+(\.?_?\d+)+)/i;
  const match = navigator.userAgent.match(reg);
  return (match && match.length > 0 && match[1]) || "";
};

const isChromeVersion =
  detectBrowserVersion(/(?:chrome|crios|crmo)\/(\d+(\.?_?\d+)+)/i);
const isChromiumVersion =
  detectBrowserVersion(/(?:chromium)[\s/](\d+(\.?_?\d+)+)/i);
const isSafariVersion =
  detectBrowser(/^((?!chrome|android).)*safari/i) &&
  detectBrowserVersion();
const isFirefoxVersion =
  detectBrowserVersion(/(?:firefox|iceweasel|fxios)[\s/](\d+(\.?_?\d+)+)/i);
const isOperaVersion = detectBrowserVersion(/(?:opr|opios)[\s/](\S+)/i);
const isSamsungVersion =
  detectBrowserVersion(/(?:SamsungBrowser)[\s/](\d+(\.?_?\d+)+)/i);
```

[parser-browsers.js](https://github.com/lancedikson/bowser/blob/master/src/parser-browsers.js)<br/>
[Detect safari and stop script](https://stackoverflow.com/questions/49872111/detect-safari-and-stop-script)
