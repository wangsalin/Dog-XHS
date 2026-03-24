# 小红书发布模块（整合版）

> 整合自 XiaohongshuSkills

---

## 一、发布方式

### 方式1：文字配图（推荐）

使用小红书内置"文字配图"功能：
1. 点击「文字配图」
2. 输入封面大字
3. 选择样式
4. 填标题+正文
5. 发布

**优点**：100%成功，自动化无障碍

### 方式2：外部图片发布

使用 XiaohongshuSkills 脚本：

```bash
# 图文发布
python scripts/cdp_publish.py publish-image \
  --title "标题" \
  --content "正文" \
  --images "图片路径1,图片路径2"

# 视频发布
python scripts/cdp_publish.py publish-video \
  --title "标题" \
  --content "正文" \
  --video "视频路径"
```

---

## 二、命令速查

### 启动浏览器
```bash
python scripts/chrome_launcher.py
```

### 检查登录
```bash
python scripts/cdp_publish.py check-login
```

### 发布图文
```bash
python scripts/cdp_publish.py publish-image \
  --title "标题" \
  --content "正文" \
  --images "图片1.png,图片2.png"
```

### 发布视频
```bash
python scripts/cdp_publish.py publish-video \
  --title "标题" \
  --content "正文" \
  --video "视频.mp4"
```

### 搜索笔记
```bash
python scripts/cdp_publish.py search-feeds --keyword "关键词"
```

### 评论互动
```bash
# 发表评论
python scripts/cdp_publish.py post-comment \
  --feed-id "笔记ID" \
  --content "评论内容"

# 回复评论
python scripts/cdp_publish.py respond-comment \
  --feed-id "笔记ID" \
  --comment-id "评论ID" \
  --content "回复内容"
```

---

## 三、注意事项

1. **图片路径**：使用绝对路径
2. **标题限制**：不超过38字
3. **图文必须有图**：小红书图文必须有图片
4. **视频图片二选一**：不能同时有图片和视频

---

## 四、故障处理

| 问题 | 解决方案 |
|------|----------|
| 上传图片失败 | 改用文字配图方式 |
| 未登录 | 执行 `python scripts/cdp_publish.py login` |
| 发布按钮点击失败 | 检查页面结构是否变化 |
| 浏览器异常 | 重启浏览器 `python scripts/chrome_launcher.py --restart` |

---

*本模块整合自 XiaohongshuSkills*
