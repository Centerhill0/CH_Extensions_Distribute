# CH_Extensions_Distribute

Blender 扩展分发仓库（自托管远程扩展仓库），托管 index.json 与扩展包，由插件开发项目的 `publish.py` 自动维护。

## 在 Blender 中添加

编辑 > 偏好设置 > 获取扩展 > 右上角 v 下拉菜单 > 仓库设置 > 添加远程仓库:

```
https://centerhill0.github.io/CH_Extensions_Distribute/index.json
```

## 维护流程

发布由插件开发项目完成: `python release.py --with_version` 构建扩展包到本仓库根目录,
`python publish.py` 自动把**同一插件的旧版包移入 `archive/`**（根目录只留最新版）、重建索引并提交推送。
多插件同批发布时, 每个插件各跑一次上述两条命令（分发提交信息才逐条准确）。

## 手动收录 / 更新第三方扩展

把扩展 zip 拷入本仓库根目录 (文件名建议含版本号, 如 mcp_V1.0.3.zip), 然后在插件开发项目运行
`python publish.py` 即自动收进索引并提交推送。手动收录的包**不参与自动归档**, 需自行管理新旧版本;
老式 bl_info 插件包 (zip 内无 blender_manifest.toml) 无法收录; 换新文件名的 zip 重传即视为新版本。

说明:
- server-generate 只扫描根目录的 zip, 并全量重建 index.json (自动计算 archive_hash / archive_size, URL 为相对路径)
- `archive/` 存放被新版取代的发行包: 因只扫根目录, 归档包**不进索引**（Blender 端看不到旧版），但仍随 git 保留为历史备份
- index.json 中的 id + version 用于 Blender 端更新检测
- 本站经 GitHub Pages 发布 (main 分支 /root), Pages CDN 缓存约 10 分钟, 刷新未见新版本请稍等再试
