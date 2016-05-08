# ����

�߽׺�����ָ����������������֮һ�ĺ�����

* ����������Ϊ���������ݣ�

* ����������Ϊ����ֵ�����

JavaScript�����еĺ�����Ȼ����߽׺�������������ʵ�ʿ����У������ǽ����������������ݣ������ú�����ִ�н����������һ�����������������ζ��кܶ�Ӧ�ó��������¾���һЩ�߽׺�����Ӧ�á�

# Ӧ��

## ��Ϊ��������

### ajax�첽����

```javascript
// callbackΪ������Ļص�����
var getUserInfo = function(userId, callback) {
     $.ajax("http://xxx.com/getUserInfo?" + userId, function(data) {
        if (typeof callback === "function") {
            callback(data);
        }
    });
}

getUserInfo(13157, function(data) {
    alert (data.userName);
});
```

### Array.prototype.sort

Array.prototype.sort����һ����������������������������װ������Ԫ�ص�������򡣴�Array.prototype.sort��ʹ�ÿ��Կ��������ǵ�Ŀ���Ƕ���������������ǲ���Ĳ��֣���ʹ��ʲô����ȥ�������ǿɱ�Ĳ��֡��ѿɱ�Ĳ��ַ�װ�ں����������̬����Array.prototype.sort��ʹArray.prototype.sort������Ϊ��һ���ǳ����ķ�����

```javascript
//��С��������
[1, 4, 3].sort(function(a, b) {
    return a - b;
});
// ���: [1, 3, 4]

//�Ӵ�С����
[1, 4, 3].sort(function(a, b) {
    return b - a;
});
// ���: [4, 3, 1]
```

## ��Ϊ����ֵ

### �ж����ݵ�����

```javascript
var Type = {};

for (var i = 0, type; type = ['String', 'Array', 'Number'][i++];) {
    (function(type) {
        Type['is' + type] = function(obj) {
            return Object.prototype.toString.call(obj) === '[object '+ type +']';
           }
       })(type)
};

Type.isArray([]);     // �����true
Type.isString("str");     // �����true
```

### ����ģʽ

```javascript
var getSingle = function(fn) {
    var ret;
    return function() {
        return ret || (ret = fn.apply(this, arguments));
    };
};
```

## ʵ��AOP

AOP�����������̣�����Ҫ�����ǰ�һЩ������ҵ���߼�ģ���޹صĹ��ܳ����������Щ��ҵ���߼��޹صĹ���ͨ��������־ͳ�ơ���ȫ���ơ��쳣����ȡ�����Щ���ܳ������֮����ͨ������̬֯�롱�ķ�ʽ����ҵ���߼�ģ���С��������ĺô������ǿ��Ա���ҵ���߼�ģ��Ĵ����͸��ھ��ԣ�����ǿ��Ժܷ���ظ�����־ͳ�Ƶȹ���ģ�顣

ͨ������JavaScript��ʵ��AOP������ָ��һ����������̬֯�롱������һ������֮�У������ʵ�ּ����кܶ࣬���������ͨ����չFunction.prototype��������һ�㡣

```javascript
Function.prototype.before = function(beforefn) {
    var __self = this;    // ����ԭ����������
    return function() {    // ���ذ�����ԭ�������º�����"����"����
        beforefn.apply(this, arguments);     // ִ���º���������this
        return __self.apply(this, arguments);    // ִ��ԭ����
    }
};

Function.prototype.after = function(afterfn) {
    var __self = this;
    return function() {
        var ret = __self.apply(this, arguments);
        afterfn.apply(this, arguments);
        return ret;
    }
};

var func = function() {
    console.log(2);
};

func = func.before(function() {
    console.log(1);
}).after(function() {
    console.log(3);
});

func();

// ��˳���ӡ��1��2��3
```

## currying

currying���������ﻯ�����ֳƲ�����ֵ��һ��currying�ĺ������Ȼ����һЩ��������������Щ����֮�󣬸ú���������������ֵ�����Ǽ�����������һ���������ղŴ���Ĳ����ں����γɵıհ��б���������������������������Ҫ��ֵ��ʱ��֮ǰ��������в������ᱻһ����������ֵ��

```javascript
// ͨ��currying����������һ������������Ҫ��currying�ĺ���
var currying = function(fn) {
    var args = [];
    return function() {
        if (arguments.length === 0) {
            return fn.apply(this, args);
        } else {
            [].push.apply(args, arguments);
            return arguments.callee;
        }
    }
};

// ����currying�ĺ���
var cost = (function() {
    var money = 0;
    return function() {
        for (var i = 0, l = arguments.length; i < l; i++) {
            money += arguments[i];
        }
        return money;
    }
})();

var cost = currying( cost );    // ת����currying����

cost( 100 );    // δ������ֵ
cost( 200 );    // δ������ֵ
cost( 300 );    // δ������ֵ

console.log (cost());     // ��ֵ�������600
```

## uncurrying

��JavaScript�У������ǵ��ö����ĳ������ʱ����ʵ����ȥ���ĸö���ԭ���Ƿ����Ϊӵ��������������Ƕ�̬�������Ե��ص㣬Ҳ�ǳ�˵��Ѽ������˼�롣

ͬ��һ������Ҳδ��ֻ��ʹ��������ķ�������ô��ʲô�취�����ö���ȥ����һ��ԭ�����������ķ����أ��𰸶���������˵�ܼ򵥣�call��apply������������������Ϊ��call��apply���԰����������this����ĳ������������һ�����������õ�this�ĵط��Ͳ��پ�����ԭ���涨�Ķ��󣬶��Ǽ��Է������õ�����������ԡ�

��uncurrying��Ŀ���ǽ�����this�Ĺ�����ȡ��������fn.call����fn.apply�����ͨ�õĺ�����

```javascript
// uncurryingʵ��
Function.prototype.uncurrying = function() {
    var self = this;
    return function() {
        return Function.prototype.call.apply(self, arguments);
    }
};

// ��Array.prototype.push����uncurrying����ʱpush���������þ͸�Array.prototype.pushһ���ˣ��Ҳ�����������ֻ�ܲ���array����
var push = Array.prototype.push.uncurrying();

var obj = {
    "length": 1,
    "0": 1
};

push(obj, 2);
console.log(obj);   // �����{0: 1, 1: 2, length: 2}
```

## ��������

��һ��������Ƶ������ʱ���������ɺܴ�����������ʱ�����ʱ����Կ��Ǻ������������ͺ��������õ�Ƶ�ʡ�

throttle������ԭ���ǣ���������ִ�еĺ�����setTimeout�ӳ�һ��ʱ��ִ�С�����ô��ӳ�ִ�л�û����ɣ�����Խ��������øú���������throttle��������2����������һ������Ϊ��Ҫ���ӳ�ִ�еĺ������ڶ�������Ϊ�ӳ�ִ�е�ʱ�䡣

```javascript
var throttle = function(fn, interval) {
    var __self = fn,    // ������Ҫ���ӳ�ִ�еĺ�������
        timer,      // ��ʱ��
        firstTime = true;    // �Ƿ��ǵ�һ�ε���

    return function() {
        var args = arguments,
            __me = this;

        if (firstTime) {    // ����ǵ�һ�ε��ã������ӳ�ִ��
            __self.apply(__me, args);
            return firstTime = false;
        }

        if (timer) {    // �����ʱ�����ڣ�˵��ǰһ���ӳ�ִ�л�û�����
            return false;
        }

        timer = setTimeout(function() {  // �ӳ�һ��ʱ��ִ��
            clearTimeout(timer);
            timer = null;
            __self.apply(__me, args);
        }, interval || 500 );
    };
};

window.onresize = throttle(function() {
    console.log(1);
}, 500 );
```

## ��ʱ����

��һ�ε��û����������ص�Ӱ��ҳ�����ܣ����ڶ�ʱ������ҳ���д������DOM�ڵ���ȻҲ����������Բ��������ǿ����Ľ����������������Ŀ�������������

�������Ľ������֮һ�������timeChunk������timeChunk�����ô����ڵ�Ĺ����������У������1���Ӵ���1000���ڵ㣬��Ϊÿ��200���봴��8���ڵ㡣

timeChunk��������3����������1�������Ǵ����ڵ�ʱ��Ҫ�õ������ݣ���2�������Ƿ�װ�˴����ڵ��߼��ĺ�������3��������ʾÿһ�������Ľڵ�������

```javascript
var timeChunk = function(ary, fn, count) {
    var t;

    var start = function() {
        for ( var i = 0; i < Math.min( count || 1, ary.length ); i++ ){
            var obj = ary.shift();
            fn( obj );
        }
     };

     return function() {
        t = setInterval(function() {
          if (ary.length === 0) {  // ���ȫ���ڵ㶼�Ѿ���������
              return clearInterval(t);
          }
          start();
        }, 200);    // ����ִ�е�ʱ������Ҳ�����ò�������ʽ����
    };
};
```

## ���Լ��غ���

��Web�����У���Ϊ�����֮���ʵ�ֲ��죬һЩ��̽�������ǲ��ɱ��⡣����������Ҫһ���ڸ�����������ܹ�ͨ�õ��¼��󶨺���addEvent��������д�����£�

**����һ��**
```javascript
var addEvent = function(elem, type, handler) {
    if (window.addEventListener) {
       return elem.addEventListener(type, handler, false);
    }
    
    if (window.attachEvent) {
          return elem.attachEvent('on' + type, handler);
    }
};
```
ȱ�㣺����ÿ�α����õ�ʱ�򶼻�ִ�������if������֧����Ȼִ����Щif��֧�Ŀ�������󣬵�Ҳ����һЩ���������ó��������Щ�ظ���ִ�й��̡�

**��������**
```javascript
var addEvent = (function() {
    if (window.addEventListener) {
        return function(elem, type, handler) {
            elem.addEventListener(type, handler, false);
        }
    }
    if (window.attachEvent) {
        return function(elem, type, handler) {
            elem.attachEvent('on' + type, handler);
        }
    }
})();
```
ȱ�㣺Ҳ�����Ǵ�ͷ��β��û��ʹ�ù�addEvent����������������һ��ʼ���������̽������ȫ����Ĳ�����������Ҳ�������ӳ�ҳ��ready��ʱ�䡣

**��������**
```javascript
var addEvent = function(elem, type, handler) {
        if (window.addEventListener) {
           addEvent = function(elem, type, handler) {
               elem.addEventListener(type, handler, false);
           }
        } else if (window.attachEvent) {
            addEvent = function(elem, type, handler) {
                elem.attachEvent('on' + type, handler);
            }
        }
        addEvent(elem, type, handler);
    };
```
��ʱaddEvent��Ȼ������Ϊһ����ͨ�������ں�������Ȼ��һЩ��֧�жϡ������ڵ�һ�ν���������֧֮���ں����ڲ�����д�����������д֮��ĺ�����������������addEvent����������һ�ν���addEvent������ʱ��addEvent�����ﲻ�ٴ���������֧��䡣