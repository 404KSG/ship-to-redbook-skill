# 小红书内容发布

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
