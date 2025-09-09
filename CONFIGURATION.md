# ArtTech MkDocs 项目配置摘要

## 项目概述

这是一个基于 MkDocs Material 的文档站点，支持 GitHub Pages 自动部署。

## VS Code Paste Image 插件配置

位置：`settings.json`

```json
{
    "pasteImage.path": "e:/MKDocs/ArtTech/docs/assets/images",
    "pasteImage.basePath": "e:/MKDocs/ArtTech/docs",
    "pasteImage.forceUnixStyleSeparator": true,
    "pasteImage.insertPattern": "![${imageFileName}](${imageFilePath})",
    "pasteImage.showFilePathConfirmInputBox": false,
    "pasteImage.defaultName": "Y-MM-DD-HH-mm-ss"
}
```

## 功能特点

1. **本地图片存储**：所有图片保存在 `docs/assets/images/` 目录
2. **自动路径生成**：根据文件位置自动生成正确的相对路径
3. **时间戳命名**：图片按时间戳命名，避免冲突
4. **GitHub Pages 部署**：通过 GitHub Actions 自动部署

## 使用方法

1. 在任意 Markdown 文件中按 `Ctrl+Alt+V` 粘贴图片
2. 图片会自动保存到 `docs/assets/images/` 目录
3. 自动生成正确的相对路径引用

## 路径规则

- 根目录文件 (`docs/test.md`)：`![image](assets/images/file.png)`
- 子目录文件 (`docs/Unity/入门.md`)：`![image](../assets/images/file.png)`
- 深层目录：根据层级自动调整 `../` 的数量

## 部署配置

- **本地验证**：使用 `mkdocs serve` 命令在本地预览文档
- **GitHub Actions**：`.github/workflows/ci.yml`
- **构建排除**：`.gitignore` 排除 `site/` 目录
- **自动部署**：推送到 main/master 分支时自动部署

## 目录结构

``` plain text
docs/
├── assets/
│   ├── images/          # 图片资源
│   └── logo.jpg         # 站点图标
├── Unity/               # Unity 相关文档
├── UE/                  # UE 相关文档
├── 社团介绍/            # 社团介绍
├── 编程基础/            # 编程基础
├── 项目信息/            # 项目信息
└── index.md             # 首页
```

## 配置验证

✅ VS Code 设置已配置
✅ 图片路径修复完成
✅ .gitignore 文件已设置
✅ GitHub Actions 工作流已配置
✅ MkDocs 配置文件正确
✅ 图片资源文件夹创建完成

## 下一步操作

1. 重启 VS Code 以应用新的 Paste Image 配置
2. 在不同深度的文件夹中测试图片粘贴功能
3. 推送到 GitHub 验证自动部署功能

paste-image配置如下

``` json
{
    "pasteImage.path": "${projectRoot}/docs/assets/images",
    "pasteImage.basePath": "${currentFileDir}",
    "pasteImage.forceUnixStyleSeparator": true,
    "pasteImage.insertPattern": "![${imageFileName}](${imageFilePath})",
    "pasteImage.showFilePathConfirmInputBox": false,
    "pasteImage.defaultName": "Y-MM-DD-HH-mm-ss"
}
```
