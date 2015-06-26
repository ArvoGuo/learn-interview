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