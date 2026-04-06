# Unity工程结构规范

> **引擎**: Unity 2022.3 LTS  
> **渲染管线**: URP (Universal Render Pipeline)  
> **创建日期**: 2026-04-06

---

## 目录结构

```
Assets/
├── _Project/                          # 🔴 项目核心代码（主要工作区）
│   ├── Scripts/
│   │   ├── Core/                     # 核心框架
│   │   │   ├── EventSystem/          # 事件系统
│   │   │   │   ├── GameEvent.cs
│   │   │   │   ├── EventListener.cs
│   │   │   │   └── EventManager.cs
│   │   │   ├── StateMachine/         # 状态机
│   │   │   │   ├── State.cs
│   │   │   │   ├── StateMachine.cs
│   │   │   │   └── StateTransition.cs
│   │   │   ├── Pool/                 # 对象池
│   │   │   │   ├── ObjectPool.cs
│   │   │   │   └── PoolManager.cs
│   │   │   ├── DI/                   # 依赖注入
│   │   │   │   ├── Container.cs
│   │   │   │   └── Injector.cs
│   │   │   └── Utils/                # 工具类
│   │   │       ├── MonoSingleton.cs
│   │   │       ├── SafeArea.cs
│   │   │       └── Extensions/
│   │   │           ├── TransformExtensions.cs
│   │   │           └── StringExtensions.cs
│   │   │
│   │   ├── Game/                     # 游戏逻辑
│   │   │   ├── Player/               # 玩家系统
│   │   │   │   ├── PlayerController.cs
│   │   │   │   ├── PlayerData.cs
│   │   │   │   ├── PlayerInput.cs
│   │   │   │   └── PlayerView.cs
│   │   │   │
│   │   │   ├── Building/             # 建筑系统
│   │   │   │   ├── BuildingController.cs
│   │   │   │   ├── BuildingData.cs
│   │   │   │   └── BuildingView.cs
│   │   │   │
│   │   │   ├── Economy/              # 经济系统
│   │   │   │   ├── CurrencyManager.cs
│   │   │   │   ├── ResourceManager.cs
│   │   │   │   └── MarketSystem.cs
│   │   │   │
│   │   │   ├── Quest/                # 任务系统
│   │   │   │   ├── QuestManager.cs
│   │   │   │   ├── QuestData.cs
│   │   │   │   └── QuestUI.cs
│   │   │   │
│   │   │   ├── UI/                   # 游戏UI
│   │   │   │   ├── MainMenu/
│   │   │   │   ├── HUD/
│   │   │   │   ├── Shop/
│   │   │   │   └── Inventory/
│   │   │   │
│   │   │   └── Managers/             # 游戏管理器
│   │   │       ├── GameManager.cs
│   │   │       ├── SceneManager.cs
│   │   │       ├── SaveManager.cs
│   │   │       └── AudioManager.cs
│   │   │
│   │   ├── Network/                  # 网络系统
│   │   │   ├── Client/
│   │   │   │   ├── NetworkClient.cs
│   │   │   │   └── ConnectionManager.cs
│   │   │   ├── Protocol/
│   │   │   │   ├── MessageTypes.cs
│   │   │   │   ├── PacketHandler.cs
│   │   │   │   └── Serializer.cs
│   │   │   └── Models/
│   │   │       ├── PlayerState.cs
│   │   │       └── GameState.cs
│   │   │
│   │   └── Editor/                   # 编辑器工具
│   │       ├── BuildTools/
│   │       └── DataTools/
│   │
│   ├── Prefabs/                      # 预制体
│   │   ├── Characters/
│   │   ├── Buildings/
│   │   ├── UI/
│   │   ├── Effects/
│   │   └── Environment/
│   │
│   ├── Scenes/                       # 场景
│   │   ├── Boot.unity                # 启动场景
│   │   ├── Loading.unity             # 加载场景
│   │   ├── MainMenu.unity            # 主菜单
│   │   ├── Game.unity                # 游戏主场景
│   │   └── Test/                     # 测试场景
│   │
│   ├── ScriptableObjects/            # 可配置数据
│   │   ├── Configs/                  # 游戏配置
│   │   │   ├── GameConfig.asset
│   │   │   ├── PlayerConfig.asset
│   │   │   └── EconomyConfig.asset
│   │   └── Variables/                # 全局变量
│   │       ├── GlobalVariables.asset
│   │       └── RuntimeVariables.asset
│   │
│   ├── Resources/                    # 运行时加载资源
│   │   ├── Data/
│   │   ├── Configs/
│   │   └── Localization/
│   │
│   ├── Settings/                     # 项目设置
│   │   ├── InputSystem.inputsettings.asset
│   │   ├── URP-HighFidelity.asset
│   │   └── URP-Performant.asset
│   │
│   └── Plugins/                      # 第三方插件
│       ├── Mirror/
│       ├── DOTween/
│       └── UniTask/
│
├── _External/                        # 🟡 外部资源
│   ├── Textures/
│   │   ├── Characters/
│   │   ├── UI/
│   │   └── Environment/
│   ├── Audio/
│   │   ├── BGM/
│   │   ├── SFX/
│   │   └── Voice/
│   ├── Models/
│   │   ├── Characters/
│   │   └── Buildings/
│   ├── Animations/
│   │   ├── Characters/
│   │   └── UI/
│   ├── Fonts/
│   │   ├── Chinese/
│   │   └── English/
│   └── Materials/
│       ├── URP/
│       └── Shaders/
│
├── AddressableAssetsData/            # Addressable配置
│   ├── AssetGroups/
│   ├── AssetGroupTemplates/
│   └── ProfileDataSourceSettings.asset
│
└── Packages/                         # 包管理
    └── manifest.json
```

---

## 关键配置文件

### manifest.json

```json
{
  "dependencies": {
    "com.unity.2d.animation": "9.1.1",
    "com.unity.2d.pixel-perfect": "5.0.3",
    "com.unity.2d.psdimporter": "8.0.5",
    "com.unity.2d.sprite": "1.0.0",
    "com.unity.addressables": "1.21.21",
    "com.unity.cinemachine": "2.9.7",
    "com.unity.collab-proxy": "2.3.1",
    "com.unity.ide.rider": "3.0.28",
    "com.unity.ide.visualstudio": "2.0.22",
    "com.unity.ide.vscode": "1.2.5",
    "com.unity.inputsystem": "1.7.0",
    "com.unity.render-pipelines.universal": "14.0.11",
    "com.unity.test-framework": "1.1.33",
    "com.unity.textmeshpro": "3.0.6",
    "com.unity.timeline": "1.7.6",
    "com.unity.toolchain.win-x86_64-linux-x86_64": "2.0.9",
    "com.unity.ugui": "1.0.0",
    "com.unity.visualscripting": "1.9.4",
    "com.unity.modules.ai": "1.0.0",
    "com.unity.modules.androidjni": "1.0.0",
    "com.unity.modules.animation": "1.0.0",
    "com.unity.modules.assetbundle": "1.0.0",
    "com.unity.modules.audio": "1.0.0",
    "com.unity.modules.cloth": "1.0.0",
    "com.unity.modules.director": "1.0.0",
    "com.unity.modules.imageconversion": "1.0.0",
    "com.unity.modules.imgui": "1.0.0",
    "com.unity.modules.jsonserialize": "1.0.0",
    "com.unity.modules.particlesystem": "1.0.0",
    "com.unity.modules.physics": "1.0.0",
    "com.unity.modules.physics2d": "1.0.0",
    "com.unity.modules.screencapture": "1.0.0",
    "com.unity.modules.terrain": "1.0.0",
    "com.unity.modules.terrainphysics": "1.0.0",
    "com.unity.modules.tilemap": "1.0.0",
    "com.unity.modules.ui": "1.0.0",
    "com.unity.modules.uielements": "1.0.0",
    "com.unity.modules.umbra": "1.0.0",
    "com.unity.modules.unityanalytics": "1.0.0",
    "com.unity.modules.unitywebrequest": "1.0.0",
    "com.unity.modules.unitywebrequestassetbundle": "1.0.0",
    "com.unity.modules.unitywebrequestaudio": "1.0.0",
    "com.unity.modules.unitywebrequesttexture": "1.0.0",
    "com.unity.modules.unitywebrequestwww": "1.0.0",
    "com.unity.modules.vehicles": "1.0.0",
    "com.unity.modules.video": "1.0.0",
    "com.unity.modules.vr": "1.0.0",
    "com.unity.modules.wind": "1.0.0",
    "com.unity.modules.xr": "1.0.0",
    "com.unity.nuget.newtonsoft-json": "3.2.1",
    "com.unity.ui.toolkit": "1.0.0"
  }
}
```

---

## 命名规范

### 文件夹命名

```
✅ PascalCase: Scripts, Prefabs, Scenes
✅ 复数形式: Scripts (不是Script), Prefabs (不是Prefab)
✅ 清晰描述: PlayerControllers (不是PC)
```

### 文件命名

```csharp
// C#脚本: PascalCase + 描述性
PlayerController.cs
EnemyAI.cs
GameManager.cs

// 预制体: PascalCase + 类型后缀
PlayerCharacter.prefab
MainMenuUI.prefab
CoinPickup.prefab

// 场景: PascalCase
MainMenu.unity
Level01.unity
LoadingScreen.unity

// 资源: 类型前缀 + 描述
TX_Player_Idle.png      // Texture
AUD_BGM_Main.mp3        // Audio
MAT_Ground_Grass.mat    // Material
ANIM_Player_Run.anim    // Animation
FNT_Main.ttf            // Font
```

---

## 场景管理

### 场景加载流程

```
Boot.unity
    ↓
Loading.unity (显示加载界面)
    ↓
MainMenu.unity 或 Game.unity
```

### Addressable分组

```
Default Local Group:
  - 核心资源
  - 常驻内存

Characters:
  - 角色预制体
  - 按需加载

Levels:
  - 关卡场景
  - 切换时加载

UI:
  - UI预制体
  - 按需加载
```

---

## 版本控制忽略

### .gitignore

```gitignore
# Unity
[Ll]ibrary/
[Tt]emp/
[Oo]bj/
[Bb]uild/
[Bb]uilds/
[Ll]ogs/
[Mm]emoryCaptures/

# Asset meta data should only be ignored when the corresponding asset is also ignored
!/[Aa]ssets/**/*.meta

# Uncomment this line if you wish to ignore the asset store tools plugin
# /[Aa]ssets/AssetStoreTools*

# Autogenerated Jetbrains Rider plugin
[Aa]ssets/Plugins/Editor/JetBrains*

# Visual Studio cache directory
.vs/

# Gradle cache directory
.gradle/

# Autogenerated VS/MD/Consulo solution and project files
ExportedObj/
.consulo/
*.csproj
*.unityproj
*.sln
*.suo
*.tmp
*.user
*.userprefs
*.pidb
*.booproj
*.svd
*.pdb
*.mdb
*.opendb
*.VC.db

# Unity3D generated meta files
*.pidb.meta
*.pdb.meta
*.mdb.meta

# Unity3D generated file on crash reports
sysinfo.txt

# Builds
*.apk
*.aab
*.unitypackage

# Crashlytics generated file
crashlytics-build.properties

# Packed Addressables
/[Aa]ssets/[Aa]ddressable[Aa]ssets[Dd]ata/*/*.bin*

# Temporary auto-generated Android Assets
/[Aa]ssets/[Ss]treamingAssets/aa.meta
/[Aa]ssets/[Ss]treamingAssets/aa/*
```

---

## 开发工作流

### 每日开发流程

```
1. 从main创建feature分支
   git checkout -b feature/v0.1/f001-login

2. 在Unity中开发
   - 编辑场景
   - 编写代码
   - 测试功能

3. 提交更改
   git add .
   git commit -m "feat(login): 实现登录界面"

4. 推送分支
   git push origin feature/v0.1/f001-login

5. 创建PR
   - 在GitHub创建PR
   - 等待审查
   - 合并到main
```

---

## 性能优化检查点

### 场景优化

```
✅ 静态批处理 (Static Batching)
✅ 动态批处理 (Dynamic Batching)
✅ GPU Instancing
✅ 对象池 (Object Pooling)
✅ 异步加载 (Addressables)
✅ LOD (Level of Detail)
✅ 遮挡剔除 (Occlusion Culling)
```

### 代码优化

```
✅ 缓存Transform引用
✅ 使用对象池
✅ 避免在Update中分配内存
✅ 使用UniTask替代Coroutine
✅ 事件驱动替代轮询
```

---

## 参考

- [Unity项目组织最佳实践](https://docs.unity3d.com/Manual/BestPracticeGuides.html)
- [Addressable Assets System](https://docs.unity3d.com/Packages/com.unity.addressables@1.21/manual/index.html)
- [Unity URP](https://docs.unity3d.com/Packages/com.unity.render-pipelines.universal@14.0/manual/index.html)
