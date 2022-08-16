---
title: Performance.toJSON()
slug: Web/API/Performance/toJSON
---
<div>{{APIRef("High Resolution Timing")}}</div>

<div>{{domxref("Performance")}} 的 <strong><code>toJSON() 方法是一个标准的串行器：它返回一个由 performance 对象各个属性组成的 JSON</code></strong></div>

<h2 id="Syntax">Syntax</h2>

<pre class="syntaxbox">myPerf = performance.toJSON()
</pre>

<h3 id="Arguments">Arguments</h3>

<p>无</p>

<h3 id="Return_value">Return value</h3>

<dl>
 <dt>myPerf</dt>
 <dd>{{domxref("Performance")}} 对象序列化之后转化成的 JSON 对象。</dd>
</dl>

<h2 id="Example">Example</h2>

<pre class="brush: js">var js;
js = window.performance.toJSON();
console.log("json = " + JSON.stringify(js));
</pre>

<h2 id="Specifications">Specifications</h2>

{{Specifications}}

<h2 id="Browser_compatibility">Browser compatibility</h2>

<div>
<div>


<p>{{Compat("api.Performance.toJSON")}}</p>
</div>
</div>