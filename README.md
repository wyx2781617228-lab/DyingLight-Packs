# Dying Light 1 · 成品包（DyingLight-Packs）

只放**成品二进制**的公开仓库，不含任何源码。源码在同账号的私有仓库 `DyingLight-Trainer` 里；
`Harran Link` 联机框架读本仓库根目录的 `pack.json`，按组件增量下载 `pack.json` 指向的 Release 资产。

## 组件

| 组件 | 安装位置 | 大小 | SHA-256 | 变化频率 |
|---|---|---|---|---|
| `trainer-dll` | `dsound.dll`（游戏根目录） | 2,836,480 | `2c1e5334b03cec1311e4caf6f37d026721283b03d68a17795a35f0b58208ea06` | 每次修改器改版 |
| `trainer-resources` | `DLTrainer/`（图标与退出辅助程序） | 9,619,988（解压 9,473,988 / 2,177 个文件） | `41d8fb3965ce97e383e8545c69c506e368fa604a246119b850972632121ab53b` | 极少变化 |

增量规则以**组件**为单位：本机已有副本的 SHA-256 与 `pack.json` 记录一致就完全不下载；只有变化的那个组件才拉取。
因此修改器改版时实际流量是 2.8 MB，而不是整包 12.3 MB；同一版本第二次安装是 0 字节。

## 校验

```powershell
Get-FileHash .\dsound-1.0.8.dll -Algorithm SHA256
```

哈希必须与上表和 `pack.json` 一致。安装前请先关闭游戏进程，安装后再核对一次。

## 已知边界

- `trainer-resources` 里的 `weapon_journal_exit_helper.exe`（286,720 字节 / `dca1e8eb…`）与图标集目前**只有二进制、没有源码**，来自 `DL-Trainer-Portable-127-20261031` 血脉；替换前必须先确认来源。
- 这些成品按 `gamedll_x64_rwdi.dll` 31,789,632 字节 / `a37265e5…` 这一份构建校验过；其他发行渠道的同版本构建需要另行核对，本仓库不声称跨渠道可用。
- 安装只覆盖清单内文件，不删除游戏目录里多出来的条目。
