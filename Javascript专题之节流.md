# 节流
    在连续一段时间内触发，在这段时间内只执行一次；
    节流常用的方式有两种：时间戳和设置定时器。

## 时间戳方式
    时间戳方式，触发立马执行，不会执行最后一次
``` bash
    function throttle(func, wait) {
            let previous = 0;
            return (...args) => {
                const now = +new Date();
                if (now - previous >= wait) {
                    previous = now;
                    func(...args);
                }
            }
        }
```
## 设置定时器方式
``` bash
    function throttle(func, wait) {
        let timer = null;
        return (...args) => {
            if (timer) return;
            timer = setTimeout(() => {
                console.log(timer);
                clearTimeout(timer);
                timer = null;
                func(...args);
            }, wait);
        }
    }
```

## 双剑合璧 
    通过 leading 判断是否执行第一次； 通过 trailing 判断是否执行最后一次； 通过 cancel 取消定时器

    ``` bash
        function throttle(func, wait, options = {}) {
            let timer = null, previous = 0;
            
            const later = (...args) => {
                clearTimeout(timer);
                timer = null;
                func(...args);
            }
            const _throttle = (...args) => {

                const now = +new Date();
                previous = options.leading === false ? now : previous;
                const remaining = wait - (now - previous);
                if (remaining <= 0 || remaining > wait) {
                    if (timer) {
                        clearTimeout(timer);
                        timer = null;
                    };

                    previous = now;
                    func(...args);
                } else if (!timer || options.trailing !== false) {
                    if (timer) return;
                    timer = setTimeout(later, wait);
                }
            }
            _throttle.cancel = () => {
                clearTimeout(timer);
                timer = null;
            }

            return _throttle;
        }
    ```
