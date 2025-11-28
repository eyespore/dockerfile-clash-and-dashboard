# dockerfile-clash-and-dashboard

项目基于`laoyutang/clash-and-dashboard`镜像，提供以下三种包装层：

- ngx_stream_module（L4）
- ngx_http_proxy_connect_module（L7）
- stunnel（L4）

来实现对Clash的HTTP/Socks5代理端口进行TLS加密

# 如何运行

首先你得有一份Clash的配置文件，这里假设配置文件被正确导入项目根目录下，且名称为`config.yml`（如果文件名不同你需要修改compose.yml中的挂载配置）

项目对不同的TLS包装层文件进行了统一的命名，例如：

## 使用ngx_stream_module作TLS包装

你将需要以下文件：

- compose-stream.yml.sample
- Dockerfile-stream：基于laoyutang/clash-and-dashboard镜像，为其安装ngx_stream_module模块

## 使用ngx_http_proxy_connect_module作TLS包装

你将需要以下文件：

- compose-http-proxy-connect.yml.sample
- Dockerfile-http-proxy-connect：基于laoyutang/clash-and-dashboard镜像，参考ngx_http_proxy_conenct_module安装流程：通过Nginx官网获取Nginx安装包后，重新编译安装Nginx

## 使用stunnel作TLS包装

你将需要以下文件：

- compose-stunnel.yml.sample
- stunnel.conf.sample：stunnel配置文件

选择一种方案并进行配置，一旦配置完成，执行

```bash
docker compose up
```

来运行代理，如果配置正确，那么你应该能够通过`https://[USERNAME[:PASSWORD]]@HOST:PORT`来访问代理