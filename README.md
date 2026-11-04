# Poker Ledger V2.1 — Preview

奶油白卡通 UI，五栏导航：首页 / 牌局 / 趋势 / 分析 / 我的。新增线上 Online / 线下 Live 分类、历史未分类、筛选与统计。

## 数据兼容性

继续使用 V2.0 的 Firebase 项目 `poker-ledger-aadb1`、Authentication 和 Firestore 文档路径 `users/{uid}/private/ledger`。原 `records`、`trash`、`revision` 字段保留；每条新记录新增可选 `playMode`。历史数据无 `playMode` 时显示“未分类”。不需要迁移或清空数据库。

## 本地预览与上线

不要直接用本地 file:// 打开测试 Firebase。可使用本地 HTTP 服务只检查 UI，但完整的邮箱登录需要 Firebase Authentication 授权域名。建议在 GitHub 独立预览仓库中部署进行真实测试；向 Firebase 添加对应的 GitHub Pages 域名（若尚未授权）。

正式替换前，请在当前 V2.0 网站“我的/备份数据”里导出 JSON 备份。先用测试账号检查线上/线下筛选、编辑、删除、回收站、跨账号权限。验证通过再上传新文件至原仓库 `main` 根目录。

项目本身没有自动修改线上 GitHub 仓库。
