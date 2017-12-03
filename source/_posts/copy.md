---
title: 对象深拷贝
date: 2016-11-25 10:09:43
categories: 前端
tags: 前端
---

1. 深浅拷贝包含,jq等框架实现方法
```javascript
function mix(){
    var options, name, src, copy, copyIsArray, clone,
        target = arguments[0] || {},
        i = 1,
        length = argument.length,
        deep = false;

    //判断是否为深拷贝
    if(typeof target === 'boolean') {
        deep = target;
        target = arguments[1] || {};
        i++ 
    }

    if(typeof target !== 'object' && !isFunction(target)){
        target = {};
    }

    for(; i < length; i++){
        if((options = arguments[i]) != null){
            for (name in options){
                try{
                    src = target[name];
                    copy = options[name];
                }catch(e){  
                    continue
                }

                if(target === copy){
                    continue
                }

                if(deep && copy && (isPlainObject(copy) || (copyIsArray = Array.isArray(copy)))){
                    if(copyIsArray){
                        copyIsArray = false;
                        clone = src && Array.isArray(src) ? src : [];
                    }else{
                        clone = src && isPlainObjrct(arc) ? src : {};
                    }
                    
                    target[name] = mix(deep, clone, copy);
                }else if(copy !== void 0){
                    target[name] = copy;
                }
            }
        }
    }
    return target;
}
```
2. 其中上面用到了判断是否为纯净对象和函数类型的方法，分别实现以下

```javascript
function isFunction(fn){
    return (!!fn&&!fn.nodename&&fn.constructor!=String&&fn.constructor!=RegExp&&fn.constructor!=Array&&/function/i.test(fn+""));
}

//或者更简单的
function isFunction(fn) {
   return Object.prototype.toString.call(fn)=== '[object Function]';
}
//jq实现
function isPlainObject(obj){
    if(jQuery.type(obj) !== 'object' || obj.nodeType || jQuery.isWindow(obj)){
        return false;
    }

    try{
        if(obj.constructor && !hasOwn.call(obj.constructor.prototype, 'isPrototypeOf')){
            return false;
        }
    }catch(e){
        return false;
    }

    return true;
}
```

3. Object.assign实现
```javascript
    function toObject(val){
        if(val == null){
            throw new TypeError('the val type cannot null')
        }
        return Object(val);
    }
    function assign(target,source){
        var from;
        var keys;
        var to = ToObject(target);

        for(var s = 1; s < arguments.length; s++){
            from = arguments[s];
            keys = Object.keys(Object(from));

            for(var i = 0; i < keys.length; i++){
                to[keys[i]] = from[key[i]];
            }
        }

        return to;
    }
```
