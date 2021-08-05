# 主题_config.yml的配置经验

## 图片

注意开启fancybox和lazyload，否则md文件里直接使用img标签的图片的src会被编译为data-src而导致图片无法被加载（因为data-src本身就是给lazyload使用的）

## 访问统计

``` yml
leancloud_visitors:
  enable: true
  app_id: L42TjYBjoxTIM133nxUznGuU-gzGzoHsz
  app_key: YS6nx260Yiwze7JUMUaBIEhy
  # Required for apps from CN region
  server_url: https://l42tjybj.lc-cn-n1-shared.com
```

server_url为升级到Next 7.8的新增选项，和leancloud官方的要求匹配

文章页面内的访问统计失效问题：

在`themes\next\layout\_third-party\statistics\lean-analytics.swig`里

``` js
if (CONFIG.hostname !== location.hostname) return; // line 80
```

这行代码对博客config设置的网址和当前的hostname进行比较，可以理解这是为了避免在本地调试时也触发counter。但这也导致了部署到远程后如果使用了第三方域名，比如我的博客本身URL为：GloveLover.github.io 但通过第三方域名转接到longglovelover.com，这也会导致counter不启动，所以需要注释掉这行代码。
