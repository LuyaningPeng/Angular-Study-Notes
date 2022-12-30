# 😁 Angular使用文件系统

#### angular使用文件系统

1.  使用`fs`，导入fs外部包正常，但无法使用其定义的函数，报错如下：

    ```javascript
    ERROR TypeError: fs__WEBPACK_IMPORTED_MODULE_0__.writeFileSync is not a function
        at LogService.test (log.service.ts:18:5)
        at HomeComponent.test (home.component.ts:70:21)
        at HomeComponent.ngOnInit (home.component.ts:37:10)
        at callHook (core.js:2538:1)
        at callHooks (core.js:2507:1)
        at executeInitAndCheckHooks (core.js:2458:1)
        at refreshView (core.js:9499:1)
        at refreshEmbeddedViews (core.js:10609:1)
        at refreshView (core.js:9508:1)
        at refreshComponent (core.js:10655:1)
    ```
2. 使用`fs-extra`，步骤
   * install --save --legacy-peer-deps
   *   angular.json

       ```json
       "allowedCommonJsDependencies": [
         "stream",
         "path",
         "constants"
         ]
       ```
   *   tsconfig.json

       ```json
       "paths": {
             "stream": [ "./node_modules/stream-browserify" ],
             "path": [ "./node_modules/path-browserify" ],
             "constants": ["./node_modules/constants-browserify"]
             }
       ```
   *   package.json

       ```json
         "browser": {
           "fs": false,
           "assert": false,
           "os": false,
           "util": false
         }
       ```
   *   导入fs-extra正常，进入不了页面，报错如下：

       ```javascript
       RROR Error: Uncaught (in promise): ReferenceError: process is not defined
       ReferenceError: process is not defined
           at 58937 (polyfills.js:3:1)
           at __webpack_require__ (bootstrap:19:1)
           at 15622 (graceful-fs.js:2:17)
           at __webpack_require__ (bootstrap:19:1)
           at 96566 (index.js:5:12)
           at __webpack_require__ (bootstrap:19:1)
           at 28857 (index.js:6:3)
           at __webpack_require__ (bootstrap:19:1)
           at 7943 (confirm-on-exit.guard.ts:38:21)
           at __webpack_require__ (bootstrap:19:1)
           at resolvePromise (zone.js:1213:1)
           at resolvePromise (zone.js:1167:1)
           at zone.js:1279:1
           at ZoneDelegate.invokeTask (zone.js:406:1)
           at Object.onInvokeTask (core.js:28679:1)
           at ZoneDelegate.invokeTask (zone.js:405:1)
           at Zone.runTask (zone.js:178:1)
           at drainMicroTaskQueue (zone.js:582:1)
       ```

#### 使用Chrome打印日志

`--enable-logging=stderr --v=1 --vmodule=metrics=2 > E:\ThingsBoard\log.txt 2>&1`

`--new-window http://43.140.204.118:9090/home --enable-logging --v=1 --vmodule=metrics=2 --log-file=C:\ThingsBoard\log.txt`

https://www.chromium.org/for-testers/enable-logging/

#### 使用Chorme浏览器

* 官方链接：https://www.chromium.org/for-testers/enable-logging/
* 命令：
  * `chrome.exe --new-window 网址 --enable-logging --v=1 --vmodule=metrics=2 --log-file=目标文件`
  * 例：`chrome.exe --new-window https://www.baidu.com --enable-logging --v=1 --vmodule=metrics=2 --log-file=E:\log.log`
* 注意：
  1. 目标文件请先在指定路径中创建好，上述命令不会自己创建文件
  2. 建议使用**管理员身份**运行上述命令
  3. chrome默认安装路径`C:\Program Files (x86)\Google\Chrome\Application`
*   实例：

    ![](E:%5CAngular%5Clearning%5C%E5%9B%BE%E7%89%87.png)
