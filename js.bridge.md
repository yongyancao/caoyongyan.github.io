本文档仅用于充之鸟直流充电站的屏幕播报，原生Android与JS交互文档，本文档定义了原生程序为JS程序所提供的原生能力，主要表现为后台推送，语音合成，软件系统的参数设置.
 
#####系统能力

|方法|参数|返回值|描述
|:---|:--|:---|:---|
|shortToast|string msg|void|系统短时间弹出提示
|longToast|string msg|void|系统较长时间弹出提示
|getDeviceID|无|string|获取设备id
|getModel|无|string|获取设备型号
|getBrand|无|string|获取设备品牌
|getAppVersion|无|string|获取App版本
|getSystemVersion|无|string|获取Android系统版本


#####语音合成能力

|方法|参数|返回值|描述|
| --------   | -----:  | :----:  | :----:  |
|onReport|string content|void|播报指定内容
|onPauseReport|无|void|暂停语音播报
|onResumeReport|无|void|恢复或继续语音播报

#####原生回调能力(JS端定义的方法)

|方法|参数|返回值|描述|
|:---|:--|:---|:---|
|onJPushMessage|string msg|void|后台推送的消息，用于处理内部逻辑(原生提供消息解密)
|onSpeakProgress|int percent,int beginPos,int endPos|void|原生语音播报进度监听，参数1：百分比，参数2：开始值，参数3：结束值

#####原生生命周期(JS端定义的方法)

|方法|参数|返回值|描述|
|:---|:--|:---|:---|
|onResume|无|void|原生恢复回调
|onPause|无|void|原生暂停回调
|onDestroy|无|void|原生销毁回调

#####JS如何调用
JS通过原生定义的bridge字段来调用相关的方法，首先判断原生是否定义了该方法，再去调用对应的方法.
```
//调用的语法：window.bridge.方法名（参数列表...）;

//1.调用原生的语音播报
var report=function(){
  //获取要播报的内容
  var content='若流芳千古，爱的人却反目.';
  //判断是否存在名称为bridge的交互
  if(window.bridge){
    window.bridge.onReport(content);
  }
}
```
#####JS需要定义的方法
如果需要接收后台推送的消息，则需要定义指定的方法，当收到消息时原生会自动调用该方法.
```
//接收后台推送的消息
var onJPushMessage=function(msg){
   //处理相关的消息内容

}
```






