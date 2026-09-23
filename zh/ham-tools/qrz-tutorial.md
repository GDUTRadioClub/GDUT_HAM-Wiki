---
title: QRZ 呼号数据库使用与 Page 编辑美化教程
description: 总结 QRZ.com 注册、登录、呼号 Page（Biography）HTML/CSS 编辑流程及 BI7KHI 美化示例
published: true
date: 2026-09-09T14:50:00.000Z
tags: QRZ, 业余无线电, 教程, 呼号数据库, BI7KHI
editor: markdown
dateCreated: 2026-09-09T14:50:00.000Z
---

# QRZ 呼号数据库使用与 Page 编辑美化教程

> 本文面向广工无线电社 / 业余无线电爱好者，整理 **QRZ.com** 的注册、登录、呼号 Page（Biography）HTML/CSS 编辑流程，并以 **BI7KHI** 为例展示“迭代美化 Page”的完整过程。适合在 Wiki 中作为入门教程分享。

---

## 1. QRZ.com 是什么？

[QRZ.com](https://www.qrz.com/) 是全球最大的业余无线电呼号数据库网站，主要功能包括：

- **呼号查询**：按 Callsign、姓名、地址、网格等查询全球业余电台信息；
- **个人 Page / Biography**：每个呼号可以维护自己的中英文简介、设备、QSL 政策、联系方式等，并支持 **HTML / CSS 美化**；
- **社区功能**：论坛、新闻、Swapmeet（跳蚤市场）、Logbook（通联日志）、Awards 等。

---

## 2. 注册与登录

### 2.1 注册

1. 打开 <https://www.qrz.com/>；
2. 点击页面右上角的 `login` 或 `help/register`；
3. 进入注册页面，按提示填写：
   - 呼号 / 用户名；
   - 电子邮箱；
   - 密码；
   - 其他个人信息（姓名、地址、网格等）；
4. 完成邮箱/人工验证后即可开始使用。

![QRZ 首页](/ham-tools/qrz/qrz-home.png)

### 2.2 登录

1. 点击 `login`，进入登录页：

![QRZ 登录页](/ham-tools/qrz/qrz-login.png)

2. 输入 **用户名 / 呼号** 和 **密码**，如开启两步验证则填写 2FA 验证码；
3. 登录成功后，页面右上角会显示当前呼号，并出现 `Edit <呼号>` 与 `Account` 等管理入口。

> 注意：QRZ 登录态保存在浏览器 Cookie 中。若重启浏览器/清理会话，可能需要重新登录。

---

## 3. 找到并编辑自己的 Page（Biography）

### 3.1 进入 Callsign Update Manager

登录后：

1. 访问自己的呼号页，例如 <https://www.qrz.com/db/BI7KHI>；
2. 点击顶部菜单的 `Edit BI7KHI`；
3. 进入 **Callsign Update Manager**，可以看到以下操作入口：

- Update the basic **callsign data**（基础资料）
- **Add or edit your biography** text, fonts, etc.（**Page 内容主体**）
- Add or edit your **pictures** and QSL images
- Map, Grid Square, and coordinate settings
- **Expert** options including **CSS styles**（高级 CSS 样式）
- Manage your Web Contact Logs
- Add a special callsign...（加后缀呼号）
- Help / FAQ / Done

![Callsign Update Manager](/ham-tools/qrz/qrz-bi7khi-edit.png)

### 3.2 编辑 Biography（HTML Page）

1. 点击 `Add or edit your biography text, fonts, etc.`；
2. 进入 **Edit Bio** 页面，默认是所见即所得（WYSIWYG）的 CKEditor：

![Bio 编辑器](/ham-tools/qrz/qrz-bi7khi-bio-edit.png)

3. **点击工具栏上的 `Source` 按钮**，切换到 HTML 源码编辑模式：

![HTML Source 模式](/ham-tools/qrz/qrz-bi7khi-bio-source.png)

4. 在源码区域粘贴或编辑自己的 HTML（支持 `<div>`、`<span>`、`<a>`、`<img>`、`<strong>` 等常用标签，以及 `style="..."` 内联样式）；
5. 编辑完成后**再点一次 `Source`** 返回预览；
6. 点击页面顶部的 `Save` 保存。

> 关键点：**必须点击 Source 才能进入 HTML 源码编辑**。直接使用 WYSIWYG 工具栏只能做富文本有限格式调整。

### 3.3 高级 CSS 样式（Expert Options）

如果希望整页调用号样式更统一（字体、颜色、背景、链接色等），可以：

1. 在 Callsign Update Manager 点击 `Expert options including CSS styles`；
2. 在 `Custom CSS styles for the BI7KHI callsign page` 文本框中编写 CSS；
3. 点击 `Save`。

![Expert CSS 编辑器](/ham-tools/qrz/qrz-bi7khi-css-edit.png)

示例 CSS：

```css
#csbody {
    color: #1f2937;
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
    line-height: 1.75;
    font-size: 14px;
}

#biodata {
    color: #1f2937;
    max-width: 960px;
    margin: 0 auto;
}

#biodata img {
    max-width: 100%;
    height: auto;
}

#biodata a {
    color: #0066cc;
    text-decoration: none;
}

#t_bio.biodiv {
    background-color: #ffffff;
}
```

---

## 4. QRZ Bio 内容规则（必须遵守）

在编辑页底部点击 `content rules [+]` 可以查看完整规则。摘要如下：

- ❌ 禁止色情 / 裸露 / 性暗示图片，QRZ 是家庭友好网站；
- ❌ 禁止使用 **JavaScript**、`<script>` 标签、`onclick` / `onmouseover` 等 **HTML 事件属性**；
- ❌ 禁止页面上出现自动播放声音/音乐；
- ❌ 禁止第三方付费广告；
- ❌ 禁止展示 **QR Code** 图片；
- ❌ 禁止使用遮盖广告、站点菜单、页面导航或隐藏内容的 HTML；
- ❌ 禁止违规/非法内容、暴力、仇恨言论、版权侵权；
- ❌ 未经许可不得擅自修改他人页面；
- ✅ 图片需托管在 QRZ 网站；`flagcounter.com`、`revolvermaps.com` 等少数第三方计数器获得豁免；
- ✅ `<iframe>` 只能使用 **已批准站点**（如 clublog、hrdlog、youtube、timeanddate、logbook.qrz.com 等）；新站点需联系 QRZ 工作人员审批。

因此，Page 美化应尽量使用**内联样式 + 合法标签**，不要依赖 JavaScript 或事件属性。

---

## 5. BI7KHI Page 美化迭代示例

本次以 [BI7KHI](https://www.qrz.com/db/BI7KHI) 为例，基于原有中英双语内容进行“迭代美化”：

### 5.1 原有状态

原页面已经有比较清晰的内容，但排版以普通段落 + 简单色块为主：

![BI7KHI 原 Page](/ham-tools/qrz/qrz-bi7khi-db.png)

### 5.2 新版改进点

改进后的 HTML 参考文件：`ham-tools/qrz/bi7khi-page-new.html`（可复制到编辑器复用）。

主要改动：

- 添加 **Hero 横幅**：呼号大字 + 呼号解释 + 社团/身份标签；
- 将个人基础信息改为**卡片网格**，视觉更清晰；
- 无线电设备清单改为**浅色卡片 + 徽章标签**（ARISS / Satellite / VHF/UHF 等）；
- QSL 政策使用**引用块样式**突出重要信息；
- 联系信息保留原链接，统一蓝色链接样式；
- 中英双语结构保留，中间以分隔线过渡；
- 保留 QRZ 允许的 FlagCounter 计数器；
- 全部使用**内联样式**，未使用 JavaScript/事件属性，符合内容规则。

### 5.3 最终效果

保存后公开页显示效果：

![BI7KHI 美化后 Page](/ham-tools/qrz/qrz-bi7khi-db-final.png)

---

## 6. 编辑 Page 的通用流程总结

```
登录 QRZ
  └─ 打开 https://www.qrz.com/db/<CALLSIGN>
       └─ 点击 Edit <CALLSIGN>
            └─ Callsign Update Manager
                 ├─ Add or edit your biography text, fonts, etc.
                 │    └─ CKEditor → 点 Source → 编辑 HTML → 再点 Source → Save
                 └─ Expert options including CSS styles
                      └─ 编辑 CSS → Save
                            └─ 刷新 https://www.qrz.com/db/<CALLSIGN> 查看效果
```

**小贴士：**

- 编辑前可以先复制一份当前 HTML 备份（页面也保留了历史版本，`get previous version...` 可回滚）；
- 修改后刷新公开页通常立即生效；
- 如果不想影响公开页，可以先编辑再观察，确认无误后再保存；
- 所有美化尽量在 **HTML Source + 内联样式** 中完成，避免被规则拦截。

---

## 7. 相关链接

| 资源 | 链接 |
|------|------|
| QRZ 首页 | https://www.qrz.com/ |
| QRZ 登录 | https://www.qrz.com/login |
| QRZ 注册 | https://ssl.qrz.com/reg |
| BI7KHI 页面 | https://www.qrz.com/db/BI7KHI |
| 图片上传 / 页面教程 | https://www.qrz.com/page/pictures.html |
| QRZ 内容规则（编辑页内） | `content rules [+]` |

---

*本教程由 GDUT HAM Wiki 编辑整理，适用于社团成员快速上手 QRZ Page 维护。*
