# canyin-daily-auth

餐饮日报的登录鉴权服务（Deno Deploy 应用，入口 `main.ts`）。
源码的原始位置是 `canyin-daily/cloud/`，改动请在那边改完再跑
`python tools\publish_auth_service.py` 推过来。

接口：`/api/login`、`/api/session`、`/api/logout`、`/api/devices`、
`/api/devices/kick`、`/api/health`。

环境变量：`USERS_JSON`（必填，账号哈希）、`MAX_DEVICES`（默认 3，设备名额上限）、
`DEVICE_TTL_DAYS`、`SESSION_DAYS`、`ALLOW_ORIGIN`、`ADMIN_TOKEN`。

部署要点：App 的 Runtime 选 Dynamic，Entrypoint 填 `main.ts`，
并在 Databases 里给它挂一个 Deno KV 实例（代码用 `Deno.openKv()`）。
