1. 一个运行服务如何做到动态更新配置  
    goroutine监听配置系统如etcd/consule，如果有变化通知，则比较老的配置和新的配置，如果某一项配置发生变化则修改这一配置，但是不同goroutine去读写同一变量可能会有问题，解决这一问题方法很多比如使用mutex，但是mutex相对更耗时，可以使用atmoic包来实现，atmoic是使用cpu指令来实现的，效率更高
2. atomic可以对哪几种数据类型做操作  
    - int32  
    - int64
    - uint32
    - uint64
    - uintptr
    - unsafe.Pointer
3. 

