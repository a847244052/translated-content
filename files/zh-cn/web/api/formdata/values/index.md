---
title: FormData.values()
slug: Web/API/FormData/values
---
<p>{{APIRef("XMLHttpRequest")}}</p>

<p><code><strong>FormData.values()</strong></code> 方法返回一个允许遍历该对象中所有值的 {{jsxref("Iteration_protocols",'迭代器')}} 。这些值是 {{domxref("USVString")}} 或是{{domxref("Blob")}} 对象。</p>

<div class="note">
<p><strong>注意：</strong> 此方法在 <a href="/en-US/docs/Web/API/Web_Workers_API">Web Workers</a> 中可用</p>
</div>

<h2 id="语法">语法</h2>

<pre class="syntaxbox">formData.values();</pre>

<h3 id="返回值">返回值</h3>

<p>返回一个{{jsxref("Iteration_protocols","迭代器")}}.</p>

<h2 id="示例">示例</h2>

<pre class="brush: js; highlight:[7]">//创建一个 FormData 测试对象
var formData = new FormData();
formData.append('key1', 'value1');
formData.append('key2', 'value2');

//显示值
for (var value of formData.values()) {
   console.log(value);
}
</pre>

<p>结果为：</p>

<pre>value1
value2</pre>

<h2 id="规范">规范</h2>

{{Specifications}}

<h2 id="浏览器兼容性">浏览器兼容性</h2>

{{Compat("api.FormData.values")}}

<h2 id="相关链接">相关链接</h2>

<ul>
 <li>{{domxref("XMLHTTPRequest")}}</li>
 <li><a href="/en-US/docs/DOM/XMLHttpRequest/Using_XMLHttpRequest">Using XMLHttpRequest</a></li>
 <li><a href="/en-US/docs/DOM/XMLHttpRequest/FormData/Using_FormData_Objects">Using FormData objects</a></li>
 <li>{{HTMLElement("Form")}}</li>
</ul>