# Nestly 法律文档中心

这个仓库包含了Nestly智能物品管理应用的所有法律文档，用于iOS App Store审核。

## 📁 文件结构

```
nestly-webinfo/
├── index.html                    # 主页
├── privacy-policy.html          # 隐私政策
├── terms-of-service.html        # 服务条款
├── subscription-terms.html      # 订阅服务条款
├── css/
│   └── style.css               # 统一样式文件
├── assets/                     # 资源文件夹（Logo等）
└── README.md                   # 本文件
```

## 🚀 快速部署到GitHub Pages

### 第一步：初始化Git仓库

```bash
cd /Users/yang/Documents/code/GitHub/nestly-webinfo
git init
git add .
git commit -m "Initial commit: Nestly legal documents"
```

### 第二步：在GitHub创建仓库

1. 访问 https://github.com/new
2. 仓库名称：`nestly-webinfo`
3. 描述：`Legal documents for Nestly app`
4. 选择 **Public**（必须是公开仓库才能使用免费的GitHub Pages）
5. 不要勾选任何初始化选项（README、.gitignore、License）
6. 点击 **Create repository**

### 第三步：推送到GitHub

```bash
git remote add origin https://github.com/nestly-young/nestly-webinfo.git
git branch -M main
git push -u origin main
```

### 第四步：启用GitHub Pages

1. 在GitHub仓库页面，点击 **Settings**（设置）
2. 在左侧菜单找到 **Pages**
3. 在 **Source** 下拉菜单中选择 `main` 分支
4. 文件夹选择 `/ (root)`
5. 点击 **Save**
6. 等待几分钟，页面会显示：
   ```
   Your site is published at https://nestly-young.github.io/nestly-webinfo/
   ```

## 🌐 访问地址

部署成功后，你的法律文档将在以下地址访问：

- **主页：** https://nestly-young.github.io/nestly-webinfo/
- **隐私政策：** https://nestly-young.github.io/nestly-webinfo/privacy-policy.html
- **服务条款：** https://nestly-young.github.io/nestly-webinfo/terms-of-service.html
- **订阅条款：** https://nestly-young.github.io/nestly-webinfo/subscription-terms.html

## 📝 在App Store Connect中填写

在提交iOS应用审核时，需要在App Store Connect中填写以下URL：

1. **Privacy Policy URL（隐私政策URL）：**
   ```
   https://nestly-young.github.io/nestly-webinfo/privacy-policy.html
   ```

2. **Terms of Service URL（服务条款URL，可选）：**
   ```
   https://nestly-young.github.io/nestly-webinfo/terms-of-service.html
   ```

## 🔄 更新文档

当需要更新法律文档时：

```bash
# 1. 修改对应的HTML文件
# 2. 提交并推送更改
git add .
git commit -m "Update legal documents"
git push origin main

# GitHub Pages会自动重新部署，通常需要1-5分钟生效
```

## ✅ iOS审核检查清单

在提交审核前，请确认：

- [x] 所有联系方式真实有效（邮箱：450861294@qq.com）
- [x] 隐私政策详细说明了数据收集和使用
- [x] 明确说明了第三方服务（DashScope、阿里云、RevenueCat）
- [x] 语音数据处理说明准确（上传到云端）
- [x] 照片/相机权限说明清晰
- [x] 订阅条款明确说明价格、续费、取消方式
- [x] 有清晰的数据删除/账户删除方式
- [x] 所有页面可以正常访问，无需登录

## 📱 在Flutter应用中使用

### 方案1：应用内WebView（推荐）

在 `pubspec.yaml` 添加依赖：
```yaml
dependencies:
  url_launcher: ^6.2.0
```

修改代码：
```dart
import 'package:url_launcher/url_launcher.dart';

Future<void> _showPrivacyPolicy() async {
  final url = Uri.parse('https://nestly-young.github.io/nestly-webinfo/privacy-policy.html');
  if (await canLaunchUrl(url)) {
    await launchUrl(
      url,
      mode: LaunchMode.inAppWebView, // 应用内WebView
    );
  }
}
```

### 方案2：混合方案（最佳）

优先加载网页版本，失败时使用本地Markdown备份：
```dart
Future<void> _showLegalDocument(LegalDocumentType type) async {
  final url = _getDocumentUrl(type);

  // 尝试加载网页版本
  try {
    if (await canLaunchUrl(url)) {
      await launchUrl(url, mode: LaunchMode.inAppWebView);
      return;
    }
  } catch (e) {
    debugPrint('无法打开网页，使用本地版本: $e');
  }

  // Fallback到本地Markdown
  final document = await LegalDocumentService.loadDocument(type);
  // ... 显示本地版本
}

Uri _getDocumentUrl(LegalDocumentType type) {
  const baseUrl = 'https://nestly-young.github.io/nestly-webinfo';
  switch (type) {
    case LegalDocumentType.privacyPolicy:
      return Uri.parse('$baseUrl/privacy-policy.html');
    case LegalDocumentType.termsOfService:
      return Uri.parse('$baseUrl/terms-of-service.html');
    case LegalDocumentType.subscriptionTerms:
      return Uri.parse('$baseUrl/subscription-terms.html');
  }
}
```

## 🔧 技术细节

### 响应式设计
所有页面都采用响应式设计，在移动设备和桌面浏览器上都有良好的显示效果。

### SEO优化
- 每个页面都有适当的meta描述
- 使用语义化HTML标签
- 清晰的标题层次结构

### 性能优化
- 纯静态HTML，加载速度快
- 统一的CSS文件，减少HTTP请求
- 适合GitHub Pages的免费托管

## 📞 联系方式

- **邮箱：** 450861294@qq.com
- **开发者：** nestly-young
- **GitHub：** https://github.com/nestly-young/nestly

## 📄 许可证

本仓库中的法律文档仅用于Nestly应用，版权归开发者所有。

---

**最后更新：** 2025年1月1日
