---
title: Performance.clearMeasures()
slug: Web/API/Performance/clearMeasures
---
<div>{{APIRef("User Timing API")}}</div>

<p><strong><code>clearMeasures()</code></strong> 方法可以从浏览器的性能入口缓存区中移除声明的度量衡。如果这个方法被调用时没有传入参数，则所有 {{domxref("PerformanceEntry.entryType","entry type")}} 标记值为"<code>measure</code>" 的{{domxref("PerformanceEntry","性能实体")}}将被从性能入口缓存区中移除。</p>

<p>{{AvailableInWorkers}}</p>

<h2 id="用法">用法</h2>

<pre class="syntaxbox"><em>performance</em>.clearMeasures();
<em>performance</em>.clearMeasures(name);
</pre>

<h3 id="参数">参数</h3>

<dl>
 <dt>name {{optional_inline}}</dt>
 <dd>用于表述时间戳名称的 {{domxref("DOMString")}}。如果没有提供这个参数，则所有 {{domxref("PerformanceEntry.entryType","entry type")}} 标记值为"<code>measure</code>" 的{{domxref("PerformanceEntry","性能实体")}}将被移除。</dd>
</dl>

<h3 id="返回值">返回值</h3>

<p>无</p>

<h2 id="例子">例子</h2>

<p>下面的两个例子演示了 <code>clearMeasures()</code> 的用法。</p>

<pre class="brush: js">function clear_measure(name) {
  if (performance.clearMeasures === undefined) {
    console.log("performance.clearMeasures Not supported");
    return;
  }
  // 根据给定的 name <code>移除所有标记类型为 "measure" 的性能入口</code>
  performance.clearMeasures(name);
}
function clear_all_measures() {
  if (performance.clearMeasures === undefined) {
    console.log("performance.clearMeasures Not supported");
    return;
  }
  // <code>移除性能缓存区中所有标记类型为 "measure" 的性能入口</code>
  performance.clearMeasures();
}
</pre>

<h2 id="规范">规范</h2>

{{Specifications}}

<h2 id="浏览器兼容性">浏览器兼容性</h2>

{{Compat("api.Performance.clearMeasures")}}