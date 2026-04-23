

## 启动
默认端口 8787 ， profile 为 default
> python bootstrap_liuy.py
>
## 指定端口和profile用户
这样可以为不同的profile指定webUI
> python bootstrap_liuy.py 8788 --profile=coder

## 设置密码
C:\Users\PC\.hermes\.env 设置, 不同的profile需要不同的.env文件
```env
HERMES_WEBUI_PASSWORD=123456    # 访问密码（推荐设置）
```


## 接口原理

```markdown
客户端发起请求
    ↓
ThreadingHTTPServer 接收连接
    ↓
创建新的 Handler 实例（在新线程中）
    ↓
解析 HTTP 请求行和方法
    ↓
根据请求方法分发到对应的 do_* 方法
    ├── GET  → do_GET()   ← 自动调用
    ├── POST → do_POST()  ← 自动调用
    ├── PUT  → do_PUT()   （如果定义了）
    └── ...
    ↓
执行你的业务逻辑
    ↓
发送 HTTP 响应
    ↓
调用 log_request() 记录日志  ← 自动调用
   ↓
调用 log_message() 输出日志  ← 自动调用（如果被触发）
    ↓
请求结束，线程回收
```


