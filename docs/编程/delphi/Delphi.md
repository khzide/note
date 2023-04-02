[TOC]



### DataSnap

* 在主从表结构中，主从表SchemaAdapte指向同一个TFDSchemaAdapter， 则以下结果相同：

主表.SaveToFile

从表.SaveToFile

FDSchemaAdapter.SaveToFile

* TSmclient.XXX(value:TStream) 执行时，内部受TSmclient.InstanceOwner的影响，如果instanceOwner=true,则value会被管理，外部只创建，不要释放。



服务器端TStream参数，必须要复制到另一个流中才可使用，可能是因为它是网络流，未收全时没有长度的原因。

主从表服务器端必须是Range（范围)类型，不能是where pid=:id这种。因为这种会因为主记录的移动刷新子数据，最终返回数据只有对应主数据一条的数据。



### SQLITE多线程:

非常重要的参考页面：

http://docwiki.embarcadero.com/RADStudio/Tokyo/en/Using_SQLite_with_FireDAC#SQLite_Transactions.2C_Locking.2C_Threads_and_Cursors

1	读取大型数据库。	将CacheSize设置为更多的页面数，这些页面将用于缓存DB数据。总缓存大小将为CacheSize * <db页面大小>。
2	数据库的独占更新。	考虑将JournalMode设置为**WAL**（更多）。
3	长时间更新交易。	将CacheSize设置为更多的页面数，这将使您可以运行具有许多更新的事务，而不会使脏页面的内存缓存过载。
4	一些并发更新过程。	将LockingMode设置为Normal以启用共享数据库访问。将“同步”设置为“Normal”或“Full”可以使提交的数据对其他人可见。将UpdateOptions.LockWait设置为True以启用等待锁定。增加BusyTimeout可以增加锁定等待时间。考虑将JournalMode设置为WAL。
5	一些并发更新线程。	参见（4）。还将SharedCache设置为False，以最大程度地减少锁定冲突。
6	一些并发更新事务。	参见（4）或（5）。还将TxOptions.Isolation设置为xiSnapshot或xiSerializible，以避免可能的事务死锁。
7	安全性高。	将“**Synchronous**”设置为“Full”可保护数据库免受已提交的数据丢失的影响。另请参阅（3）。考虑加密数据库以提供完整性。
8	高度保密。	加密数据库以提供机密性和完整性。
9	开发时间。	将LockingMode设置为Normal可在IDE和调试的程序中同时使用SQLite DB。

SQLite作为文件服务器DBMS，可在更新时锁定数据库表。以下设置影响并发访问：

- 当多个线程正在更新同一数据库时，请将**SharedCache**连接参数设置为False。这可以帮助您避免一些可能的死锁。
- 当多个进程或线程正在更新同一数据库表时，请将**LockingMode**设置为Normal以启用对表的并发访问。还将“**Synchronous**”参数设置为“FULL”或“正常”。这样，SQLite在事务完成后立即更新数据库文件，并且其他连接可以按可预见的方式查看更新。
- 到连接之间避免锁定冲突，设置UpdateOptions.LockWait为True，并且**BusyTimeout**为更高的值。
- 为避免长时间运行的更新事务之间发生锁定冲突，请将TADConnection.TxOptions.Isolation设置为xiSnapshot或**xiSerializible**。

### 事务和隔离模式

SQLite支持普通[事务](http://docwiki.embarcadero.com/RADStudio/Tokyo/en/Managing_Transactions_(FireDAC))和嵌套事务（检查点）。它不支持多个事务。进一步列出了SQLite支持的隔离模式：

| **模式**         | **对应于**                                                   |
| ---------------- | ------------------------------------------------------------ |
| xiDirtyRead      | [PRAGMA read_uncommitted](http://www.sqlite.org/pragma.html#pragma_read_uncommitted) = 1 |
| xiReadCommitted  | [开始交易](http://www.sqlite.org/lang_transaction.html)      |
| xiRepeatableRead | 与xiReadCommitted相同。                                      |
| xiSnapshot       | 立即开始交易                                                 |
| 可串行化         | 独家交易开始                                                 |

DLL共享数据库连接:

DLLConnection.SharedCliHandle = MainAPPConnection.CliHandle.  共享后DLLConnection中的所有设置无效，或者不需要。

应用程序连接不跟踪 DLL 中执行的状态更改。因此不要在DLL中操作事务及其它设置。

DLL连接不适合长时间连接。并且事务应在主程序中运行。如下：

```
procedure TForm1.Button1Click(Sender: TObject);
type
  TSomeTaskProc = procedure (ACliHandle: Pointer); stdcall;
var
  hDll: THandle;
  pSomeTask: TSomeTaskProc;
begin
  hDll := LoadLibrary(PChar('Project2.dll'));
  try
    @pSomeTask := GetProcAddress(hDll, PChar('SomeTask'));
    FDConnection1.StartTransaction;
    try
      pSomeTask(FDConnection1.CliHandle);
      FDConnection1.Commit;
    except
      FDConnection1.Rollback;
      raise;
    end;
  finally
    FreeLibrary(hDll);
  end;
end;
```

应用程序可能会在卸载包含 FireDAC 的 DLL 时挂起。这种情况的标准症状是应用程序挂断了 FreeLibrary 调用。这是 FireDAC 的限制，它有两种解决方法：

- 1.在 DLL 中启用 FireDAC 静默模式，以便 FireDAC 不显示等待游标、对话框等。为此，请放入您的 DLL DPR 文件：

```
uses
  FireDAC.UI.Intf;

begin
  FFDGUIxSilentMode := True;
end.
```

* 卸载DLL前执行：

  

  ```
  uses
    FireDAC.Stan.Factory;
  
  procedure Shutdown;
  begin
    FDTerminate;
  end;
  
  exports
    Shutdown;
  ```



### TFDLocalSQL

UseTransactions －〉设置为true时，提交数据时，conn会自动进入事务状态，并不自动提交事务。还需要执行  if conn.InTransaction then    conn.Commit; 不然其它连接看不到数据修改。

mutipleCursors->true, 不然提交修改时，会改变原数据表中显示的记录数。原本只会显示修改后的结果。

如果原表开启了缓存更新，则提交后原表进入updatepending状态。





