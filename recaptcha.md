# reCAPTCHA v3

为了减少 SPAM 和其它恶意评论，Pomment 支持使用 [reCAPTCHA v3](https://developers.google.com/recaptcha/docs/v3) 对访客的评论进行验证。如果验证不通过，那么对应的评论会被隐藏。不过，如果通过管理员通道回复这些评论，它们会被自动恢复显示。

## 启用

1. [申请开通 reCAPTCHA v3](https://g.co/recaptcha/v3)
2. 将获得的密钥（Secret Key）填入配置文件中的 `reCAPTCHA/secretKey`，并将 `reCAPTCHA/enabled` 设置为 `true`。
3. 如果你使用的是 Pomment 官方前端，直接引用 [官方 JavaScript 代码](https://developers.google.com/recaptcha/docs/v3)，并将获得的网站密钥（Site Key）填入挂件选项中即可：

```html
<script src="https://www.recaptcha.net/recaptcha/api.js?render=【你的 reCAPTCHA v3 Site Key】"></script>
<script>
    var widget = new PommentWidget({
        // ...
        reCAPTCHA: '你的 reCAPTCHA v3 Site Key 在这里',
    });
</script>
```

然后就大功告成了。

如果使用自定义客户端，则需要确保客户端在请求 `/v3/submit` 时能够提交正确的 `responseKey` 值。

## reCAPTCHA v3 在中国大陆不可用？

Pomment 默认使用 `www.recaptcha.net` 而非 `www.google.com` 作为 reCAPTCHA 服务器地址，而前者是可以在中国大陆正常使用的。
