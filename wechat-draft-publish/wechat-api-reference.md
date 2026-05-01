# 微信公众号 API 完整参考

## 基础接口

### 获取 Access Token
- **URL**: `GET https://api.weixin.qq.com/cgi-bin/token`
- **参数**: `grant_type=client_credential`, `appid=APPID`, `secret=APPSECRET`
- **返回**: `{"access_token": "xxx", "expires_in": 7200}`
- **限制**: 每日获取上限2000次，Token有效期7200秒

---

## 素材管理

### 上传图文消息内图片
- **URL**: `POST https://api.weixin.qq.com/cgi-bin/media/uploadimg`
- **参数**: `access_token`, form-data `media` (图片文件)
- **限制**: jpg/png格式，1MB以下
- **返回**: `{"url": "http://mmbiz.qpic.cn/..."}`
- **注意**: 此接口上传的图片不占用5000个素材库限额；返回的URL仅可在微信域名内使用

### 新增永久素材（封面图）
- **URL**: `POST https://api.weixin.qq.com/cgi-bin/material/add_material`
- **参数**: `access_token`, `type=image`, form-data `media` (图片文件)
- **限制**: bmp/png/jpeg/jpg/gif，2MB以下
- **返回**: `{"media_id": "xxx", "url": "http://..."}`
- **注意**: 永久素材上限5000个

---

## 草稿管理

### 新增草稿
- **URL**: `POST https://api.weixin.qq.com/cgi-bin/draft/add`
- **参数**: `access_token`
- **请求体**:
```json
{
  "articles": [{
    "article_type": "news",
    "title": "标题",
    "author": "作者",
    "digest": "摘要",
    "content": "正文HTML",
    "content_source_url": "原文链接",
    "thumb_media_id": "封面图永久素材ID",
    "need_open_comment": 0,
    "only_fans_can_comment": 0,
    "show_cover_pic": 1
  }]
}
```
- **返回**: `{"media_id": "草稿media_id"}`
- **注意**: content 必须 < 2万字符、< 1MB，会去除JS；图片URL必须来自uploadimg接口

### 获取草稿列表
- **URL**: `POST https://api.weixin.qq.com/cgi-bin/draft/batchget`
- **请求体**: `{"offset": 0, "count": 20, "no_content": 1}`

### 获取草稿详情
- **URL**: `POST https://api.weixin.qq.com/cgi-bin/draft/get`
- **请求体**: `{"media_id": "xxx"}`

### 更新草稿
- **URL**: `POST https://api.weixin.qq.com/cgi-bin/draft/update`
- **请求体**: `{"media_id": "xxx", "index": 0, "articles": {...}}`

### 删除草稿
- **URL**: `POST https://api.weixin.qq.com/cgi-bin/draft/delete`
- **请求体**: `{"media_id": "xxx"}`

### 获取草稿总数
- **URL**: `POST https://api.weixin.qq.com/cgi-bin/draft/count`

---

## 发布管理

### 发布草稿
- **URL**: `POST https://api.weixin.qq.com/cgi-bin/freepublish/submit`
- **请求体**: `{"media_id": "xxx"}`
- **返回**: `{"publish_id": "xxx"}`
- **注意**: 发布后草稿从草稿箱移除；发布需审核

### 查询发布状态
- **URL**: `POST https://api.weixin.qq.com/cgi-bin/freepublish/get`
- **请求体**: `{"publish_id": "xxx"}`

### 删除发布文章
- **URL**: `POST https://api.weixin.qq.com/cgi-bin/freepublish/delete`
- **请求体**: `{"article_id": "xxx"}`

---

## 完整发布流程

```
1. 获取 access_token
2. 上传正文图片 → uploadimg → 获取微信URL
3. 替换HTML中的图片URL
4. 上传封面图 → add_material → 获取 thumb_media_id
5. 创建草稿 → draft/add → 获取 media_id
6. (可选) 发布草稿 → freepublish/submit
7. (可选) 查询发布状态 → freepublish/get
```

## 常见错误码

| 错误码 | 说明 | 解决方案 |
|--------|------|----------|
| -1 | 系统繁忙 | 稍后重试 |
| 40001 | access_token无效/过期 | 重新获取token |
| 40007 | invalid media_id | 检查素材ID |
| 40009 | 图片尺寸/格式不对 | 检查图片规格 |
| 41001 | 缺少access_token | 传入token参数 |
| 42001 | access_token超时 | 重新获取 |
| 45009 | 接口调用超过限制 | 等待后重试 |
| 45064 | 创建草稿频率限制 | 每分钟限10次 |
| 48001 | api功能未授权 | 检查公众号类型和权限 |
| 50002 | 用户受限 | 检查账号状态 |

## 参考链接

- [草稿管理官方文档](https://developers.weixin.qq.com/doc/offiaccount/Draft_Box/Add_draft.html)
- [素材管理官方文档](https://developers.weixin.qq.com/doc/offiaccount/Asset_Management/New_temporary_materials.html)
- [发布能力官方文档](https://developers.weixin.qq.com/doc/offiaccount/Publish/Publish.html)
