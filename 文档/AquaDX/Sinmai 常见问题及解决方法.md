# Sinmai 常见问题及解决方法

### 常见的黑屏问题

- 微星小飞机（AfterBurner）不能开（其他 OSD 也基本不行）
- SignalRGB 会占用 RGB 端口导致 Mai 出问题

### MelonLoader 报错

![[Pasted image 20250119060731.png]]

路径不能含有中文

### 自检卡在 Aime

游戏不能放在 E 盘，最好放在 C 或 D 盘
### 卡在自检完成的状态

![[Pasted image 20250119061244.png]]

去 Test -> Game Assignments 里面的第一项，设置基准机
### 画面变得很迷你，或者别的分辨率不对的情况

![[Pasted image 20250119060345.png]]

解决方法：

在 AquaMai 的 Window 下手动设置分辨率为屏幕的分辨率

```toml
## 窗口化 / 分辨率设置
[GameSystem.Window]
## 窗口化游戏
Windowed = false
## 宽度（和高度）窗口化时为游戏窗口大小，全屏时为渲染分辨率
## 如果设为 0，窗口化将记住用户设定的大小，全屏时将使用当前显示器分辨率
Width = 2160
## 高度，同上
Height = 3840
```

也可以使用 MaiChartManager 设置

![[Pasted image 20250119060856.png]]

