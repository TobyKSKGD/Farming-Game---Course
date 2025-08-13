# Farming-Game---Course
Udemy 的课程 Learn To Create A Farming Game With Unity 6 &amp; C# 的笔记。

课程地址如下：[Learn To Create A Farming Game With Unity 6 & C# | Udemy](https://www.udemy.com/course/unity6-farming/?couponCode=MT130825G1)

## Section 1: Introduction

本次课程的所有素材可以在仓库的 `./Resources/UdemyFarmingAssets-JamesDoyle.unitypackage` 中找到，请在开始前导入到 Unity 当中，直接将文件拖入 Unity 的素材库即可。

## Section 2: Getting Started

### Setting Up The Project

本项目在 Unity 6 中进行，国内可能需要用魔法在外网官网手动下载安装。

首先删除本项目中无需用到的包，点击左上角菜单栏 Windows -> Package Manager，Remove 删除以下包：`Visual Scripting`、`Timeline`、`Multiplayer Center`、`JetBrains Rider Editor`、`Test Framework`。

然后将 Unity 的工作视图调整为下面这样即可开始咯：

![](./Pictures/View.png)

## Section 3: Tiles & Tilemaps

### Creating Tiles

首先要做的第一件事就是开始设置要使用的场景。左上角菜单栏：File -> New Scene -> Lit 2D(URP)，然后在 Hierachy 中删除不需要的灯光 Global Light 2D。接着 Ctrl + S 保存在 Assets > Scenes 并给场景命名为 `Main`。

这里将使用瓦片 Tile Map 地图系统来布局我们的游戏场景，使场景统一。在素材库中进入导入的资源，然后进入以下路径：Art > Tiny Wonder Farm > Tilemaps，展开 summer farm tilemap 资源可以看到很多的素材。点击左上角菜单栏 Windows -> 2D -> Tile Palette，可以将此栏拖放到检查器旁边，首先点击 Create New Tile Palette 新建一个图块调色板，将其命名为 `Outdoor Ground`，并放在 Assets > Tiles > Outdoor Ground 文件下（自行新建一个 `Tiles` 和 `Outdoor Ground` 文件夹）。Tile Palette 中 Drag Tile, Sprite, Texture... 提示我们将素材拖入，我们将 summer farm tilemap 资源折叠然后整个拖入，将其保存在 Assets > Tiles > Outdoor Ground。为了更好的预览，可以将这个界面的下边界往下拖以放大界面。现在我们基本上已经拥有了想要的所有的瓦片。
