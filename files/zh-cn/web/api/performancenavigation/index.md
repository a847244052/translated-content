---
title: PerformanceNavigation
slug: Web/API/PerformanceNavigation
---
<p>{{APIRef("Navigation Timing")}}</p>

<h2 id="Summary">Summary</h2>

<p><strong><code>PerformanceNavigation</code></strong><code>接口呈现了如何导航到当前文档的信息。</code></p>

<p>这个类型的对象可以被只读属性{{domxref("Performance.navigation")}}调用。</p>

<h2 id="Properties">Properties</h2>

<p><em><code>PerformanceNavigation</code> 接口不继承任何属性。</em></p>

<dl>
 <dt>{{domxref("PerformanceNavigation.type")}} {{readonlyInline}}</dt>
 <dd>一个无符号短整型，表示是如何导航到这个页面的。可能的值如下：
 <dl>
  <dt><code>TYPE_NAVIGATE</code> (0)</dt>
  <dd>当前页面是通过点击链接，书签和表单提交，或者脚本操作，或者在 url 中直接输入地址，type 值为 0</dd>
  <dt><code>TYPE_RELOAD</code> (1)</dt>
  <dd>点击刷新页面按钮或者通过{{domxref("Location.reload()")}}方法显示的页面，type 值为 1</dd>
  <dt><code>TYPE_BACK_FORWARD</code> (2)</dt>
  <dd>页面通过历史记录和前进后退访问时。type 值为 2</dd>
  <dt><code>TYPE_RESERVED</code> (255)</dt>
  <dd>任何其他方式，type 值为 255</dd>
 </dl>
 </dd>
 <dt>{{domxref("PerformanceNavigation.redirectCount")}} {{readonlyInline}}</dt>
 <dd>无符号短整型，表示在到达这个页面之前重定向了多少次。</dd>
</dl>

<h2 id="Methods">Methods</h2>

<p><em><em><code>Performance</code> 接口没有继承任何方法</em></em></p>

<dl>
 <dt>{{domxref("PerformanceNavigation.toJSON()")}} {{non-standard_inline}}</dt>
 <dd>把<code>PerformanceNavigation</code>转换成 JSON 对象</dd>
</dl>

<h2 id="规范">规范</h2>

<p>因为 <a href="https://w3c.github.io/navigation-timing/#obsolete">Navigation Timing 规范</a>已被弃用，此特性不再有望成为标准。请使用 {{domxref("PerformanceNavigationTiming")}} 接口代替。</p>

<h2 id="浏览器兼容性">浏览器兼容性</h2>

{{Compat}}

<h2 id="See_also">See also</h2>

<ul>
 <li>The {{domxref("Performance")}} that allows access to an object of this type.</li>
 <li>{{domxref("PerformanceNavigationTiming")}} (part of Navigation Timing Level 2) {{experimental_inline}}</li>
</ul>