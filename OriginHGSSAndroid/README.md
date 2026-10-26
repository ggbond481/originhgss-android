# 起源心金 4.0 存档编辑器 Android 工程

这是把最终 HTML 编辑器封装成 Android WebView 应用的工程源文件。包含：
- 本地加载 HTML；
- Android 文件选择器导入 `.dsv/.sav/.nds/.txt`；
- 使用系统“保存文件”对话框导出修改后的存档（避免 WebView 的 blob 下载不兼容）；
- WebView 本地存储和联网权限（名称表/码表需要网络时使用）。

## 构建 APK

需要安装 Android Studio（推荐 Koala 或更新版本）和 Android SDK Platform 35。
1. 解压此工程 ZIP。
2. Android Studio 选择 **Open**，打开 `OriginHGSSAndroid` 文件夹。
3. 等待 Gradle Sync；如果提示安装 SDK Platform 35 / Build Tools，按提示安装。
4. 菜单 **Build → Build APK(s)**。
5. APK 通常位于 `app/build/outputs/apk/debug/app-debug.apk`。

注意：当前运行环境没有 Android SDK、Gradle 或 aapt 工具，且无法联网下载构建工具，因此这里无法直接编译出经过验证的 APK；本包提供可在 Android Studio 中构建的完整工程，而不是伪装成 APK 的文件。

## 没有 Android Studio：使用 GitHub 云端自动构建

工程已附带 `.github/workflows/build-apk.yml`，可在 GitHub Actions 云端构建 APK，不需要在自己的手机/电脑安装 Android Studio。

1. 在 GitHub 新建一个空仓库。
2. 将本工程解压后的**文件和文件夹内容**上传到仓库根目录（包括 `.github` 文件夹；若手机端看不到隐藏文件夹，请先在电脑/文件管理器开启显示隐藏文件，或通过网页上传时确认 `.github/workflows/build-apk.yml` 已上传）。
3. 打开仓库的 **Actions** 标签，选择 **Build Android APK**，点击 **Run workflow**。首次使用时按页面提示启用 Actions。
4. 等待运行完成，点开绿色成功的任务，在 **Artifacts** 区域下载 `OriginHGSS-debug-apk`，解压后得到 `app-debug.apk`。
5. 把 `app-debug.apk` 下载到 Android 手机上，允许安装此来源的应用后安装。

这是 debug 签名 APK，适合个人测试；不要把它当作正式发布签名版本。上传到 GitHub 的仓库建议设为 **Private**，因为项目内含编辑器源码。
