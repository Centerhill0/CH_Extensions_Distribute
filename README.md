# CH_Extensions_Distribute

Blender 扩展分发仓库（自托管远程扩展仓库），托管 index.json 与扩展包，由插件开发项目的 `publish.py` 自动维护。

## 在 Blender 中添加

编辑 > 偏好设置 > 获取扩展 > 右上角 v 下拉菜单 > 仓库设置 > 添加远程仓库:

```
https://centerhill0.github.io/CH_Extensions_Distribute/index.json
```

## 维护流程

发布由插件开发项目完成: `python release.py --with_version` 构建扩展包到本仓库根目录,
`python publish.py` 重建索引并提交推送 (重建索引前自动按插件仅保留最新 3 个版本, 更早版本出库)。

## 手动收录 / 更新第三方扩展

把扩展 zip 拷入本仓库根目录 (文件名建议含版本号, 如 mcp_V1.0.3.zip), 然后在插件开发项目运行
`python publish.py` 即自动收进索引并提交推送。手动收录的包不参与"保留最新 3 版"裁剪;
老式 bl_info 插件包 (zip 内无 blender_manifest.toml) 无法收录; 换新文件名的 zip 重传即视为新版本。

说明:
- server-generate 只扫描根目录的 zip, 并全量重建 index.json (自动计算 archive_hash / archive_size, URL 为相对路径)
- index.json 中的 id + version 用于 Blender 端更新检测
- 本站经 GitHub Pages 发布 (main 分支 /root), Pages CDN 缓存约 10 分钟, 刷新未见新版本请稍等再试
