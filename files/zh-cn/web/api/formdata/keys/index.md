---
title: FormData.keys()
slug: Web/API/FormData/keys
---
<p>{{APIRef("XMLHttpRequest")}}</p>

<p><code><strong>FormData.keys()</strong></code> 该方法返回一个迭代器（{{jsxref("Iteration_protocols",'iterator')}}），遍历了该 formData  包含的所有 key，这些 key 是 {{domxref("USVString")}} 对象。</p>

<div class="note">
<p><strong>注意</strong>: 该方法在 <a href="/en-US/docs/Web/API/Web_Workers_API">Web Workers</a> 可用。</p>
</div>

<h2 id="语法">语法</h2>

<pre class="syntaxbox">formData.keys();</pre>

<h3 id="返回值">返回值</h3>

<p>返回一个迭代器（ {{jsxref("Iteration_protocols","iterator")}}）。</p>

<h2 id="示例">示例</h2>

<pre class="brush: js; highlight:[7]">// 先创建一个 FormData 对象
var formData = new FormData();
formData.append('key1', 'value1');
formData.append('key2', 'value2');

// 输出所有的 key
for (var key of formData.keys()) {
   console.log(key);
}
</pre>

<p>结果如下：</p>

<pre>key1
key2</pre>

<h2 id="规范">规范</h2>

{{Specifications}}

<h2 id="浏览器兼容性">浏览器兼容性</h2>

{{Compat("api.FormData.keys")}}

<h2 id="相关链接">相关链接</h2>

<ul>
 <li>{{domxref("XMLHTTPRequest")}}</li>
 <li><a href="/en-US/docs/DOM/XMLHttpRequest/Using_XMLHttpRequest">Using XMLHttpRequest</a></li>
 <li><a href="/en-US/docs/DOM/XMLHttpRequest/FormData/Using_FormData_Objects">Using FormData objects</a></li>
 <li>{{HTMLElement("Form")}}</li>
</ul>