---
title: "FILE222"
date: 2025-05-21
showTableOfContents: true
---
## FILE结构

#### _IO_jump_t

```C
struct _IO_jump_t {
    JUMP_FIELD(size_t, __dummy);         // 占位字段
    JUMP_FIELD(size_t, __dummy2);        // 占位字段
    JUMP_FIELD(_IO_finish_t, __finish);  // 关闭文件流时调用
    JUMP_FIELD(_IO_overflow_t, __overflow); // 缓冲区溢出时触发（如 `exit()` 调用）
    JUMP_FIELD(_IO_underflow_t, __underflow); // 缓冲区不足时读取数据
    JUMP_FIELD(_IO_underflow_t, __uflow);    // 读取单个字符的底层实现
    JUMP_FIELD(_IO_pbackfail_t, __pbackfail); // 回退字符处理
    JUMP_FIELD(_IO_xsputn_t, __xsputn);  // 批量写入数据（被 `fwrite` 调用）
    JUMP_FIELD(_IO_xsgetn_t, __xsgetn);  // 批量读取数据（被 `fread` 调用）
    JUMP_FIELD(_IO_seekoff_t, __seekoff); // 调整文件指针位置（`fseek` 依赖）
    JUMP_FIELD(_IO_seekpos_t, __seekpos); // 绝对位置调整
    JUMP_FIELD(_IO_setbuf_t, __setbuf);   // 设置缓冲区
    JUMP_FIELD(_IO_sync_t, __sync);       // 同步文件流状态
    JUMP_FIELD(_IO_doallocate_t, __doallocate); // 动态分配缓冲区
    JUMP_FIELD(_IO_read_t, __read);       // 底层读取函数
    JUMP_FIELD(_IO_write_t, __write);     // 底层写入函数
    JUMP_FIELD(_IO_seek_t, __seek);       // 底层定位函数
    JUMP_FIELD(_IO_close_t, __close);     // 关闭文件描述符
    JUMP_FIELD(_IO_stat_t, __stat);       // 获取文件状态
    JUMP_FIELD(_IO_showmanyc_t, __showmanyc); // 检查剩余可读数据
    JUMP_FIELD(_IO_imbue_t, __imbue);     // 区域设置相关
#if 0
    // 旧版未实现的字段（已弃用）
    get_column;  
    set_column;
#endif
};
```



