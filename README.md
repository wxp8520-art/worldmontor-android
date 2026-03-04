# WorldMonitor Android App

完整Android Studio项目，用于在创维65寸电子白板上运行WorldMonitor并自动翻译新闻内容为中文。

## 项目结构

```
WorldMonitorApp/
├── app/
│   ├── src/main/
│   │   ├── java/com/worldmonitor/app/
│   │   │   ├── MainActivity.kt      # 主活动 - WebView + 翻译
│   │   │   └── BootReceiver.kt      # 开机自启
│   │   ├── res/
│   │   │   ├── layout/
│   │   │   │   └── activity_main.xml
│   │   │   ├── values/
│   │   │   │   ├── strings.xml
│   │   │   │   └── themes.xml
│   │   │   └── xml/
│   │   │       └── network_security_config.xml
│   │   └── AndroidManifest.xml
│   ├── build.gradle
│   └── proguard-rules.pro
├── build.gradle
└── settings.gradle
```

## 功能特性

- ✅ WebView 加载 worldmonitor.app
- ✅ 全屏显示（隐藏状态栏/导航栏）
- ✅ 开机自启动
- ✅ 中文翻译（关键词映射 + 标记）
- ✅ 翻译按钮（右上角）
- ✅ 自动翻译新加载的内容
- ✅ 保持屏幕常亮

## 翻译实现

使用JavaScript注入，包含1000+关键词映射：
- `breaking` → `突发`
- `conflict` → `冲突`
- `war` → `战争`
- ...（共1000+词条）

## 构建步骤

### 1. 打开项目
```bash
# 使用 Android Studio 打开 WorldMonitorApp 文件夹
```

### 2. 同步项目
```
File → Sync Project with Gradle Files
```

### 3. 构建APK
```
Build → Build Bundle(s) / APK(s) → Build APK(s)
```

### 4. 输出路径
```
app/build/outputs/apk/debug/app-debug.apk
app/build/outputs/apk/release/app-release-unsigned.apk
```

## 安装到创维白板

### 方法1: ADB
```bash
adb install app-debug.apk
```

### 方法2: U盘
1. 复制APK到U盘
2. 插入白板USB口
3. 文件管理器安装

## 配置开机自启

应用已配置开机自启权限，但部分系统可能需要额外设置：

### 创维白板设置
1. 设置 → 应用 → 自启动管理
2. 找到 "WorldMonitor 中文"
3. 开启自启动权限

## 使用说明

1. **启动应用**：自动全屏加载worldmonitor.app
2. **翻译内容**：点击右上角"🌐 翻译"按钮
3. **自动翻译**：新内容加载后自动翻译（2秒延迟）
4. **返回键**：拦截返回键防止退出

## 定制翻译

编辑 `MainActivity.kt` 中的 `dict` 字典添加更多词条：

```kotlin
val dict = mapOf(
    "newword" to "新词",
    // 添加更多...
)
```

## 注意事项

- 首次启动需要网络连接
- 翻译基于关键词映射，可能不完美
- 如需更精确翻译，可接入DeepL/Google Translate API

## 技术栈

- Kotlin
- Android WebView
- JavaScript Injection
