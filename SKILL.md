---
name: ship-to-redbook-skill
description: 小红书（Xiaohongshu/Little Red Book/Redbook）发布主入口。自动发布内容到小红书，支持自动判断发布方式、图片处理、标题规则校验、无头模式和有窗口模式。替代 `xiaohongshu-publisher` 和 `social-post` 的小红书发布路径；只有旧命令显式调用时才使用那些兼容 skill。
---

# 小红书内容发布

这是当前小红书发布的 canonical skill。`xiaohongshu-publisher` 和 `social-post xiaohongshu` 仅作为旧入口/底层兼容，不参与新任务路由。

根据用户输入自动判断发布方式，简化发布流程。

## 工作流程

- 用户提供完整内容 + 图片/图片URL → 直接进入发布流程
- 用户提供网页 URL → WebFetch 提取内容和图片 → 适当总结 → 发布流程

## 发布命令

### 无头模式（推荐）

```bash
python scripts/publish_pipeline.py --headless \
    --title-file title.txt \
    --content-file content.txt \
    --image-urls "URL1" "URL2"
```

### 有窗口模式

```bash
python scripts/publish_pipeline.py \
    --title-file title.txt \
    --content-file content.txt \
    --image-urls "URL1" "URL2"
```

## 标题规则

标题长度 ≤ 38，计算规则：
- 中文字符和中文标点：每个计 2
- 英文字母/数字/空格/ASCII标点：每个计 1

## 注意事项

- 发布前必须让用户确认内容
- 小红书发布必须有图片
- 如需登录，脚本会自动切换到有窗口模式

## ⚠️ 重要提示

### 草稿保存机制
**小红书的草稿保存在浏览器本地，不是服务器端！**
- ✅ 只能在脚本使用的 Chrome 浏览器中查看草稿
- ❌ 换浏览器或设备看不到草稿
- ❌ 清除浏览器数据会删除草稿
- 📝 最多保存 100 篇草稿

### 查看草稿的正确方式
1. 打开脚本使用的 Chrome 浏览器（profile: `~/Google/Chrome/XiaohongshuProfiles/default`）
2. 访问：https://creator.xiaohongshu.com/publish/publish
3. 点击页面上的"草稿箱"标签

### 避免多标签页问题
- 脚本会自动管理标签页
- 如果遇到问题，先关闭所有小红书标签页
- 重新运行脚本
