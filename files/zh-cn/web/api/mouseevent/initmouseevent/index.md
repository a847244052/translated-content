---
title: MouseEvent.initMouseEvent()
slug: Web/API/MouseEvent/initMouseEvent
---
<p>{{APIRef("DOM Events")}}{{deprecated_header}}</p>

<p><code><strong>MouseEvent.initMouseEvent()</strong></code> 方法用以在鼠标事件创建时 (一般用 {{domxref("Document.createEvent()")}}方法创建) 初始化其属性的值。</p>

<p>事件初始化是在事件被{{ domxref("Document.createEvent()") }}方法创建后必需的。这个方法必须在事件被{{ domxref("EventTarget.dispatchEvent()") }}方法发送出来前调用。一旦事件被发送后，它将不再起任何作用。 </p>

<div class="note">
<p><strong>不要再用此方法，已过时。</strong></p>

<p>使用特定的事件构造器来替代它，像 {{domxref("MouseEvent.MouseEvent", "MouseEvent()")}}。<a href="/en-US/docs/Web/Guide/Events/Creating_and_triggering_events">创建并发送事件</a> 页面里有更多的使用信息。</p>
</div>

<h2 id="Syntax">语法</h2>

<pre class="syntaxbox"><em>event</em>.initMouseEvent(<em>type</em>, <em>canBubble</em>, <em>cancelable</em>, <em>view</em>,
<em>                     detail</em>, <em>screenX</em>, <em>screenY</em>, <em>clientX</em>, <em>clientY</em>,
<em>                     ctrlKey</em>, <em>altKey</em>, <em>shiftKey</em>, <em>metaKey</em>,
<em>                     button</em>, <em>relatedTarget</em>);</pre>

<h3 id="形参">形参</h3>

<dl>
 <dt><em><code>type</code></em></dt>
 <dd>设置事件类型{{domxref("Event.type", "type")}} 的字符串，包含以下几种鼠标事件：<code>click，</code><code>mousedown</code>，<code>mouseup</code>，<code>mouseover</code>，<code>mousemove</code>，<code>mouseout</code>。</dd>
 <dt><em><code>canBubble</code></em></dt>
 <dd>是否可以冒泡。取值集合见{{domxref("Event.bubbles")}}。</dd>
 <dt><em><code>cancelable</code></em></dt>
 <dd>是否可以阻止事件默认行为。取值集合见{{domxref("Event.cancelable")}}。</dd>
 <dt><em><code>view</code></em></dt>
 <dd>事件的 AbstractView 对象引用，这里其实指向{{domxref("window")}} 对象。取值集合见 {{domxref("UIEvent.view")}}。</dd>
 <dt><em><code>detail</code></em></dt>
 <dd>事件的鼠标点击数量。取值集合见{{domxref("Event.detail")}}。</dd>
 <dt><em><code>screenX</code></em></dt>
 <dd>事件的屏幕的 x 坐标。取值集合见{{domxref("MouseEvent.screenX")}}。</dd>
 <dt><em><code>screenY</code></em></dt>
 <dd>事件的屏幕的 y 坐标。取值集合见{{domxref("MouseEvent.screenY")}}。</dd>
 <dt><em><code>clientX</code></em></dt>
 <dd>事件的客户端 x 坐标。取值集合见{{domxref("MouseEvent.clientX")}}。</dd>
 <dt><em><code>clientY</code></em></dt>
 <dd>事件的客户端 y 坐标。取值集合见{{domxref("MouseEvent.clientY")}}。</dd>
 <dt><em><code>ctrlKey</code></em></dt>
 <dd>事件发生时 <kbd>control</kbd> 键是否被按下。取值集合见{{domxref("MouseEvent.ctrlKey")}}。</dd>
 <dt><em><code>altKey</code></em></dt>
 <dd>事件发生时 <kbd>alt</kbd> 键是否被按下。取值集合见{{domxref("MouseEvent.altKey")}}。</dd>
 <dt><em><code>shiftKey</code></em></dt>
 <dd>事件发生时 <kbd>shift</kbd> 键是否被按下。取值集合见{{domxref("MouseEvent.shiftKey")}}。</dd>
 <dt><em><code>metaKey</code></em></dt>
 <dd>事件发生时 <kbd>meta</kbd> 键是否被按下。取值集合见{{domxref("MouseEvent.metaKey")}}。</dd>
 <dt><em><code>button</code></em></dt>
 <dd>鼠标按键值 {{domxref("MouseEvent.button", "button")}}。</dd>
 <dt><em><code>relatedTarget</code></em></dt>
 <dd>事件的<a href="/en/DOM/event.relatedTarget">相关对象</a>。只在某些事件类型有用 (例如 <code>mouseover</code> ?和 <code>mouseout</code>)。其它的传 null。</dd>
</dl>

<h2 id="Example">示例</h2>

<h3 id="HTML">HTML</h3>

<pre class="brush: html"><code>&lt;div style="background:red;width:180px;padding:10px;"&gt;
 &lt;div id="out"&gt;&lt;/div&gt;
 &lt;input type="text"&gt;
&lt;/div&gt;</code>
</pre>

<h3 id="JavaScript">JavaScript</h3>

<pre class="brush: js"><code>document.body.onclick = function(){
 e = arguments[0];
 var dt = e.target,stag = dt.tagName.toLowerCase();
 </code>document.getElementById("out").innerHTML = stag;<code>
};
var simulateClick = function(){
 var evt = document.createEvent("MouseEvents");
 evt.initMouseEvent("click", true, true, window, 0, 0, 0, 80, 20, false, false, false, false, 0, null);
 document.body.dispatchEvent(evt);
}
simulateClick();//Why it can not show "input" ?</code>
</pre>

<p>这里有个在线演示</p>

<p>{{EmbedLiveSample('Example', 200, 36)}}</p>

<p>{{ LiveSampleLink('Example', 'Link to live demo') }}</p>

<h2 id="规范">规范</h2>

<p>此特性不属于任何规范，也不再有望成为标准。</p>

<p>请使用 {{domxref("MouseEvent.MouseEvent", "MouseEvent()")}} 构造函数代替。</p>

<h2 id="Browser_compatibility">浏览器兼容性</h2>

{{Compat}}

<h2 id="参阅">参阅</h2>

<ul>
 <li>{{domxref("MouseEvent.MouseEvent()","MouseEvent()")}}构造器，更标准的创建{{domxref("MouseEvent")}}对象方法。</li>
 <li>{{domxref("Event.initEvent()")}}可以简单达到相同目的的方法。它已过时不再使用。</li>
</ul>