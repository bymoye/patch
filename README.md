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
