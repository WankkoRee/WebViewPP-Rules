# EnableWebViewDebugging-Rules [启用 WebView 调试的规则库]

## 如何提交

1. `fork` 本仓库
2. 如果是本规则库已收录的app，请直接进入第3步，否则：
   - 新建`rules/{包名}`文件夹
   - 新建`rules/{包名}/metadata.json`文件，内容参考其他已有规则
   - 修改`rules/rules.json`文件，添加`{包名}`
3. 如果是本规则库已收录的app版本，请直接进入第4步，否则：
   - 新建`rules/{包名}/{版本名}({版本号}).json`文件
   - 修改`rules/{包名}/metadata.json`文件，在`versions`节点添加`{版本名}({版本号})`
4. 修改`rules/{包名}/{版本名}({版本号}).json`，以如下格式进行规则的编写，其中用`*`包裹的内容请自行替换
   ```json
   {
     "*在这填写内置 hook 方法名*": [
       {
         "name": "*在这里填写规则名*",
         "version": *在这里填写规则版本号，格式为正整数，用于检查规则是否有更新*,
         "remark": "*在这里填写规则的相关备注*",
         "require": *在这里填写规则需要的最低模块版本号，格式为正整数*,
         "*在这里填写 hook 参数名*": "*在这里填写 hook 参数内容*",
         "*在这里填写 hook 参数名*": "*在这里填写 hook 参数内容*",
         "*在这里填写 hook 参数名*": "*在这里填写 hook 参数内容*",
         ...
       }, {
         "name": "*在这里填写规则名*",
         "version": *在这里填写规则版本号，格式为正整数，用于检查规则是否有更新*,
         "remark": "*在这里填写规则的相关备注*",
         "require": *在这里填写规则需要的最低模块版本号，格式为正整数*,
         "*在这里填写 hook 参数名*": "*在这里填写 hook 参数内容*",
         "*在这里填写 hook 参数名*": "*在这里填写 hook 参数内容*",
         "*在这里填写 hook 参数名*": "*在这里填写 hook 参数内容*",
         ...
       }, {
         "name": "*在这里填写规则名*",
         "version": *在这里填写规则版本号，格式为正整数，用于检查规则是否有更新*,
         "remark": "*在这里填写规则的相关备注*",
         "require": *在这里填写规则需要的最低模块版本号，格式为正整数*,
         "*在这里填写 hook 参数名*": "*在这里填写 hook 参数内容*",
         "*在这里填写 hook 参数名*": "*在这里填写 hook 参数内容*",
         "*在这里填写 hook 参数名*": "*在这里填写 hook 参数内容*",
         ...
       },
       ...
     ]
   }
   ```
5. 对修改进行`commit`
6. 对`commit`进行`push`和`pull requests`

## 内置 hook 方法及其标准 demo

1. `hookWebView`
   ```json
   {
     "name": "标准 WebView Hook 点",
     "version": 1,
     "remark": "",
     "require": 0,
     "Class_WebView": "android.webkit.WebView",
     "Method_getSettings": "getSettings",
     "Method_setWebContentsDebuggingEnabled": "setWebContentsDebuggingEnabled",
     "Method_setJavaScriptEnabled": "setJavaScriptEnabled",
     "Method_loadUrl": "loadUrl",
     "Method_setWebViewClient": "setWebViewClient"
   }
   ```
2. `hookWebViewClient`
   ```json
   {
     "name": "标准 WebView Client Hook 点",
     "version": 1,
     "remark": "",
     "require": 0,
     "Class_WebView": "android.webkit.WebView",
     "Class_WebViewClient": "android.webkit.WebViewClient",
     "Method_onPageStarted": "onPageStarted",
     "Method_onPageFinished": "onPageFinished",
     "Method_evaluateJavascript": "evaluateJavascript",
     "Class_ValueCallback": "android.webkit.ValueCallback"
   }
   ```
3. `replaceNebulaUCSDK`
   ```json
   {
     "name": "标准 UC_U4 内核替换 Hook 点",
     "version": 1,
     "remark": "",
     "require": 0,
     "Class_UcServiceSetup": "com.alipay.mobile.nebulauc.impl.UcServiceSetup",
     "Method_updateUCVersionAndSdcardPath": "updateUCVersionAndSdcardPath",
     "Field_sInitUcFromSdcardPath": "sInitUcFromSdcardPath"
   }
   ```
4. `hookCrossWalk`
   ```json
   {
     "name": "标准 CrossWalk Hook 点",
     "version": 1,
     "remark": "",
     "require": 0,
     "Class_XWalkView": "org.xwalk.core.XWalkView",
     "Method_getSettings": "getSettings",
     "Method_setJavaScriptEnabled": "setJavaScriptEnabled",
     "Method_loadUrl": "loadUrl",
     "Method_setResourceClient": "setResourceClient",
     "Class_XWalkPreferences": "org.xwalk.core.XWalkPreferences",
     "Method_setValue": "setValue"
   }
   ```
6. `hookXWebPreferences`
   ```json
   {
     "name": "标准 XWeb Preferences Hook 点",
     "version": 1,
     "remark": "",
     "require": 0,
     "Class_XWebPreferences": "org.xwalk.core.Preferences",
     "Method_setValue": "setValue"
   }
   ```
各内核 demo 可参考如下文件：
1. [WebView](rules/cn.wankkoree.test.webview)
2. [TBS X5](rules/cn.wankkoree.test.tbsx5)
3. [UC U4](rules/com.mpaas.demo)
4. [CrossWalk](rules/cn.wankkoree.test.crosswalk)

## 一些说明

- `Method_xxx`的参数值可以有两种格式：
  - 纯方法名，如`onPageFinished`
    - 此时类中所有的`onPageFinished`方法都会被 hook
  - 方法名+方法参数类型，如`onPageFinished(android.webkit.WebView,java.lang.String)`
    - 此时只有传参形如`(WebView, String)`的`onPageFinished`方法才会被 hook
    - 如果无参数，则写作`onPageFinished()`，表示只有传参形如`()`的`onPageFinished`方法才会被 hook
- 规则的参数不是必须的，未设定值的参数将使用模块中内置的默认值
  - 何为未设定：
    - `"Class": "123"`、`"Class": ""`，这都是已设定的情况
    - `"Class": null`、没写这个参数，这都是未设定的情况

## 一些使用条件

1. 如需开启远程调试，请确保以下条件满足其中之一:
   1. 对于 **WebView** 、 **TBS X5** ，至少有一个`hookWebView`规则生效。
   2. 对于 **UC U4** ，至少有一个`replaceNebulaUCSDK`规则生效，已开启`UC 调试内核`注入，且选择版本与目标页面所用的内核版本一致。
   3. 对于 **CrossWalk** ，至少有一个`hookCrossWalk`规则生效。
2. 如需注入`vConsole`，请确保以下条件满足所有：
   1. 至少有一个`hookWebViewClient`规则生效。
   2. 如果目标页面未开启`javascript 执行`功能，请确保 **#1 条件(远程调试)** 满足。
   3. 已开启`vConsole`注入，且选择版本支持目标页面所用的内核版本。
   4. 目标页面使用了`WebViewClient`接口。
