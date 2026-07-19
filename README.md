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

### 智能服务：开屏广告

- 包名：`com.miui.systemAdSolution`
- 选择器：

```text
[vid="view_skip_button"][text^="跳过广告"][clickable=true][visibleToUser=true]
```

该规则已完成实机验证：GKD 能够自动命中并点击右上角的跳过按钮。

### 淘宝：关闭购物红包弹窗

- 包名：`com.taobao.taobao`
- Activity：`com.taobao.themis.container.app.TMSActivity`
- 上下文选择器：

```text
TextView[text*="购物红包"][visibleToUser=true]
```

- 点击目标：

```text
Button[text="关闭"][clickable=true][visibleToUser=true]
```

完整规则使用 `matches` 数组：只有“购物红包”标题和可点击的“关闭”按钮同时存在时，才点击最后一个选择器对应的关闭按钮。

该规则已经完成以下验证：

- 两个选择器均能在手机当前实时界面查询成功；
- 完整规则能够将 `Button：关闭` 选为最终操作节点。

### 淘宝：签到并领取元宝

该规则按顺序执行两步：

1. 点击“立即签到”；
2. 在第一步执行后，点击“+任意数量元宝，点击领取”。

第一步选择器：

```text
Button[text="立即签到"][clickable=true][visibleToUser=true]
```

第二步选择器：

```text
Button[text$="元宝，点击领取"][clickable=true][visibleToUser=true]
```

第二步通过 `preKeys: [10]` 要求第一步刚刚执行过，避免脱离上下文单独点击领取按钮。两个页面状态的选择器均已在对应静态快照中成功命中正确按钮；完整自动点击链路尚待下一次签到机会实机验证。

## 在 GKD 中添加

1. 打开 GKD 的“订阅”页面。
2. 点击右下角的 `+`。
3. 粘贴 Raw GitHub 或 jsDelivr 订阅地址。
4. 添加后启用所需规则组。

## 更新规则

修改规则时，需要同时递增以下两个文件中的 `version`：

- `gkd.json5`
- `gkd.version.json5`

订阅的 `id` 应保持不变。
