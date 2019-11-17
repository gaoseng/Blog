# 防抖
    防抖的原理就是：你尽管触发事件，但是我一定在事件触发 n 秒后才执行，如果你在一个事件触发的 n 秒内又触发了这个事件，那我就以新的事件的时间为准，n 秒后才执行，总之，就是要等你触发完事件 n 秒内不再触发事件，我才执行，真是任性呐!
## 第一版 
    

    ```bash
        function debounce (fn, wait) {
            let timer = null;
            return (...args) => {
                clearTimeout(timer);
                timer = setTimeout(() => {
                    fn(...args);
                }, wait)
            }
        }

    ```

## 第二版
    需求： 需要在调用的时候立即执行函数， 然后在n秒之后再执行一次；

    ```bash
        function debounce(fn, wait, immediate) {
            let timer = null;
            return (...args) => {

                if (timer) clearTimeout(timer);

                if (immediate) {
                    const canRun = !timer;
                    timer = setTimeout(() => {
                        timer = null;
                        fn(...args);   
                    }, wait);
                    if (canRun) fn(...args);
                } else {
                    timer = setTimeout(() => {
                        fn(...args);
                    }, wait)
                }

            }
        }
    ```

### 第三版
    需求： 需要一个方法，清除定时器

    ```bash
        function debounce(fn, wait, immediate) {
            let timer = null;
            const debounded =  (...args) => {

                if (timer) clearTimeout(timer);

                if (immediate) {
                    const canRun = !timer;
                    timer = setTimeout(() => {
                        timer = null;
                        fn(...args);   
                    }, wait);
                    if (canRun) fn(...args);
                } else {
                    timer = setTimeout(() => {
                        fn(...args);
                    }, wait)
                }

            }
            debounded.cancel = () => {
                clearTimeout(timer);
                timer = null;
            }

            return debounded;
        }
    ```
    