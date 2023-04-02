CEF4Delphi学习笔记

TChromium 运行是多进程多线程方式,所以很多事件都是异步线程事件,设及到VCLUI操作,就需要一种同步手段,这可以通过windows消息循环系统来实现. 这也是编码复杂麻烦的原因所在.



TChromium 启动过程:



TForm.WMMove

```
TForm.WMMove
  先于FormCreate执行,
  inherited;
  //去除了没发现有什么影响
  if Chromium1 <> nil then
    Chromium1.NotifyMoveOrResizeStarted;
TForm.FormCreate
TForm.FormShow
	if not Chromium1.CreateBrowser(CEFWindowParent1) then
		timer1.Enabled := True; 
	创建绑定到CEFWindowParent1的Browser,如何失败,延迟300ms在事件中重试.直到成功.
TForm.WMMove
TForm.Chromium1AfterCreated 线程中
  现在browser已完全创建,异步消息让主线程执行后续操作
  PostMessage(Handle, CEF_AFTERCREATED,0,0);
TForm.CEF_AFTERCREATED 消息
  没干啥事.
TForm.Chromium1BeforePopup 线程中
   因点击了页面链接等而请求弹出新URL
TForm.WMMoving
   用户移动了窗口
TForm.WMMove
TForm.FormCloseQuery
   取消关闭,进入关闭中状态,并调用CloseBrowser
   CanClose := FCanClose;
  if not FClosing then
  begin
    FClosing := True;
    Chromium1.CloseBrowser(True);
  end;
TForm.Chromium1Close 线程中
	延迟关闭,发消息让主线程处理关闭事件
	PostMessage(Handle, CEF_DESTROY,0,0);
  	aAction := cbaDelay;
TForm.CEF_DESTROY 消息
    注销了VCL组件
	CEFWindowParent1.Free;
TForm.Chromium1BeforeClose 线程中
	Chromium正在关闭,设置窗口关闭状态,并重发关闭消息
	FCanClose := true;
  PostMessage(Handle, WM_CLOSE,0,0);
TForm.FormCloseQuery
   关闭窗口
   
   
总结就是异步线程事件+消息实现主线程处理方式(主要是设及到VCL UI操作)导致了代码大量增加.
```

