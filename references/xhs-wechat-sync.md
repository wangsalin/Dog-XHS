# 小绿书（微信公众号）发布规范

> 更新日期：2026-03-23

---

## 一、配置文件

位置：`C:\Users\Administrator\.openclaw\workspace\wechat-article.config.json`

```json
{
  "appid": "wx77109d7e269659de",
  "appsecret": "24ea9d25b9ebd9052599936f85092122",
  "author": "狗哥",
  "account_name": "狗哥的胡思乱想",
  "slogan": "创业 · AI · 那些没人告诉你的事"
}
```

---

## 二、发布流程

### 1. 准备内容
- 标题：不超过64字
- 正文：HTML格式
- 摘要：120字以内
- 封面图：推荐900x500

### 2. 封面图
- 使用小红书AI生成的封面图
- 尺寸：推荐1080x1440（3:4）
- 格式：PNG/JPG

### 3. 执行发布（必须是图片消息newspic！）

**小绿书 = 小红书排版**

微信公众号的"图片消息"（newspic）和小红书竖版图文排版完全一致！

```bash
python "C:\Users\Administrator\.openclaw\workspace\wechat-article-skill\publish_image_post.py"
```

脚本会自动：
1. 上传封面图到微信素材库
2. 创建图片消息草稿（newspic）
3. 封面图嵌入文章内容顶部

**⚠️ 关键点：**
- ✅ 使用 `article_type = "newspic"`（图片消息 = 小红书竖版排版）
- ❌ 禁止使用 `article_type = "news"`（图文模式 = 横版）

---

## 三、内容同步规则

### 同步原则
- 小红书发什么，小绿书就发什么
- 内容必须一致，只是格式转换

### 格式转换
- 小红书emoji → 保留
- 小红书话题 → 转为文内标签
- **换行 → 必须保留！** 每段结束加 `<br><br>` 实现换行
- 段落之间必须有换行，不能连在一起
- 配图 → 整合到HTML中

---

## 四、发布检查清单

### 发布前
- [ ] 确认内容与小红书一致
- [ ] 标题≤64字
- [ ] 摘要≤120字
- [ ] 封面图准备好

### 发布后
- [ ] 确认推送到草稿箱
- [ ] 记录到发布日志

---

## 五、账号信息

| 项目 | 内容 |
|------|------|
| 公众号 | 狗哥的胡思乱想 |
| AppID | wx77109d7e269659de |
| 作者 | 狗哥 |
| slogan | 创业 · AI · 那些没人告诉你的事 |

---

## 六、常用命令

### 发布到草稿箱
```bash
python publish_image_post.py --title "标题" --author "作者" --digest "摘要" --content-file "文件.html" --cover "封面.jpg"
```

### 生成封面
使用AI生成封面图，保持与小红书封面风格一致

---

*本规范需严格遵守*

---

## С�����Ű�淶�������棩

### �����Ű�

`html
<section style="max-width: 677px; margin: 0 auto; padding: 0 20px; color: #3f3f3f; font-size: 15px; line-height: 1.75;">
  <p style="margin: 1.5em 0;">��������</p>
</section>
`

### ���й���
- ���������</p>
- ����֮�䣺<p style="margin: 1.5em 0;">��һ��</p>
- ͬһ�����ڻ��У�<br />

### �ص�ǿ��
`html
<strong style="color: #3daad6;">�ص�����</strong>
`

### С����
`html
<p style="margin: 1.5em 0; font-size: 18px; font-weight: bold; color: #2e6e9e;">�½ڱ���</p>
`

### �ָ���
`html
<hr style="border: none; border-top: 1px solid #eee; margin: 2em 0;" />
`

### ��ɫ����
- ����ɫ��#2e6e9e��������
- ǿ��ɫ��#3daad6��ǳ����
- ����ɫ��#3f3f3f
- ע��ɫ��#a5a5a5

### ͬ��ʱ��ʽת��
1. С����emoji �� ����
2. С���黰�� �� תΪ���ڱ�ǩ
3. **���� �� ÿ���� <p> �������μ�� margin: 1.5em 0**
4. �ص��� <strong> ����
