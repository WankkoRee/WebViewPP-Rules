# EnableWebViewDebugging-Rules [启用 WebView 调试的规则库]

## 如何提交

1. `fork` 本仓库
2. 如果是本规则库未收录的app，请在`rules`目录下新建**以"app包名"命名**的文件夹，否则直接进入第3步
3. 如果是本规则库未收录的app版本，请在`rules`目录下**以"app包名"命名**的文件夹中新建**以"版本名(版本号).json"命名**的文件，否则直接进入第4步
4. 请打开`rules`目录下**以"app包名"命名**的文件夹中的**以"版本名(版本号).json"命名**的文件，以如下格式进行规则的编写，其中用`*`包裹的内容请自行替换
   ```json
   {
     "*在这填写内置 hook 方法名*": [
       {
         "name": "*在这里填写规则名*",
         "*在这里填写 hook 参数名*": "*在这里填写 hook 参数内容*",
         "*在这里填写 hook 参数名*": "*在这里填写 hook 参数内容*",
         "*在这里填写 hook 参数名*": "*在这里填写 hook 参数内容*",
         ...
       }, {
         "name": "*在这里填写规则名*",
         "*在这里填写 hook 参数名*": "*在这里填写 hook 参数内容*",
         "*在这里填写 hook 参数名*": "*在这里填写 hook 参数内容*",
         "*在这里填写 hook 参数名*": "*在这里填写 hook 参数内容*",
         ...
       }, {
         "name": "*在这里填写规则名*",
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
     "Class_WebView": "android.webkit.WebView",
     "Class_WebViewClient": "android.webkit.WebViewClient",
     "Method_onPageFinished": "onPageFinished",
     "Method_evaluateJavascript": "evaluateJavascript",
     "Class_ValueCallback": "android.webkit.ValueCallback"
   }
   ```
3. `replaceNebulaUCSDK`
   ```json
   {
     "name": "标准 UC_U4 内核替换 Hook 点",
     "Class_UcServiceSetup": "com.alipay.mobile.nebulauc.impl.UcServiceSetup",
     "Method_updateUCVersionAndSdcardPath": "updateUCVersionAndSdcardPath",
     "Field_sInitUcFromSdcardPath": "sInitUcFromSdcardPath"
   }
   ```
其他内核 demo 可参考 [TBS X5](rules/cn.wankkoree.test.tbsx5)、[UC U4](rules/com.mpaas.demo) 。
