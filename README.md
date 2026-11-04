# Poker Ledger V2.0

黑金德州战绩追踪，公开邮箱注册，Firebase Authentication + Cloud Firestore 按 UID 隔离。

## GitHub Pages
1. 将 `index.html`、`manifest.webmanifest`、`icon-180.png`、`icon-192.png`、`icon-512.png` 上传到仓库根目录（main 分支）。
2. 仓库 Settings → Pages → Build and deployment → Deploy from a branch → main → /(root) → Save。
3. 访问 https://cherryzhao19-png.github.io/Poker-ledger/ 。

## Firebase
使用 Firebase 项目 `poker-ledger-aadb1`：启用 Authentication → Email/Password，Cloud Firestore；在 Authentication → Settings → Authorized domains 添加 `cherryzhao19-png.github.io`。
确认 Firestore `firestore.rules` 与线上已发布规则相同。此文件只用于备份，不要上传到 GitHub Pages 作为必要资源。

## 数据与兼容性
- 本版仅从当前账号的 `users/{uid}/private/ledger` 读取数据，不能读取其他 UID 的记录。数据首次保存时自动生成。
- 旧版 JSON 需要登录后使用「恢复备份」主动导入；导入会**覆盖当前账号**已有记录，请提前导出备份。
- 同账号多设备可读取云端同步数据。每次写入使用 Firestore transaction + revision 比对，检测修改冲突而不静默覆盖。
- 需要联网才能确认写入成功；浏览器已有数据显示不意味着操作已同步。
- Firebase 免费额度、文档 1 MiB 大小限制及项目计费限制适用；长期高频使用建议迁移到每场独立文档，并配置后台备份。
- 账号权限由 Firestore Rules 保护；公开注册场景建议开启 Firebase App Check 或反滥用保护，监控配额。

## 验收
1. A 注册并新增一场，刷新页面、另一设备用 A 登录观察是否存在。
2. B 注册并登录，应显示 0 场；Firestore Rules Playground 以 B UID 尝试访问 A 路径应被拒绝。
3. A 编辑/删除/恢复牌局，确认历史与累计图自动更新。
4. 导出 JSON 后导入测试账号，确保字段兼容；不要在真实账号覆盖前跳过备份。
