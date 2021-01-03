#### 窗口显示关闭/最小化/全屏
设置window.styleMask = NSWindowStyleMaskTitled | NSWindowStyleMaskMiniaturizable | NSWindowStyleMaskClosable | NSWindowStyleMaskResizable; 需要什么自行添加, 要显示titleBar必须设置NSWindowStyleMaskTitled, 否则无法展示;

#### 显示窗口
window.makeKeyAndOrderFront(nil) 显示, 类似xib里面的visible at launch


#### 关闭窗口
window.close()  如果崩溃, window需要被强持有, 并且关闭从屏幕移除window.orderOut(nil)

#### 关闭窗口需要再次展示
window.close()之后再次展示, 需设置window.releasedWhenClosed = false;  否则关闭窗口后window被释放掉, 即使是被强持有的window也不行

#### MacOS ATS的问题, 访问HTTP失败
info.plist设置NSAllowsArbitraryLoads = true, 然后clean工程, 并重启xcode.  和iOS不同, 应该是MacOS上的Bug

### writeFoFile: atomically:
关于atomically的问题, NO直接覆盖写入, YES保证发生意外时有中转文件来保存信息, 知道写入完成(损耗大, 慢).   遇到直接的问题是, 当往机械硬盘里面写入时, 如果用YES, 那么执行完写入并马上往下执行时, 最终的操作结果有误. 比如我写入info.plist之后马上进行zip操作, 这个时候得到zip里面的info.plist是有问题的

### 关于plist文本
plist文本有两种格式, xml/binary plist,  bplist格式可用sublime之类的查看, 头部为bplist, 而xml则是<?xml开头

转换方式如下:  
Converting a plist File to XML from Binary
plutil -convert xml1 ExampleBinary.plist

Converting a plist Binary File to XML Format
plutil -convert binary1 Example.plist



