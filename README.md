写一个深克隆
----------

```javascript
function deepClone(obj) {
  var copy;
  if (null == obj || typeof obj !== 'object') {
    return obj;
  }

  if (obj instanceof Date) {
    copy = new Date();
    copy.setTime(obj.getTime());
    return copy;
  }

  if (obj instanceof Array) {
    copy = [];
    for (var i = 0, len = obj.length; i < len; i ++) {
      copy[i] = deepClone(obj[i]);
    }
    return copy;
  }

  if (obj instanceof Object) {
    copy = {};
    for(var attr in obj) {
      if (obj.hasOwnProperty(attr)) {
        copy[attr] = deepClone(obj[attr]);
      }
    }
    return copy;
  }

}
```

写一个indexOf
------------

```javascript
String.prototype.indexOf = function(str) {
  var reg = new RegExp(str, 'g');
  var result = [];
  while(reg.exec(this.toString()) !== null) {
    result.push(reg.lastIndex);
  }
  return result;
}
```

load 和 ready
------------

```javascript
document.onload = function() {
  //所有资源加载完 包括大量图片
  //此时document.readystatus == "complete"
}

$(document).ready = function() {
  //这个方法大致的思路是
  // if (document.readystatus == "complete"), 就执行回调
  // else  addEventListener('DOMContentLoaded', 回调),
  //DOMContentLoaded事件要在window.onload之前执行，当DOM树构建完成的时候就会执行DOMContentLoaded事件，
  //而window.onload是在页面载入完成的时候，才执行，这其中包括图片等元素。大多数时候我们只是想在DOM树构建完成后，绑定事件到元素，我们并不需要图片元素，加上有时候加载外域图片的速度非常缓慢。
  //对于IE 不支持 DOMContentLoaded事件， 采用doScroll的hack
}

```

为什么不把css放在页面底部
---------------------

在网络延迟下，会造成用户先看到无css样式的 dom结构，就像平时xxx.css没有加载到一样, 接着加载完css后会再绘制页面。

为什么把script放在</body>前
------------------------

1.从标准上讲， 新的html规范认为body闭合标签之后出现script或其他元素的开始标签，都是parse error，浏览器会忽略之前的</body>, 默认去包涵后来出现的内容在</body>内。

2.从页面加载上来讲，页面是自上而下的加载，如果中间出现script就会阻塞，去加载和解析完成后，再解析后面的dom

script放在</body>前，onload， ready 的区别
----------------------------------------

这个问题本身就混杂了以上两个问题，需要脑袋清晰－ － ，不然就乱了。

常见路由控制的方法
--------------------

window.onpopstate 监听
history.pushState 改变

对于不支持的浏览器，简单的方式 就是settimeout。。




