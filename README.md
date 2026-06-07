# SkinAI 安卓打包工程

这个工程把你的网页(`skinai_v4_accurate.html`)封装成了一个标准的安卓 App。
- ✅ 网页已**内置**进 App,**完全离线**也能运行(不依赖你的 GitHub Pages 网站)。
- ✅ 图表库 Chart.js 已本地化,断网也能正常显示图表。
- ✅ 已配置**摄像头权限**,App 内的"实时监测"相机功能可正常使用。
- ✅ 应用名:**SkinAI**;包名:**com.skinai.app**;支持 **Android 7.0 及以上**(覆盖几乎所有在用手机)。

最终产物是一个 `.apk` 文件,任何国家、任何安卓手机都可以下载后直接安装(无需上架应用商店)。

---

## 方法一:用 GitHub 自动编译(推荐,无需在电脑上装任何东西)

你已经在用 GitHub,这是最省事的方式。

1. **新建一个空仓库**(例如叫 `skinai-app`)。
2. 把本工程里的**所有文件**上传到该仓库(可直接网页拖拽上传,或用 git 推送)。
   - 注意要包含隐藏文件夹 `.github`(里面是自动编译脚本)。
3. 上传后,GitHub 会**自动开始编译**。也可以进入仓库的 **Actions** 标签页,手动点击运行 `Build Android APK`。
4. 等待约 3–5 分钟,编译完成后:
   - 进入仓库右侧的 **Releases**,会看到一个名为 **`SkinAI 最新版`** 的发布,里面的 **`SkinAI.apk`** 就是安装包。
   - 这个下载链接是**公开的**,任何人(无需登录 GitHub)点开就能下载。把这个链接发给别人即可。

> 想换图标或应用名?见下方"自定义"。改完重新上传,会自动编译出新版本。

---

## 方法二:在自己电脑上用 Android Studio 编译

适合想本地调试的人。

1. 安装 [Android Studio](https://developer.android.com/studio)(免费)。
2. 安装 [Node.js](https://nodejs.org)。
3. 在工程根目录执行:
   ```bash
   npm install
   npm run open        # 用 Android Studio 打开 android 工程
   ```
4. 在 Android Studio 里点击菜单 **Build → Build APP Bundle(s) / APK(s) → Build APK(s)**。
5. 编译好的 APK 在 `android/app/build/outputs/apk/debug/app-debug.apk`。

或者纯命令行:
```bash
npm run build:apk
# 产物:android/app/build/outputs/apk/debug/app-debug.apk
```

---

## 手机上如何安装这个 APK

1. 把 `SkinAI.apk` 传到手机(下载链接、微信、数据线均可)。
2. 点击打开,系统会提示"未知来源",按提示**允许安装此来源的应用**。
3. 安装后首次使用相机功能时,**允许摄像头权限**即可。

---

## 自定义(可选)

- **改应用名**:编辑 `android/app/src/main/res/values/strings.xml` 里的 `app_name`。
- **改包名**:修改 `capacitor.config.json` 的 `appId`(如发布多个 App 需保证唯一)。
- **换图标**:在 Android Studio 中右键 `app` → New → Image Asset,导入你的图标;
  或直接替换 `android/app/src/main/res/mipmap-*` 下的 `ic_launcher` 图片。
- **更新网页内容**:替换 `www/index.html`,再重新上传/编译即可。

---

## 关于"正式签名"与应用商店(进阶,通常不需要)

- 上面产出的是 **debug 签名**的 APK,**可以正常侧载安装、自由分发**,适合"任何人下载安装"的需求。
- 如果今后要上架 **Google Play**,需要改用**正式签名(release keystore)**并打包成 AAB,流程更复杂,可届时再处理。
- 提示:这是一款与皮肤健康相关的应用。如果作为正式的医疗/诊断工具大范围分发,部分国家对"医疗器械软件"有监管要求,应用分发平台也可能有健康类内容政策——按需了解即可,侧载分发本身不受应用商店审核限制。
