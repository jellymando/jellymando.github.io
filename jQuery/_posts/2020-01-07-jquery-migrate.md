---
layout: post
title: "jQuery Migrate로 버전 업그레이드🐡"
sitemap: false
---

{:toc .large-only}

## 🚃 jQuery 1.7.2를 3.5.0로 업그레이드 하는 여정

<br/>

1. jQuery 파일을 1.12.4로 바꾸고 Migrate 1.4.1를 추가한다.

[jQuery 1.12.4 다운로드](https://blog.jquery.com/2016/05/20/jquery-1-12-4-and-2-2-4-released/)<br/>
[jQuery migrate 1.4.1 다운로드](https://code.jquery.com/jquery/#jquery-migrate-all)
<br/><br/>

2. Migrate warning messages에 따라 에러를 잡는다.

   [Migrate 1.x warning messages](https://github.com/jquery/jquery-migrate/blob/1.x-stable/warnings.md)<br/>
   [jQuery Core 1.9 Upgrade Guide](https://jquery.com/upgrade-guide/1.9/)
   <br/><br/>

3. jQuery 파일을 3.5.1로 바꾸고 Migrate 3.3.2를 추가한다.

   [jQuery 3.5.1 다운로드](https://blog.jquery.com/2020/05/04/jquery-3-5-1-released-fixing-a-regression/)<br/>
   [jQuery migrate 3.3.2 다운로드](https://github.com/jquery/jquery-migrate/#download)<br/>
   [jQuery 가장 최신 버전 다운로드](https://jquery.com/download/)
   <br/><br/>

4. Migrate warning messages에 따라 에러를 잡는다.

   [Migrate 3.x warning messages](https://github.com/jquery/jquery-migrate/blob/master/warnings.md)<br/>
   [jQuery Core 3.0 Upgrade Guide](https://jquery.com/upgrade-guide/3.0/)<br/>
   [jQuery Core 3.5 Upgrade Guide](https://jquery.com/upgrade-guide/3.5/)
   <br/><br/>

## 🗒 수정사항 노트

## Ajax()

- [**jqXHR**](https://jquery.com/upgrade-guide/3.0/#ajax)

`$.ajax()` 에서 반환 된 jqXHR 개체는 Promise 인터페이스를 구현하여 Promise의 모든 속성, 메서드 및 동작을 제공합니다.
이러한 메서드는 `$.ajax()` 요청이 종료 될 때 호출되는 하나 이상의 함수 인수를 사용합니다.

> `jqXHR.success()` `jqXHR.error()` 및 `jqXHR.complete()` 콜백은 jQuery를 3.0에서 제거됩니다.<br/>대신 `jqXHR.done()`, `jqXHR.fail()` 그리고 `jqXHR.always()` 을 사용할 수 있습니다.

[jQuery.ajax](https://api.jquery.com/jQuery.ajax/)

## Attributes

- **.removeAttr() no longer sets properties to false**

checked, selected 속성에 대해 .removeAttr()를 사용하면 명명된 해당 속성을 false로 설정할 수 있었습니다.
3.0부터는 `.removeAttr("checked")` 대신 `.prop("checked", false)` 를 사용합니다.
checked, selected, disabled, readonly 등에 적용됩니다.

<br/>
- **.toggleClass( Boolean )**

[.toggleClass([state])는 3.0부터 사용되지 않습니다.](https://api.jquery.com/toggleclass/#toggleClass2)

## Core

- **'ready' event is deprecated**

'ready' 이벤트는 더 이상 사용되지 않습니다.

`$(document).on("ready", function(){})` 를 `$(document).ready(function(){})` 나 그냥 `$(function(){})` 로 변경할 수 있습니다.

<br/>
- **jQuery.fn.live() is deprecated**

`.live()` 및 `.die()` 는 1.7부터 더 이상 지원되지 않으며 대신 `.on()` 나 `.delegate()` 을 사용합니다.

<br/>
- **.size() removed**

`.size()`는 1.8부터 더 이상 사용되지 않으며 대신 `.length` 을 사용합니다.

<br/>
- **jQuery.parseJSON()**

jQuery 3.0 기준 `$.parseJSON()` 은 더 이상 사용되지 않습니다. JSON 문자열을 구문 분석하려면 `JSON.parse()` 메서드를 사용하십시오.

```js
// $.parseJSON
var obj = jQuery.parseJSON('{ "name": "John" }');
// JSON.parse
var obj = JSON.parse('{ "name": "John" }');
```

<br/>
- **.bind() and .delegate()**

`.bind()` `.unbind()` `.delegate()` `.undelegate()` 는 3.0부터 `.on()` 또는 `.off()` 로 변경됩니다.

<br/>
- **jQuery.fn.click() event shorthand is deprecated**

`.on()` 및 `.trigger()` 메서드는 모든 이벤트 유형에 대해 이벤트 핸들러를 설정하거나 이벤트를 생성할 수 있으므로 shortcut 메서드 대신 사용해야 합니다.

이 메시지는 `blur, focus, focusin, focusout, resize, scroll, dblclick, mousedown, mouseup, mousemove, mouseover, mouseout, mouseenter, mouseleave, change, select, submit, keydown, keypress, keyup, and contextmenu` 를 포함한 다른 이벤트에도 적용됩니다.

`.click(fn)` 대신 `.on("click", fn)` 사용 / `.click()` 대신 `.trigger("click")` 사용합니다.

<br/>
- **jQuery.isFunction() has been deprecated**

jQuery 3.3부터 `jQuery.isFunction()` 은 더 이상 사용되지 않습니다. 대신 `typeof x === "function"` 을 사용할 수 있습니다.

```js
var fn = function () {};

// old
jQuery.isFunction(fn);

// new
typeof fn === "function";
```
