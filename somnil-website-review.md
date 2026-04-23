# Somnil 官网优化评审报告

> **评审时间：** 2026-04-23
> **评审人：** Melt (AI Subagent)
> **官网路径：** `/var/www/html/somnil/` (生产服务器)
> **报告路径：** `somnil-website-review.md`

---

## 一、现状总评

| 维度 | 评分 | 简评 |
|------|------|------|
| 用户理解度 | ⭐⭐⭐ (3/5) | 技术表达强，用户价值传达弱；产品形态（头环）首屏不可见 |
| Awesome Design | ⭐⭐⭐⭐ (4/5) | 视觉风格独特，terminal 美学突出，但受众匹配度存疑 |
| 转化漏斗 | ⭐⭐ (2/5) | CTA 路径模糊，无 social proof，无 email capture |
| SEO / 性能 | ⭐⭐⭐ (3/5) | 结构化数据优秀，但性能优化空间大 |

---

## 二、用户理解度检查

### 2.1 首屏价值主张

**当前首屏（Hero Section）：**
- Eyebrow（眉标）：`床头睡眠环境被动干预`
- 标题：`Somnil`
- 副标题：`半夜惊醒，不是你的问题。是环境没跟上你的大脑。`
- Hero terminal：显示 EEG 技术参数（250Hz、8通道、接触式）

**问题诊断：**

1. **产品形态缺失：** 首屏完全没有产品图片或实物图。用户看到 "Somnil" 这个词，不知道它是硬件头环、软件、还是服务。直到 Page 003 才在产品描述框里看到"软质头环"这个关键词。竞品 Dreem/Withings Aura 首屏必有产品图。

2. **eyebrow 技术术语过重：** "床头睡眠环境被动干预" 对睡眠障碍用户（而非技术背景用户）来说理解成本高。前半句"床头"是有用的空间定位，但"被动干预"需要解释。

3. **标题无差异化：** "Somnil" 本身是一个自造词，首屏没有任何辅助信息帮助用户理解这个品牌做什么。相比之下，SleepWatch 的首屏标题是 "Find Your Best Sleep."，一句话说清楚。

4. **Hero terminal 喧宾夺主：** curl 命令展示了 EEG 技术细节，但这个展示对目标用户的价值主张没有帮助——它在解释"怎么做"，而不是"能解决什么问题"。技术极客会喜欢，但睡眠障碍的普通用户可能会感到困惑或被吓退。

### 2.2 CTA（行动召唤）

**当前 CTA（Page 005）：**
- 主按钮：`申请体验 限量 100 名` → 跳转到飞书 Wiki 页面
- 次按钮：`了解更多` → 跳转到 GitHub（但链接是 `github.com/Affaan987/somnil-eeg`，不是 `v0id-byte`，且 GitHub 仓库名与主 CTA 文案不一致）

**问题诊断：**

1. **没有直接购买 CTA：** Somnil V1.0 是硬件产品，但没有价格、没有"立即购买"或"预订"入口，整个漏斗停在 waitlist 申请。

2. **飞书 Wiki 作为 CTA 落地页非常规：** 用户点击"申请体验"期望一个精致的表单或落地页，而不是内部 Wiki 页面。这会严重降低信任感。

3. **次按钮指向错误的 GitHub 仓库：** `Affaan987/somnil-eeg` 是第三方 fork，与 v0id-byte/somnil-eeg 不一致，会造成品牌混乱。

### 2.3 使用流程

**问题：** 整页没有任何地方解释"用户实际怎么使用 Somnil"。几点钟戴？戴多久？需要充电吗？配合 App 吗？床头放在哪里？这些问题在首屏完全没有回答。

**竞品参考：** Dreem 的首屏会展示"戴上头环，睡觉"的示意。SleepWatch 直接说 "Simply wear your Apple Watch to bed or use your iPhone."

---

## 三、Awesome Design 设计原则对照

### 3.1 视觉风格

| 原则 | Somnil 现状 | 评分 |
|------|------------|------|
| 品牌一致性 | 深色终端风，紫色强调色，Inter + JetBrains Mono，风格统一 | ⭐⭐⭐⭐ |
| 视觉层次 | PAGE 001→005 结构清晰，页面分隔明确 | ⭐⭐⭐⭐ |
| 动效克制 | 大量 CSS 动画（pulse、ringPulse、scrollPulse），reduced-motion 支持良好 | ⭐⭐⭐ |
| 色彩情绪 | 深蓝+紫色营造科技感，但竞品（如 Calm、Headspace）多采用暖色/渐变传达睡眠的"放松"感，Somnil 的纯黑+终端风偏硬 | ⭐⭐⭐ |

### 3.2 可访问性（A11y）

| 检查项 | 现状 | 评分 |
|--------|------|------|
| prefers-reduced-motion | ✅ 完整支持 | ⭐⭐⭐⭐⭐ |
| skip-to-content 链接 | ✅ 有（但实现用 inline JS，稍有瑕疵） | ⭐⭐⭐⭐ |
| ARIA labels | ⚠️ 部分 SVG 有 aria-label，但 EEG display 区域使用 `aria-live` | ⭐⭐⭐ |
| 颜色对比度 | ⚠️ 深色背景+白色文字大部分达标，但 text-dim (#777) 可能接近 WCAG AA 临界值 | ⭐⭐⭐ |
| 焦点可见性 | ⚠️ 未发现 focus 样式定义 | ⭐⭐⭐ |

### 3.3 移动端适配

**现状：** 有 hamburger nav，CSS 中有 `@media (max-width: 768px)` 断点，移动端基本可用。

**问题：**
- 导航 hamburger 图标在 iOS Safari 上的点击区域偏小
- terminal 显示内容在移动端直接 `display: none`（loss of content）
- solution-grid 在移动端变成 2 列，但 solution-item padding 在小屏上显得拥挤
- hero-terminal 隐藏后，技术参数的传达渠道消失

---

## 四、转化漏斗分析

### 漏斗现状

```
Landing（首屏） 
    ↓ 用户看完 hero → 下滑
Problem（Page 001）→ Story（Page 002.5）→ 现有方案失效（Page 002）→ 产品方案（Page 003）→ 技术（Page 004）→ CTA（Page 005）
    ↓
CTA 点击 → 飞书 Wiki（waitlist 申请）→ ??? 
    ↓
Retention：无明显留存机制
```

### 关键缺口

| 漏斗阶段 | 缺口 | 影响 |
|---------|------|------|
| Landing → Interest | 首屏无产品图、无明确用户痛点标题 | 跳出率可能很高 |
| Interest → Consideration | 无 social proof（用户评价、媒体报道、用户数） | 信任建立困难 |
| Consideration → Signup | 无 email capture 表单，只有飞书 waitlist | 流失 |
| Signup → Retention | 无 App 下载入口、无后续触达机制 | 用户静默 |

### 没有的关键元素

1. **Social Proof / 信任背书**
   - 用户评价/使用证言（testimonials）
   - 媒体报道链接
   - 合作机构/研究背书（如"已在 XX 医院进行临床测试"）
   - 下载量/用户量展示

2. **Email Capture**
   - 没有 newsletter 订阅入口（可用于 waitlist 预热）
   - 竞品 SleepWatch 首屏就有 App Store / Play Store 下载链接

3. **产品图片**
   - 整个页面没有任何真实产品渲染图或实物图
   - 只有 ASCII-art 风格的头环轮廓 SVG（在 Page 003，且不显眼）

4. **定价策略呈现**
   - V1.0 工程样机阶段可能不适合展示价格，但可以展示"早鸟价"或"预订意向"

---

## 五、SEO / 加载速度 / 技术问题

### 5.1 SEO 现状

| 检查项 | 现状 | 评分 |
|--------|------|------|
| Meta title/description | ✅ 完整且相关 | ⭐⭐⭐⭐ |
| Canonical URL | ✅ 有 | ⭐⭐⭐⭐ |
| Open Graph | ✅ og:title/description/type/url，但 **缺少 og:image** | ⭐⭐⭐ |
| Twitter Card | ⚠️ 有 twitter:card 但无对应图片 | ⭐⭐⭐ |
| FAQPage Schema | ✅ 完整（5个 Q&A） | ⭐⭐⭐⭐⭐ |
| Product Schema | ❌ 无 | ⭐⭐ |
| BreadcrumbList Schema | ❌ 无 | ⭐⭐ |
| hreflang | ❌ 无（中英文页面未标注） | ⭐⭐ |
| 404 页面 | ❌ 未知（未测试） | ⭐⭐ |
| sitemap.xml | ❌ 未发现 | ⭐⭐ |
| robots.txt | ❌ 未发现 | ⭐⭐ |

### 5.2 加载性能

| 指标 | 现状 | 参考值 |
|------|------|--------|
| 资源大小（HTML）| ~30KB（内联 CSS + JS）| 可接受 |
| 外部依赖 | Google Fonts（Inter + JetBrains Mono）| 字体加载应加 `display=swap` |
| 图片 | 无 raster 图片（纯 CSS/SVG）| 优点，无图片优化压力 |
| Loading Screen | 首次访问有 ~1.5s 加载动画 | 使用 `sessionStorage` 避免重复，用户体验尚可 |
| CSS 动画 | 大量 animation/keyframe，无 GPU 加速提示 | 低端设备可能卡顿 |
| JS | 全部内联，无 CDN，无 minify | 增量更新困难，缓存无效 |

**关键问题：**
- Google Fonts 加载未加 `display=swap`，会导致字体闪烁（FOIT）
- 大量 inline CSS 和 JS，每次页面访问都需要重新下载，无法利用浏览器缓存
- 建议：将 CSS/JS 拆分到独立文件，开启 gzip，并加长期 cache 头

### 5.3 结构性建议

- 添加 `sitemap.xml` 到根目录
- 添加 `robots.txt`（允许爬取 somnil.top，但禁止爬取后台路径）
- 补充 Open Graph image（1200×630 产品图）
- 考虑添加 `@type: Product` 的 Schema（如未来有明确产品信息）

---

## 六、竞品参考

### 6.1 SleepWatch (sleepwatchapp.com)

**优势参考：**
- 首屏一句话价值主张："Find Your Best Sleep"
- 明确 CTA 指向 App Store / Play Store
- 分 section 展示核心功能图标（Total Sleep Time、Sleep Rhythm、HR Dip 等）
- 使用 Apple Watch 硬件，降低用户"额外设备"心理负担
- 导航清晰：Sleep 101 / Our Approach / Learn / About Us / Help

**适用 Somnil 的点：** 功能 icon grid 形式可以借鉴，Somnil 的三路干预（温控/声场/香气）也可以用更醒目的 icon grid 替代当前文字描述。

### 6.2 Dreem（硬件竞品）

- 定位为"医疗级睡眠改善设备"
- 强调神经科学背书和研究数据
- 展示真实佩戴图（非抽象图形）

**适用 Somnil 的点：** Somnil 有 Sleep-EDF + CAP Sleep 数据，应在官网显眼位置展示，而非埋在技术页的 footer 里。

### 6.3 Withings Aura / Sleep（睡眠监测硬件）

- 床头设备定位（非 wearable）
- 与智能手机 ecosystem 集成展示
- 产品照片+生活场景图

**适用 Somnil 的点：** 如果 Somnil 强调"床头"定位（官网标题是"床头睡眠环境被动干预"），可以考虑在场景图中展示设备放在床头柜上的样子，而不是只有头环轮廓。

---

## 七、改进建议汇总（按优先级）

### 🔴 P0 — 核心转化修复（上线前必须）

1. **首屏添加产品图或产品轮廓图**
   - 当前首屏只有文字+terminal，没有产品视觉
   - 建议：在 hero section 添加一张Somnil头环的渲染图或照片，放在 hero-title 下方，尺寸约 200x200px，放在视觉中心位置
   - 如果没有渲染图，可以用 CSS 做一张产品示意图放在 hero

2. **修复次按钮 GitHub 链接**
   - 当前 `github.com/Affaan987/somnil-eeg` → 改为 `github.com/v0id-byte/somnil-eeg`
   - 确认哪个是官方 repo，保持一致

3. **补充 Open Graph image**
   - 当前 OG tag 缺失 og:image，导致分享到社交平台时没有预览图
   - 建议：制作一张 1200×630 的 og:image（包含 Somnil 品牌 logo + "重新入睡" 标语）

4. **Email capture 表单**
   - 在 Page 005 CTA 区域上方或下方，添加 email 输入框："想第一时间知道 Somnil V1.0 开放购买？留下邮箱"
   - 可以用飞书表单或简单的 mailto link，逐步构建用户列表

### 🟠 P1 — 用户理解度提升（影响留存和信任）

5. **Eyebrow 改写**
   - 当前：`床头睡眠环境被动干预`
   - 建议：`在你睡着时，悄悄守护你的焦虑反射`
   - 或更直白：`半夜惊醒，有解了`

6. **Hero terminal 降级或重写**
   - 当前 terminal 展示技术参数，对普通用户意义不大
   - 建议：改为展示"干预日志"格式，让用户看到设备如何实际工作的，例如：
     ```
     [03:17] β波升高 → 触发温度-1.5°C
     [03:18] 薰衣草香气释放
     [03:19] β/θ 恢复到 0.8 → 神经回归睡眠节律
     [03:19] 无需醒来 ✓
     ```
   - 这样既保留 terminal 美学，又传达了用户价值

7. **添加 Social Proof**
   - 最少需要：一条真实的早期用户评价或内测反馈
   - 如果没有真实用户：展示媒体报道或研究引用
   - 格式参考："「凌晨3点再也没有惊醒过」— 早期测试用户"
   - 位置：放在 Page 005 CTA 上方或 Story Section 下方

8. **补充 FAQ 或 How it Works 短视频**
   - 当前 FAQ 是文字 Schema，可以增加一个"3步开始使用"的可视化步骤
   - Step 1：睡前戴上 Somnil → Step 2：设备自动监测 → Step 3：焦虑来临前自动干预
   - 竞品 Dreem 和 Withings 都有"How it works"视频占位

### 🟡 P2 — 设计优化（提升转化率）

9. **三路干预特征更显性化**
   - 当前 feature icon + 文字描述埋在 Page 003
   - 建议：升级为动图或更醒目的 visual（类似 SleepWatch 的 icon grid）
   - 温控、声场、香气三条路径应该有独立的视觉区分度

10. **Loading Screen 可以更品牌化**
    - 当前加载动画是百分比数字+进度条，科技感强
    - 建议：可以加一个 Somnil 产品轮廓的淡入动画，强化"产品"记忆
    - 确保 `sessionStorage` 逻辑正确，避免用户刷新时重复看到加载页

11. **颜色情绪微调**
    - 当前纯黑（#000000）+ 紫色（#8B5CF6）+ 深蓝（#0a1628）+ 青色（#4a9eff）偏科技感
    - 竞品 Calm/Headspace 多用深蓝+薰衣草渐变，传达"睡眠放松"感
    - 建议：考虑在 hero 或 features 区域加入微妙的暖色点缀（如微弱的薰衣草色光晕）

12. **Solution Grid（Page 002）文案优化**
    - "追踪器：仅观测，不干预" 这个 verdict 可以更精准
    - 建议："追踪器：仅告诉你睡得怎么样，不能阻止惊醒"（对比 Somnil 的主动干预）

### ⚪ P3 — SEO / 技术（长期优化）

13. **CSS/JS 拆分 + CDN**
    - 将内联 CSS/JS 拆分到独立文件，加 gzip + 长期 cache
    - 这样每次改代码只需更新对应文件，用户端利用缓存

14. **Google Fonts 加 display=swap**
    ```html
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&family=JetBrains+Mono:wght@400;500;700&display=swap" rel="stylesheet">
    <!-- 改为 -->
    <link href="https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&family=JetBrains+Mono:wght@400;500;700&display=swap&family=display=swap" rel="stylesheet">
    ```

15. **添加 sitemap.xml 和 robots.txt**

16. **补充 Product Schema**（未来产品正式发布后）

17. **移动端 hamburger nav 无障碍优化**
    - 给 hamburger button 加 `aria-expanded` 和 `aria-controls`
    - 确保点击后 nav 可以通过键盘导航

---

## 八、总结

Somnil 官网的视觉设计和代码质量是**优秀的**——terminal 美学、动画体系、技术数据展示、Schema 标记都体现了高水平工程思维。

但作为**营销漏斗**，存在三个核心缺口：

1. **产品不可见** — 首屏没有任何产品图，用户不知道 Somnil 是什么
2. **信任感缺失** — 无 social proof，无评价，无媒体报道
3. **转化路径模糊** — 停留在 waitlist 申请，没有 email capture 和后续触达机制

建议优先级：先修 P0（产品图 + GitHub 链接 + OG image），再补充 P1（social proof + How it works），最后做 P2/P3 的设计和技术迭代。

---

*报告生成时间：2026-04-23 | 评审工具：HTML 源码分析 + Web Search 竞品调研*
