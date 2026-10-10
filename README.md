# 年鉴表生成 —— Bangumi 收藏年鉴 & 动画生涯喜好表

纯静态**单文件**网页：填入 Bangumi ID（用户名或数字 UID）即可生成收藏年鉴——
统计卡、月度/评分分布、标签云、按月封面墙、评分 TOP10、**动画生涯喜好表**，全部计算在浏览器本地完成，无需任何后端。

> 部署：把 `index.html` 丢进任意静态托管（Cloudflare Pages / GitHub Pages / Vercel…），甚至直接双击本地打开也能用。

## 功能

- **只需填 ID**：用户名或数字 UID 均可；URL 直达 `/index.html?uid=xxx&type=anime&year=all`，可分享
- **双数据源**：官方 `api.bgm.tv` 直连；或自填任意支持 `/v0` 透传 + CORS 的 **Bangumi 镜像根域**（本地记忆，国内网络友好）
  - 镜像同时是 [bgm-proxy](https://github.com/makabaka11/bangumi-proxy-workers) 类反代同域部署时，自动优先走 `/report/api` 聚合接口（一次请求全量 + 边缘缓存）
- **生涯喜好表**（[itorr/anime-grid](https://github.com/itorr/anime-grid) 玩法）：经典 15 格 / 扩展 60 格，列表内选片、按 Subject ID 查询、自定义文字，"按评分自动填"一键填充；**NSFW 不筛除**（bgm 图床原图对所有人开放）
- **导出**：一图全收录海报（上半封面拼贴 + 下半片名索引）、白底喜好表 PNG、JSON、Markdown（兼容 [Shell32-Natsu/bangumi_yearly_report](https://github.com/Shell32-Natsu/bangumi_yearly_report) 格式）、打印/PDF
- **嵌入其他 app**：iframe（`?uid=&type=&year=&source=&embed=1`）、postMessage 事件（`bgm-report-ready` / `bgm-report-error`）、同窗口 `BGMReport.load()` API
- **流畅**：封面 Cache Storage 持久缓存（强刷不重下，带一键清除按钮）、数据 localStorage 6 小时缓存、渐进渲染、懒加载

## 数据源说明

| 源 | 地址 | 适用 |
|---|---|---|
| 主站（官方） | `api.bgm.tv` 直连 | 官方 API 本身带 CORS，海外/可直连网络 |
| 镜像（自填） | 页面顶部"镜像根域"输入框 | 任意 Bangumi 镜像（要求 `/v0/*` 透传 + 响应带 CORS 头）；自部署反代同域时留空即可 |

统计口径：仅"已收藏"（v0 type=2），收藏时间取 `updated_at`；服务端无关，数据只在你的浏览器处理与缓存。

## 来源与致谢

| 来源 | 用途 |
|---|---|
| [itorr/anime-grid](https://github.com/itorr/anime-grid) | 生涯喜好表玩法与格子标签文案（原作禁止商业利用，本项目同为非商业用途） |
| [Shell32-Natsu/bangumi_yearly_report](https://github.com/Shell32-Natsu/bangumi_yearly_report) | 年鉴思路与 Markdown 导出格式 |
| [Bangumi 番组计划](https://bgm.tv/) | 全部条目/收藏数据来自官方 API，版权归 Bangumi 及条目贡献者所有 |

## License

[MIT](LICENSE) © TsangAsuna —— 转载/二改请保留页面与导出图中的来源署名。
