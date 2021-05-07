# CJSON 源码阅读笔记

如果不懂 Makefile 可以先看看

-   [Make 命令教程](http://www.ruanyifeng.com/blog/2015/02/make.html)
-   [Makefile 由浅入深--教程、干货](https://zhuanlan.zhihu.com/p/47390641)

执行编译生成可执行文件

```zsh
make
make test
# 输出测试文本内容...
```

可以先从 test.c 入手查看它的一些基本使用方法

## cJSON.h

<details>
<summary>[x] cJSON Types 的`<<`操作是为什么？</summary>

```
这里利用了位掩码的特性，使用 增、删、比较 这些操作

React 源码中也有相同的使用
```

</details>

<details>
<summary>为什么宏`CJSON_PUBLIC`来定义其它的方法？例如：`cJSON_Version`、`cJSON_InitHooks`等</summary>

暂时理解为可以根据不同平台定义不同的`CJSON_PUBLIC`宏，后续有不同理解再加以修正
```C
#if (defined(__GNUC__) || defined(__SUNPRO_CC) || defined (__SUNPRO_C)) && defined(CJSON_API_VISIBILITY)
#define CJSON_PUBLIC(type)   __attribute__((visibility("default"))) type
#else
#define CJSON_PUBLIC(type) type
#endif

CJSON_PUBLIC(int) func_int(void); // 等同于下面
int func_int(void);
```

</details>

## cJSON.c

TODO: 
