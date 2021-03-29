## Patches

### nginx.patch
* Add HTTP3(QUIC) Support.
* Add HTTP2 HPACK Encoding Support.
* Add Dynamic TLS Record support.

  For BoringSSL support OCSP stapling.

  Thanks [@kn007](https://github.com/kn007/patch/)

Test pass: 1.19.8

After version 1.19.7, the kn007 patch and the patch provided by quiche are no longer valid,  cause post_accept_timeout had been removed by Nginx.
But after checking the relevant commit, I found a way to fix it.

 `post_accept_timeout` 
 
 can use 
 
 ```
 cscf = ngx_http_get_module_srv_conf(hc->conf_ctx,ngx_http_core_module);
  ngx_add_timer(rev, cscf->client_header_timeout); 
```

Replace.

—————————————————————————————————————————————————
### nginx.patch
* 添加HTTP3(QUIC)支持 (quiche实现)
* 添加HTTP2 HPACK编码支持
* 添加动态TLS记录支持
* 给Boringssl添上OCSP装订
  感谢[@kn007](https://github.com/kn007/patch/)提供的补丁

测试通过版本为 Nginx 1.19.8 
在Nginx 1.19.7 版本之后 `post_accept_timeout` 就被移除了 查看Nginx的[commit](https://github.com/nginx/nginx/commit/2ec8fac2d6b8e5023c9894d10bc50d78e63f242c)之后发现了一个替代的方法
如上英文版所言
