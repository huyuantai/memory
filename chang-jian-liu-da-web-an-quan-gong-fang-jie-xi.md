https://segmentfault.com/a/1190000018073845

cxsf 跨站攻击， B网站诱导客户点击 请求A网站数据
1.验证 Referer 请求头来源
2.所有请求添加Token（时间戳+随机字符串）
3.Get 请求不对数据进行修改
4.不让第三方网站访问到用户 Cookie

