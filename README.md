# GKD 自用订阅

这个仓库用于托管个人使用的 GKD 订阅。

## 订阅地址

Raw GitHub：

```text
https://raw.githubusercontent.com/shockbladenull/gkd-subscription/main/gkd.json5
```

jsDelivr：

```text
https://fastly.jsdelivr.net/gh/shockbladenull/gkd-subscription@main/gkd.json5
```

## 当前规则

### 智能服务

- 包名：`com.miui.systemAdSolution`
- 规则组：`开屏广告`
- 选择器：

```text
[vid="view_skip_button"][text^="跳过广告"][clickable=true][visibleToUser=true]
```

该选择器已经在静态快照中唯一命中右上角的“跳过广告”节点，并已完成实机验证：GKD 能够自动触发并点击目标节点。

规则使用 `matchRoot: true`，并将匹配时间限制为进入应用后的 10 秒；每次进入应用最多执行一次。

## 在 GKD 中添加

1. 打开 GKD 的“订阅”页面。
2. 点击右下角的 `+`。
3. 粘贴 Raw GitHub 或 jsDelivr 订阅地址。
4. 添加后确认“智能服务 → 开屏广告”已启用。

## 更新规则

修改规则时，需要同时递增以下两个文件中的 `version`：

- `gkd.json5`
- `gkd.version.json5`

订阅的 `id` 应保持不变。
