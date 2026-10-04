# CH_Extensions_Distribute

Blender 扩展分发仓库（自托管远程扩展仓库），托管 index.json 与各版本扩展包。

## 在 Blender 中添加

编辑 > 偏好设置 > 获取扩展 > 右上角 v 下拉菜单 > 仓库设置 > 添加远程仓库:

```
https://raw.githubusercontent.com/Centerhill0/CH_Extensions_Distribute/main/index.json
```

## 维护流程

发版: 把扩展 zip 拷入本仓库根目录 (与 index.json 平级), 然后重建索引并推送:

```bash
blender --command extension server-generate --repo-dir=<本仓库本地目录>
git add -A && git commit -m "release: <插件名> <版本>" && git push
```

说明:
- server-generate 只扫描根目录的 zip, 并全量重建 index.json (自动计算 archive_hash / archive_size, URL 为相对路径)
- index.json 中的 id + version 用于 Blender 端更新检测
