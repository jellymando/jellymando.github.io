---
title: "onUnload 이벤트에서 새로고침과 창 닫힘 구분"
categories: [Javascript]
tags: [javascript]
---

{:toc .large-only}

~~~js
function handleUnload()
{
    if (self.screenTop > 9000)
   {
      // 브라우저 닫힘
    }
    else
    {
        if (document.readyState == "complete")
        {
            // 새로고침
        }
         else  if (document.readyState == "loading")
        {
           // 다른 사이트로 이동
         }
}

window.addEventListener('unload', handleUnload);
~~~

<br/>
unload할 때, `document.readyState` 가 complete면 새로고침으로 판단한다.

<br/>
[onUnload 이벤트에서 새로고침과 창 닫힘 구분](https://globalhost.interdol.com/156)