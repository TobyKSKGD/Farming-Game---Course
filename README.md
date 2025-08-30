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

首先要做的第一件事就是开始设置要使用的场景。左上角菜单栏：File -> New Scene -> Lit 2D(URP)，然后在 Hierachy 中删除不需要的灯光 Global Light 2D。接着 Ctrl + S 保存在 Assets > Scenes 并给场景命名为 `Main`。（这里如果刚开始有自带的场景 Simple Scene，也可以直接将其重命名为 Main 来使用）

这里将使用瓦片 Tile Map 地图系统来布局我们的游戏场景，使场景统一。在素材库中进入导入的资源，然后进入以下路径：Art > Tiny Wonder Farm > Tilemaps，展开 summer farm tilemap 资源可以看到很多的素材。点击左上角菜单栏 Windows -> 2D -> Tile Palette，可以将此栏拖放到检查器旁边，首先点击 Create New Tile Palette 新建一个图块调色板，将其命名为 `Outdoor Ground`，并放在 Assets > Tiles > Outdoor Ground 文件下（自行新建一个 `Tiles` 和 `Outdoor Ground` 文件夹）。Tile Palette 中 Drag Tile, Sprite, Texture... 提示我们将素材拖入，我们将 summer farm tilemap 资源折叠然后整个拖入，将其保存在 Assets > Tiles > Outdoor Ground。为了更好的预览，可以将这个界面的下边界往下拖以放大界面。现在我们基本上已经拥有了想要的所有的瓦片和调色板。

### Using Tilemaps For The Ground

接下来绘制瓦片，左上角的菜单栏 GameObject -> 2D Object -> Tilemap -> Rectangular，将其命名为 `Ground`。于是看到场景里有了网格 Gird，和可以在上面绘制的 `Ground`。

回到 Tile Palette 简单介绍以下几个常用的绘制工具：

![](./Pictures/TilePalette.png)

- 从左往右第三个工具：也就是现在选择的这个是画笔，可以允许我们使用鼠标随意画瓦片。
- 从左往右第四个工具：允许我们使用矩形工具画出大量瓦片。
- 从左往右第六个工具：橡皮擦工具。

我们会发现如果我们填入非整格填满的瓦片的话，就会露出透明的部分，就像下面这样。

![](./Pictures/TileError.png)

解决这个问题的办法就是以这个绿色为底层背景，再在上面添加一层瓦片集。右键 Grid，2D Object -> Tilemap -> Rectangular，将其命名为 `Ground Overlay`，选中之后即可在第一层绿色背景上画新的一层而且不会露出透明部分。

当你第一次放瓦片的时候，你可能看不到你放的这些东西。进入两个 Tilemap 的监视器中，在 Tilemap Renderer 的 Additional Settings 下会看到 Order in Layer 的属性，也就是他们的优先级，此时你会发现这两个 Tilemap 的顺序都是 0，这个时候我测试游戏 Unity 就会随机决定将这两个 Tilemap 中的其中一个显示在另一个之上。因为我想要 `Ground Overlay` 覆盖在 `Ground` 上，因此我们要给它的Order in Layer 设置的比 0 大，这里设置为 `5`。

## Section 4: The Player

### Setting Up The Player

有了场景以后，接下来需要一个可以走动的角色。在 Hierarchy 中右键 Create Empty，新建一个对象并将其命名为 `Player`。我们导入的资源中 Art > Tiny Wonder Farm > Character 中有非常多可供使用的角色图像资源。选择 walk and idle 中的第三个图像，将其拖拽到 Scene 场景当中。此时 Hierarchy 中会出现一个新的对象 `walk and idle_2`，将其重命名为 `Sprite`。接着我们将 Sprite 拖拽到 Player 下。为了使角色在正中心，可以将其 Position 的 X, Y, Z 设置为 `0, 0, 0`，并且我们依旧可能无法在测试时看到角色，同理我们需要将其 Order in Layer 设置为大于 0 的值。

不过再想一下，如果每次我们新的角色，每次都为这个角色都设置 Order in Layer 是很头疼且麻烦的，所以此时我们点击上面 Sorting Layer 的 Default，选择 Add Sorting Layer...，接着会出现一个图层列表，我们在 Sorting Layers 下面点击加号添加新的层，添加两个层，将 `Layer 1` 命名为 `Player`，将 `Layer 2` 命名为 `Ground`。此时加上默认的 `Layer 0` 一共有三个层，这里的 Layer 越大表示其优先级越高，越优先被看到，所以看的顺序是优先从列表底部向顶部的顺序。我们希望玩家始终可见，于是拖动 Layer 改变层的顺序，最终 `Layer 0` 为 `Ground`，`Layer 1` 为 `Default`， `Layer 2` 为 `Player`。

设置完后，回到 Player 下 Sprite 的监视器，将其 Sorting Layer 设置为 `Player`。接着也可以将之前Grid 下的 Ground 和 Ground Overlay 的 Sorting Layer 也设置为 `Ground`（Order in Layer 只对同一 Sorting Layer 生效）。现在真正重要的是我们有了层号顺序！

现在我们要添加所谓的碰撞体 rigid body，碰撞体能够使用 Unity 的输入或内置物理系统。选中 Hierarchy 中的 Player，在其监视器中选择 Add Component 添加新的组件，选择 Physics 2D -> Rigidbody 2D（或直接搜索 Rigidbody 2D）。此时测试游戏，你会发现角色下落了，这里需要将碰撞体的 Gravity Scale 从 1 改为 `0`。

### Setting Up Our First Script

现在，我想要我们的玩家可以四处移动，因此需要脚本来控制角色。首先我们现在资料库中的 Assets 下新建一个用来存放脚本的文件夹 `Scripts`。在 Scripts 文件夹下新建脚本，右键 Create -> MonoBehaviour Script（*Unity 6 中将脚本命名为 MonoBehaviour Script，如果在旧的 Unity 中就是 C# Script*），将其命名为 `PlayerController`。

接着需要将这个脚本与角色绑定起来，将脚本拖入 Player 监视器空白部分即可，在监视器中双击这个脚本就可以用 Visual Studio 编译器打开脚本文件了。此时会看到已经自动为我们写好了两个函数的框架，也对这两个函数的作用做了解释：

- Start()：在 MonoBehavior 创建后首次执行 Update 之前，Start() 函数会被调用一次。
- Update()：每帧调用一次 Update() 函数。

我们知道，现在这里的 Rigidbody 碰撞体控制着我们角色的物理特性，我们想用它来让我们的玩家四处移动。虽然创建的脚本与物体的相关属性在同一个位置，但是脚本无权直接访问与控制这些属性。而一般的做法是创建一个变量。

所以下面这里创建一个名为 `the RB` 的 Rigidbody 2D 类的变量（创建对 Rigidbody 2D 这个组件类型的引用）：

```c#
public Rigidbody2D theRB;
```

此时回到 Unity，会发现 Player 的检查器中多了一个我们刚刚创建好的变量 `The RB`。不过此时它的值是 `None`，你需要将检查器中的 Rigidbody 2D 拖动到下面的 `The RB` 处，或者从 Hierarchy 的场景中将 Player 拖入 `The RB` 中（因为 Player 包含 Rigidbody 2D）。当然，这里如果你不想让在脚本中创建的变量能在 Unity 中被看到且随意修改，你可以将这个变量从 public 改为 private。不过，你也可以点击检查器最右边的省略号，将 Normal 改成 Debug，在调试模式下你也依旧能看到 private 的私有变量。

### Moving The Player

为了让角色移动起来，我们回到脚本给角色创建一个新的变量 `moveSpeed` 用来表示角色的移动速度：

```c#
public float moveSpeed;
```

回到 Unity 就会发现 Player 多了一个 `Move Speed` 的变量，我们可以将其值设置为 `8` 先。

此时如果我们在 Update() 函数中写入：

```c#
theRB.linearVelocity = new Vector2(moveSpeed, 0f);
```

这里的意思是给 `theRB` 变量的 `linearVelocity` 水平增加 `(moveSpeed, 0f)`，这里的 Vector2 新变量包含两个值，一个为 X 轴的值，一个为 Y 轴的值，这里向实现水平移动，所以第一个值是移动的速度，第二个值是 `0f`（`0f` 的意思是浮点数的 0，如果只写 `0` 就是 int 类型的数字 0）。前面说过 Update() 函数每一帧都会调用一次，所以这里每一帧都会增加角色的 X 轴的坐标，开启调试的效果就是角色一直往右边走。

### Controlling The Player

现在来说明如何控制玩家的移动。因此，我们想要做的当然是能够捕捉来自玩家的输入，知道玩家按下了什么来控制实际角色。

好消息是，Unity 内置了一个完整的输入系统，默认设置了一堆东西来处理玩家的各种类型的输入，在 Project 资源库中的 Assets 中可以找到这个系统 InputSystem_Actions（三折叠地图的图标）。我们双击打开这个系统，展开 Move，就可以看到常见的 WASD 移动方式。

了解这个系统之后，我们便可以将其关闭然后回到脚本中了。创建一个 InputSystem Actions 中的类：

```c#
public InputActionReference moveInput;
```

回到 Unity，会看到 Player 多了变量 `Move Input`，不过此时其值为 `None`，点击右边中间有点的圈可以看到很多控制方式，我们选择 Player/Move，现在我们对输入系统上的运动动作有了参考。然后将我们之前在 Update() 函数中的语句改成：

```c#
theRB.linearVelocity = moveInput.action.ReadValue<Vector2>() * moveSpeed;
```

回到 Unity 调试，此时使用 WASD 便可以控制我们的角色了。这里 `moveInput.action.ReadValue<Vector2>()` 是获取玩家输入的方向，乘上角色的移动速度便是整个移动的实现。（如果你有手柄控制器，可以试试一样可以用左摇杆控制移动）

### Limiting Diagonal Movement

调试的时候，我们发现斜着移动的时候速度比水平移动的速度快一些，因为在斜着移动的时候，没有减慢一个方向上的移动速度，只是增加了另一个方向上的速度。这样可能导致键盘的控制方式和手柄控制速度不符的问题。

Unity 为我们提供了解决方案以至于我们不需要计算三角形，其做法就是在 `moveInput.action.ReadValue<Vector2>()` 后面加上 `normalized` 即可标准化输入的向量，将其控制在 0 到 1 之间。

```c#
theRB.linearVelocity = moveInput.action.ReadValue<Vector2>().normalized * moveSpeed;
```

### Setting Up Animations

接下来我们为角色移动加入动画！

首先要知道怎么打开动画窗口，如果你的 Unity 界面没有 Animation 窗口，可以点击左上角 Window -> Animation -> Animation。

我们先为动画创建一个文件夹，在 Assets 中新建 Animations，点击 Player 下的 Sprite，然后在 Animation 中 Create 一个新的动画 `Player_Idle` 在 Animations 文件内。然后选择 Art > Tiny Wonder Farm > Character 资产中的 walk and idle 中选择空闲状态的动作，也就是第三张图和第四张图。我们将第三章图拖动到 Animation 中的 0:00 时间点上，然后将第四张图拖动到 0:15 时间点上，最后再将第三张图拖动到 0:30 时间点上，这样就简单实现了一个空闲动作的循环。

相同的，点击 Animation 中左上角 Player_Idle 位置，我们再在 /Assets/Animations 中新建一个移动的动画 `Player_Move`。将 Art > Tiny Wonder Farm > Character 资产中的 walk and idle 中最后八张图片按 0.05 的间隔一次在时间轴上放置（一共九个关键帧，最后一个是第八张图或第一张图，因为循环动画每次退出最后一帧会很快，这里可以将最后一帧的时间点放在 0:39 上），如下图所示：

![](./Pictures/Move_Animation.png)

### Making The Animator Work

现在让我们将刚刚做完的动画真正作用于我们的角色！

那首先需要知道怎么打开 Animator 窗口，如果你的 Unity 界面没有 Animator 窗口，可以点击左上角 Window -> Animation -> Animator。

Animator 中的 Entry 是进入动画的入口，也就是动画的起点，我们可以右键非默认动画，选择 Set as Layer Default State，将动画改为默认动画，不过这里选择 Player_Idle 为默认动画。还有就是 Any State 状态，基本上是一种从任意特定状态过渡的方式，时刻进入一个新状态。

所以我们要做的就是找到一种方法来在两种状态之间移动，为此我们可以创建一个连接。右键 Player_Idle -> Make Transition，连接 Player_Move。点击箭头，首先我们需要做到是需要勾选 Has Exit Time 这个选项，这样状态转换的时候才不会有延迟。不过这样会跳出一个报错警告，编辑器告诉我们不想直接转到新的动画，现在我们先不去管这个警告。点开下面的 Settings 还有一个需要注意的变量是 Transition Duration，这个是在某些场景下通过这种过渡让角色身体从一个位置平稳运动，让同一个角色的身体从一个位置到另一个位置，不过这里我们只想让 Sprite 快速到另一个状态，所以这里的变量设置为 `0` 即可。

可以看到此时检查器中 Conditions 的变量是没有的，我们可以点击 Animator 中的 Parameters 新建一个 Float 变量 `speed`。然后点击 Conditions 中的加号添加 `speed` 变量。然后选择 `Greater`，并且将值改为 `0.1`，意思是如果速度大于 0.1，那么就执行这个箭头。

相反的，我们需要在 Player_Move 到 Player_Idle 之间做过渡连接，方法与前面一样，然后别忘记给箭头的 Has Exit Time 和 Transition Duration 变量做设置，然后也是个 Conditions 添加一个变量 `speed`，然后选择 `Less`，值为 `0.1`。

接下来我们需要回到脚本，利用脚本控制 `speed` 这个变量。这里新建一个 Animator 类的变量 `anim`：

```c#
public Animator anim;
```

回到 Unity，查看 Sprite，可以看到新建的 Animator 状态栏。点击 Player，我们将 Player 下的 Sprite 拖到 Anim 这个变量中（这个 Sprite 也可以在 /Assets/Animations 下找到）。我们在 Update() 方法下写入：

```c#
anim.SetFloat("speed", theRB.linearVelocity.magnitude);
```

这里的意思是我们设置 anim 的 speed 的数值为 `theRB.linearVelocity.magnitude`，anim 是刚刚创建的对我们角色的动画器实例，前面在 Unity 编辑器中新建的变量 speed 实际上是字符串 String，所以这里要加上双引号并且保证这里的变量名和 Unity 编辑器中新建的变量名完全一致，`theRB.linearVelocity` 表示的是水平方向向量，可以分为 x 和 y 两个方向，但是这里需要的是一个数值，于是取下面的 `magnitude` 方法，表示其值。

如此，我们便设置了角色的动画！

### Flipping The Player

最后我们来实现角色行走时的翻转！

----

这里贴一个前面课程的方法做对比（仅供参考【也可以实现翻转】，后面是本次课程的方法）：

我们在代码中创建一个布尔值 `facingRight` （默认情况下角色将朝右）：

```c#
private bool facingRight = true;
```

然后我们写一个翻转方法，就是当执行这个方法时 `facingRight` 这个布尔值不等于它自己也就是相反，然后旋转角色进行翻转：

```c#
private void Flip()
    {
        facingRight = !facingRight;
        transform.Rotate(0, 180, 0);
    }
```

然后我们创建一个新方法 FlipController() 调用 Flip() 方法即可，具体实现为当角色向左移动时，其 x 轴上的速度为负数，然后此时如果 facingRight 也为 true 也就是此时角色朝右，我们就进行翻转，向右时反之：

```c#
private void FlipController()
    {
        if (theRB.linearVelocity.x < 0 && facingRight)
        {
            Flip();
        }
        else if (theRB.linearVelocity.x > 0 && !facingRight)
        {
            Flip();
        }
    }
```

最后我们在 Update() 方法中调用 FlipController() 方法即可：

```c#
FlipController();
```

----

这里需要注意的一点是，我们翻转的时候是翻转 Player，而不是 Player 下的 Sprite 图片，因为我们之后可能会需要让角色拿东西，而这个东西的贴图也是在 Player 下的，如果只翻转 Sprite 显然是不对的，一定要翻转 Player。而这里翻转的是 Player 中的 `Scale` 值。从 Unity 编辑器上看，如果将 Player 的 `Scale` 的 X 改为 `-1`，可以看到角色翻转了，所以这里更简单的方法是在 Update() 方法中：

```c#
if(theRB.linearVelocity.x < 0f)
{
    transform.localScale = new Vector3(-1f, 1f, 1f);
}
else if(theRB.linearVelocity.x > 0f)
{
    transform.localScale = Vector3.one;
}
```

这里的意思是，如果角色的水平方向小于 0，也就是此时角色有向左的速度，此时将其 Scale 值转变为 `(-1f, 1f, 1f)`，也就是将 Player 的 `Scale` 的 X 改为 `-1`，否则其 Scale 为 `(1, 1, 1)`。这里的几个小细节是，`theRB.linearVelocity.x` 表示 X 轴方向上的向量，`transform.localScale` 表示改变 Scale 的值，`Vector3` 的 3 表示三个轴（因为 Scale 分 X, Y, Z 三个方向），`Vector3.one` 表示的是将三个值写为 (1, 1, 1)。如果这里只写 else，我们测试游戏的时候如果向左移动然后松手，玩家就会翻转回来依旧朝着右侧，因为只写 else，当玩家朝着左侧时此时其速度为 0，在下一次判定中速度为 0，小于 0 不满足，所以进入了 else 条件导致其翻转回来，因此这里的 else if 判定语句是一定要加的。

以上便是这个玩家控制相关的内容，完整脚本代码如下：

```c#
using UnityEngine;
using UnityEngine.InputSystem;

public class PlayerController : MonoBehaviour
{
    public Rigidbody2D theRB;
    public float moveSpeed;

    public InputActionReference moveInput;

    public Animator anim;

    // Start is called once before the first execution of Update after the MonoBehaviour is created
    void Start()
    {
        
    }

    // Update is called once per frame
    void Update()
    {
        theRB.linearVelocity = moveInput.action.ReadValue<Vector2>().normalized * moveSpeed;

        anim.SetFloat("speed", theRB.linearVelocity.magnitude);

        if(theRB.linearVelocity.x < 0f)
        {
            transform.localScale = new Vector3(-1f, 1f, 1f);
        }
        else if(theRB.linearVelocity.x > 0f)
        {
            transform.localScale = Vector3.one;
        }
    }

}

```

