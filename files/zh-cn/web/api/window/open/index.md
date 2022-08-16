---
title: Window.open()
slug: Web/API/Window/open
---
<div>{{APIRef}}</div>

<p><code>Window</code> 接口的 <strong><code>open()</code></strong> 方法，是用指定的名称将指定的资源加载到浏览器上下文（窗口 <code>window</code> ，内嵌框架 <code>iframe</code> 或者标签 <code>tab</code> ）。如果没有指定名称，则一个新的窗口会被打开并且指定的资源会被加载进这个窗口的浏览器上下文中。</p>

<h2 id="Syntax">语法</h2>

<pre class="syntaxbox" style="font-size: 14px; white-space: normal;"><code>
</code>let <var>windowObjectReference</var> = window.open(<var>strUrl</var>, <var>strWindowName</var>, [<var>strWindowFeatures</var>]);</pre>

<div class="note">
<p><var>strUrl === </var>要在新打开的窗口中加载的 URL。</p>

<p><var>strWindowName === </var>新窗口的名称。</p>

<p><var>strWindowFeatures === </var>一个可选参数，列出新窗口的特征 (大小，位置，滚动条等) 作为一个{{domxref("DOMString")}}。</p>
</div>

<p></p>

<h2 id=".E5.8F.82.E6.95.B0.E4.B8.8E.E8.BF.94.E5.9B.9E.E5.80.BC">参数与返回值</h2>

<dl>
 <dt><code>WindowObjectReference</code></dt>
 <dd>打开的新窗口对象的引用。如果调用失败，返回值会是 <code>null 。如果</code>父子窗口满足“<a href="/cn/JavaScript%E7%9A%84%E5%90%8C%E6%BA%90%E7%AD%96%E7%95%A5">同源策略</a>”，你可以通过这个引用访问新窗口的属性或方法。</dd>
</dl>

<dl>
 <dt><code>strUrl</code></dt>
 <dd>新窗口需要载入的 url 地址。<var>strUrl</var>可以是 web 上的 html 页面也可以是图片文件或者其他任何浏览器支持的文件格式。</dd>
</dl>

<dl>
 <dt><code>strWindowName</code></dt>
 <dd>新窗口的名称。该字符串可以用来作为超链接 {{HTMLElement("a")}} 或表单 {{HTMLElement("form")}} 元素的目标属性值。字符串中不能含有空白字符。注意：<var>strWindowName</var> 并不是新窗口的标题。</dd>
</dl>

<dl>
 <dt><code>strWindowFeatures</code></dt>
 <dd>可选参数。是一个字符串值，这个值列出了将要打开的窗口的一些特性 (窗口功能和工具栏) 。 字符串中不能包含任何空白字符，特性之间用逗号分隔开。参考下文的<a href="#Position and size features">位置和尺寸特征</a>。</dd>
</dl>

<h2 id=".E8.AF.B4.E6.98.8E">说明</h2>

<p><code>open()</code> 方法，创建一个新的浏览器窗口对象，如同使用文件菜单中的新窗口命令一样。<var>strUrl</var> 参数指定了该窗口将会打开的地址。如果<var>strUrl</var> 是一个空值，那么打开的窗口将会是带有默认工具栏的空白窗口（加载<code>about:blank</code>）。</p>

<p>注意：调用<code>window.open()</code>方法以后，远程 URL 不会被立即载入，载入过程是异步的。（实际加载这个 URL 的时间推迟到当前脚本块执行结束之后。窗口的创建和相关资源的加载异步地进行。）</p>

<h2 id=".E4.BE.8B.E5.AD.90">例子</h2>

<pre><code>let windowObjectReference;
let strWindowFeatures = `
    menubar=yes,
    location=yes,
    resizable=yes,
    scrollbars=yes,
    status=yes
`;

function openRequestedPopup() {
    windowObjectReference =
    window.open(
        "http://www.cnn.com/",
        "CNN_WindowName",
        strWindowFeatures
    );
}</code></pre>

<pre>let WindowObjectReference;

const openRequestedPopup = () =&gt; {
    windowObjectReference = window.open(
        "https://www.domainname.ext/path/ImageFile.png",
        "DescriptiveWindowName",
        "resizable,scrollbars,status"
    );
}
</pre>

<p>如果已经存在以 <var>strWindowName</var> 为名称的窗口，则不再打开一个新窗口，而是把 <var>strUrl</var> 加载到这个窗口中。在这种情况下，方法的返回值是这个已经打开的窗口，并忽略参数 <var>strWindowFeatures</var> 。<em>strUrl</em>设为空字符串时，可以在不改变窗口地址的情况下获得一个已经打开的同名窗口的引用。如果要在每次调用 <code>window.open()</code>时都打开一个新窗口，则要把参数 <var>strWindowName</var> 设置为 <code>_blank</code>。</p>

<p><var>strWindowFeatures</var> 是一个可选的字符串，包含了新窗口的一组用逗号分割的特性，在窗口打开之后，就不能用 JavaScript 改变窗口的功能和工具栏的设置。如果名称是 <var>strWindowName</var> 的窗口不存在并且又没有提供 <var>strWindowFeatures</var> 参数（或者 <var>strWindowFeatures</var> 参数为空字符串），则子窗口以父窗口默认的工具栏渲染。</p>

<p>如果 <var>strWindowFeatures</var> 参数中没有定义窗口大小，则新窗口的尺寸跟最近渲染的窗口尺寸一样。</p>

<p>如果 <var>strWindowFeatures</var> 参数中没有定义窗口位置，则新窗口显示在最近渲染的窗口的坐标偏移 22 个像素的位置。这种新窗口偏移量的做法被浏览器开发商广泛地实现（MSIE 6 SP2 在默认主题下的偏移量是 29 个像素），目的是提醒用户注意有新的窗口打开。如果最近使用的窗口是最大化的，则没有这 22 像素的偏移，新（子）窗口也会被最大化。</p>

<p><strong>如果你定义了 <var>strWindowFeatures</var> 参数，那么没有在这个字符串中列出的特性会被禁用或移除</strong> （除了 <var>titlebar</var> 和 <var>close</var> 默认设置为 yes）</p>

<div class="note">
<p><strong>提示</strong>: 如果你使用了 <var>strWindowFeatures</var> 参数，那么只需要列出新窗口中启用的特性，其它的特性（除了<em>titlebar</em>和<em>close</em>）将被禁用或移除。</p>
</div>

<p><img alt="Firefox Chrome Toolbars Illustration" src="https://developer.mozilla.org/@api/deki/files/210/=FirefoxChromeToolbarsDescription7a.gif" style="border: 1px dotted green;"></p>

<h2 id="Position_and_size_features"><a id="Position and size features" name="Position and size features">位置尺寸特征</a></h2>

<h3 id="Position_and_size_features"></h3>

<p><a href="#Note_on_position_and_dimension_error_correction">Note on position and dimension error correction</a></p>

<p>{{bug(176320)}}</p>

<p><a href="#Note_on_precedence">Note on precedence</a></p>

<dl>
 <dt>left</dt>
 <dd>Specifies the distance the new window is placed from the left side of the work area for applications of the user's operating system to the leftmost border (resizing handle) of the browser window. The new window can not be initially positioned offscreen.</dd>
 <dt>top</dt>
 <dd>Specifies the distance the new window is placed from the top side of the work area for applications of the user's operating system to the topmost border (resizing handle) of the browser window. The new window can not be initially positioned offscreen.</dd>
 <dt>height</dt>
 <dd>Specifies the height of the content area, viewing area of the new secondary window in pixels. The height value includes the height of the horizontal scrollbar if present. The minimum required value is 100.<br>
 <a href="#Note_on_outerHeight_versus_height">Note on outerHeight versus height (or innerHeight)</a></dd>
 <dt>width</dt>
 <dd>Specifies the width of the content area, viewing area of the new secondary window in pixels. The width value includes the width of the vertical scrollbar if present. The width value does not include the sidebar if it is expanded. The minimum required value is 100.</dd>
 <dt>screenX</dt>
 <dd>Deprecated. Same as <a href="#left">left</a> but only supported by Netscape and Mozilla-based browsers.</dd>
 <dt>screenY</dt>
 <dd>Deprecated. Same as <a href="#top">top</a> but only supported by Netscape and Mozilla-based browsers.</dd>
 <dt>centerscreen</dt>
 <dd>Centers the window in relation to its parent's size and position. Requires chrome=yes.</dd>
 <dt>outerHeight</dt>
 <dd>Specifies the height of the whole browser window in pixels. This outerHeight value includes any/all present toolbar, window horizontal scrollbar (if present) and top and bottom window resizing borders. Minimal required value is 100.<br>
 <strong>Note</strong>: since titlebar is always rendered, then requesting outerHeight=100 will make the innerHeight of the browser window under the minimal 100 pixels.<br>
 <a href="#note_on_outerheight_versus_height">Note on outerHeight versus height (or innerHeight)</a></dd>
 <dt>outerWidth</dt>
 <dd>Specifies the width of the whole browser window in pixels. This outerWidth value includes the window vertical scrollbar (if present) and left and right window resizing borders.</dd>
 <dt>innerHeight</dt>
 <dd>Same as <a href="#height">height</a> but only supported by Netscape and Mozilla-based browsers. Specifies the height of the content area, viewing area of the new secondary window in pixels. The <var>innerHeight</var> value includes the height of the horizontal scrollbar if present. Minimal required value is 100.<br>
 <a href="#Note_on_outerHeight_versus_height">Note on outerHeight versus height (or innerHeight)</a></dd>
 <dt>innerWidth</dt>
 <dd>Same as <a href="#width">width</a> but only supported by Netscape and Mozilla-based browsers. Specifies the width of the content area, viewing area of the new secondary window in pixels. The innerWidth value includes the width of the vertical scrollbar if present. The innerWidth value does not include the sidebar if it is expanded. Minimal required value is 100.</dd>
</dl>

<h3 id="Toolbar_and_chrome_features">Toolbar and chrome features</h3>

<dl>
 <dt>NOTE: All features can be set to yes, 1 or just be present to be "on", set to <em>no</em> or<em> 0 </em>or in most cases just not present to be "off"</dt>
 <dd>example "status=yes", "status=1" and "status" have identical results</dd>
 <dt>menubar</dt>
 <dd>If this feature is on, then the new secondary window renders the menubar.<br>
 Mozilla and Firefox users can force new windows to always render the menubar by setting <code>dom.disable_window_open_feature.menubar</code> to <var>true</var> in <a href="http://support.mozilla.com/en-US/kb/Editing+configuration+files#about_config">about:config</a> or in their <a href="http://support.mozilla.com/en-US/kb/Editing+configuration+files#user_js">user.js file</a>.</dd>
 <dt>toolbar</dt>
 <dd>If this feature is on, then the new secondary window renders the Navigation Toolbar (Back, Forward, Reload, Stop buttons). In addition to the Navigation Toolbar, Mozilla-based browsers will render the Tab Bar if it is visible, present in the parent window. (If this feature is set to <var>no</var> all toolbars in the window will be invisible, for example extension toolbars).<br>
 Mozilla and Firefox users can force new windows to always render the Navigation Toolbar by setting <code>dom.disable_window_open_feature.toolbar</code> to <var>true</var> in <a href="http://support.mozilla.com/en-US/kb/Editing+configuration+files#about_config">about:config</a> or in their <a href="http://support.mozilla.com/en-US/kb/Editing+configuration+files#user_js">user.js file</a>.</dd>
 <dt>location</dt>
 <dd>If this feature is on, then the new secondary window renders the Location bar in Mozilla-based browsers. MSIE 5+ and Opera 7.x renders the Address Bar.<br>
 Mozilla and Firefox users can force new windows to always render the location bar by setting <code>dom.disable_window_open_feature.location</code> to <var>true</var> in <a href="http://support.mozilla.com/en-US/kb/Editing+configuration+files#about_config">about:config</a> or in their <a href="http://support.mozilla.com/en-US/kb/Editing+configuration+files#user_js">user.js file</a>. {{Fx_minversion_note(3, "In Firefox 3, <code>dom.disable_window_open_feature.location</code> now defaults to <var>true</var>, forcing the presence of the Location Bar much like in IE7. See bug 337344 for more information.")}}</dd>
 <dt>personalbar</dt>
 <dd>If this feature is on, then the new secondary window renders the Personal Toolbar in Netscape 6.x, Netscape 7.x and Mozilla browser. It renders the Bookmarks Toolbar in Firefox. In addition to the Personal Toolbar, Mozilla browser will render the Site Navigation Bar if such toolbar is visible, present in the parent window.<br>
 Mozilla and Firefox users can force new windows to always render the Personal Toolbar/Bookmarks toolbar by setting <code>dom.disable_window_open_feature.personalbar</code> to <var>true</var> in <a href="http://support.mozilla.com/en-US/kb/Editing+configuration+files#about_config">about:config</a> or in their <a href="http://support.mozilla.com/en-US/kb/Editing+configuration+files#user_js">user.js file</a>.</dd>
 <dt>directories {{Deprecated_Inline}}</dt>
 <dd>Obsolete synonym of personalbar. In IE, it rendered the Links bar. Supported in Gecko up to 1.9.2 and in IE up to 6.</dd>
 <dt>status</dt>
 <dd>If this feature is on, then the new secondary window has a status bar. Users can force the rendering of status bar in all Mozilla-based browsers, in MSIE 6 SP2 (<a href="#Note_on_security_issues_of_the_status_bar_presence">Note on status bar in XP SP2</a>) and in Opera 6+. The default preference setting in recent Mozilla-based browser releases and in Firefox 1.0 is to force the presence of the status bar.<br>
 <a href="#Note_on_status_bar">Note on status bar</a></dd>
</dl>

<h3 id="Window_functionality_features">Window functionality features</h3>

<dl>
 <dt>attention {{NonStandardBadge}}</dt>
 <dd>If this feature is specified, the window is able to open even if another application is already in the foreground. This feature is for Firefox OS applications only, and is currently restricted to certified applications. See {{SectionOnPage("/en-US/docs/Archive/B2G_OS/Firefox_OS_apps/App_permissions", "Internal (Certified) app permissions")}} for more information.</dd>
 <dt>dependent</dt>
 <dd>If on, the new window is said to be dependent of its parent window. A dependent window closes when its parent window closes. A dependent window is minimized on the Windows task bar only when its parent window is minimized. On Windows platforms, a dependent window does not show on the task bar. A dependent window also stays in front of the parent window.<br>
 Dependent windows are not implemented on MacOS X, this option will be ignored.<br>
 The dependent feature is currently under revision to be removed ({{Bug(214867)}})<br>
 In MSIE 6, the nearest equivalent to this feature is the <code>showModelessDialog()</code> method.</dd>
 <dt>dialog</dt>
 <dd><a href="https://developer.mozilla.org/@api/deki/files/268/=MenuSystemCommands.png"><img alt="MenuSystemCommands.png" class="internal lwrap" src="https://developer.mozilla.org/@api/deki/files/268/=MenuSystemCommands.png?size=webview" style="float: left; height: 170px; width: 170px;"></a>The <code>dialog</code> feature removes all icons (restore, minimize, maximize) from the window's titlebar, leaving only the close button. Mozilla 1.2+ and Netscape 7.1 will render the other menu system commands (in FF 1.0 and in NS 7.0x, the command system menu is not identified with the Firefox/NS 7.0x icon on the left end of the titlebar: that's probably a bug. You can access the command system menu with a right-click on the titlebar). Dialog windows are windows which have no minimize system command icon and no maximize/restore down system command icon on the titlebar nor in correspondent menu item in the command system menu. They are said to be dialog because their normal, usual purpose is to only notify info and to be dismissed, closed. On Mac systems, dialog windows have a different window border and they may get turned into a sheet.</dd>
 <dt>minimizable</dt>
 <dd>This setting can only apply to dialog windows; "minimizable" requires <code>dialog=yes</code>. If <code>minimizable</code> is on, the new dialog window will have a minimize system command icon in the titlebar and it will be minimizable. Any non-dialog window is always minimizable and <code>minimizable=no</code> will be ignored.</dd>
 <dt>fullscreen</dt>
 <dd>Do not use. Not implemented in Mozilla. There are no plans to implement this feature in Mozilla.<br>
 This feature no longer works in MSIE 6 SP2 the way it worked in MSIE 5.x. The Windows taskbar, as well as the titlebar and the status bar of the window are not visible, nor accessible when fullscreen is enabled in MSIE 5.x.<br>
 <code>fullscreen</code> always upsets users with large monitor screen or with dual monitor screen. Forcing <code>fullscreen</code> onto other users is also extremely unpopular and is considered an outright rude attempt to impose web author's viewing preferences onto users.<br>
 <a href="#Note_on_fullscreen">Note on fullscreen</a><br>
 <code>fullscreen</code> does not really work in MSIE 6 SP2.</dd>
 <dt>resizable</dt>
 <dd>If this feature is on, the new secondary window will be resizable.<br>
 <strong>Note</strong>: Starting with version 1.4, Mozilla-based browsers have a window resizing grippy at the right end of the status bar, this ensures that users can resize the browser window even if the web author requested this secondary window to be non-resizable. In such case, the maximize/restore icon in the window's titlebar will be disabled and the window's borders won't allow resizing but the window will still be resizable via that grippy in the status bar.
 <p>Starting with Firefox 3, secondary windows are always resizable ({{Bug(177838)}})</p>

 <div class="note">
 <p>For accessibility reasons, it is strongly recommended to set this feature always on</p>
 </div>
 <dd>Mozilla and Firefox users can force new windows to be easily resizable by setting<br>
 <code>dom.disable_window_open_feature.resizable</code><br>
 to <var>true</var> in <a href="http://support.mozilla.com/en-US/kb/Editing+configuration+files#about_config">about:config</a> or in their <a href="http://support.mozilla.com/en-US/kb/Editing+configuration+files#user_js">user.js file</a>.</dd>
 <dt>scrollbars</dt>
 <dd>If this feature is on, the new secondary window will show horizontal and/or vertical scrollbar(s) if the document doesn't fit into the window's viewport.
 <div class="note">
 <p><strong>Tip</strong>: For accessibility reasons, it is strongly encouraged to set this feature always on.</p>
 </div>
 Mozilla and Firefox users can force this option to be always enabled for new windows by setting<br>
 <code>dom.disable_window_open_feature.scrollbars</code><br>
 to <var>true</var> in <a href="http://support.mozilla.com/en-US/kb/Editing+configuration+files#about_config">about:config</a> or in their <a href="http://support.mozilla.com/en-US/kb/Editing+configuration+files#user_js">user.js file</a>.<br>
 <a href="#Note_on_scrollbars">Note on scrollbars</a></dd>
</dl>

<h3 id="Features_requiring_privileges">Features requiring privileges</h3>

<p>The following features require the <code>UniversalBrowserWrite</code> privilege, otherwise they will be ignored. Chrome scripts have this privilege automatically, others have to request it from the PrivilegeManager.</p>

<dl>
 <dt>chrome</dt>
 <dd><strong>Note</strong>: Starting with Mozilla 1.7/Firefox 0.9, this feature requires the <code>UniversalBrowserWrite</code> privilege ({{Bug(244965)}}). Without this privilege, it is ignored.<br>
 If on, the page is loaded as window's only content, without any of the browser's interface elements. There will be no context menu defined by default and none of the standard keyboard shortcuts will work. The page is supposed to provide a user interface of its own, usually this feature is used to open XUL documents (standard dialogs like the JavaScript Console are opened this way).</dd>
 <dt>modal</dt>
 <dd><strong>Note</strong>: Starting with Mozilla 1.2.1, this feature requires the <code>UniversalBrowserWrite</code> privilege ({{Bug(180048)}}). Without this privilege, it is ignored.<br>
 If on, the new window is said to be modal. The user cannot return to the main window until the modal window is closed. A typical modal window is created by the <a href="https://developer.mozilla.org/en-US/docs/DOM/window.alert">alert() function</a>.<br>
 The exact behavior of modal windows depends on the platform and on the Mozilla release version.
 <div class="note">
 <p><strong>Note:</strong> As of {{Gecko("1.9")}}, the Internet Explorer equivalent to this feature is the {{domxref("window.showModalDialog()")}} method. For compatibility reasons, it's now supported in Firefox. Note also that starting in {{Gecko("2.0")}}, you can use {{domxref("window.showModalDialog()")}} without UniversalBrowserWrite privileges.</p>
 </div>
 </dd>
 <dt>titlebar</dt>
 <dd>By default, all new secondary windows have a titlebar. If set to <var>no or 0</var>, this feature removes the titlebar from the new secondary window.<br>
 Mozilla and Firefox users can force new windows to always render the titlebar by setting<br>
 <code>dom.disable_window_open_feature.titlebar</code><br>
 to <var>true</var> in <a href="http://support.mozilla.com/en-US/kb/Editing+configuration+files#about_config">about:config</a> or in their <a href="http://support.mozilla.com/en-US/kb/Editing+configuration+files#user_js">user.js file</a>.</dd>
 <dt>alwaysRaised</dt>
 <dd>If on, the new window will always be displayed on top of other browser windows, regardless of whether it is active or not.</dd>
 <dt>alwaysLowered</dt>
 <dd>If on, the new created window floats below, under its own parent when the parent window is not minimized. alwaysLowered windows are often referred as pop-under windows. The alwaysLowered window can not be on top of the parent but the parent window can be minimized. In NS 6.x, the alwaysLowered window has no minimize system command icon and no restore/maximize system command.</dd>
 <dt>z-lock</dt>
 <dd>Same as <code>alwaysLowered</code>.</dd>
 <dt>close</dt>
 <dd>When set to <var>no or 0</var>, this feature removes the system close command icon and system close menu item. It will only work for dialog windows (<code>dialog</code> feature set). <code>close=no</code> will override <code>minimizable=yes</code>.<br>
 Mozilla and Firefox users can force new windows to always have a close button by setting<br>
 <code>dom.disable_window_open_feature.close</code><br>
 to <var>true</var> in <a href="http://support.mozilla.com/en-US/kb/Editing+configuration+files#about_config">about:config</a> or in their <a href="http://support.mozilla.com/en-US/kb/Editing+configuration+files#user_js">user.js file</a>.</dd>
</dl>

<p>The position and size feature elements require a number to be set. The toolbars and window functionalities can be set with a <var>yes</var> or <var>no</var>; you can use <var>1</var> instead of <var>yes</var> and <var>0</var> instead of <var>no</var>. The toolbar and functionality feature elements also accept the shorthand form: you can turn a feature on by simply listing the feature name in the <var>features</var> string. If you supply the <var>features</var> parameter, then the <code>titlebar</code> and <code>close</code> are still <var>yes</var> by default, but the other features which have a <var>yes</var>/<var>no</var> choice will be <var>no</var> by default and will be turned off.</p>

<p>Example:</p>

<pre class="brush:js  language-js"><code class="language-js">var windowObjectReference; // global variable

function openRequestedPopup() {
  windowObjectReference = window.open(
    "http://www.domainname.ext/path/ImgFile.png",
    "DescriptiveWindowName",
    "width=420,height=230,resizable,scrollbars=yes,status=1"
  );
}</code></pre>

<p>In this example, the window will be resizable, it will render scrollbar(s) if needed, if the content overflows requested window dimensions and it will render the status bar. It will not render the menubar nor the location bar. Since the author knew about the size of the image (400 pixels wide and 200 pixels high), he added the margins applied to the root element in MSIE 6 which is 15 pixels for top margin, 15 pixels for the bottom margin, 10 pixels for the left margin and 10 pixels for the right margin.</p>

<h2 id="Best_practices">Best practices</h2>

<pre class="brush:js  language-js"><code class="language-js">&lt;script type="text/javascript"&gt;
var windowObjectReference = null; // global variable

function openFFPromotionPopup() {
  if(windowObjectReference == null || windowObjectReference.closed)
  /* if the pointer to the window object in memory does not exist
     or if such pointer exists but the window was closed */

  {
    windowObjectReference = window.open("http://www.spreadfirefox.com/",
   "PromoteFirefoxWindowName", "resizable,scrollbars,status");
    /* then create it. The new window will be created and
       will be brought on top of any other window. */
  }
  else
  {
    windowObjectReference.focus();
    /* else the window reference must exist and the window
       is not closed; therefore, we can bring it back on top of any other
       window with the focus() method. There would be no need to re-create
       the window or to reload the referenced resource. */
  };
}
&lt;/script&gt;

(...)

&lt;p&gt;&lt;a
 href="http://www.spreadfirefox.com/"
 target="PromoteFirefoxWindowName"
 onclick="openFFPromotionPopup(); return false;"
 title="This link will create a new window or will re-use an already opened one"
&gt;Promote Firefox adoption&lt;/a&gt;&lt;/p&gt;</code></pre>

<p>The above code solves a few usability problems related to links opening secondary window. The purpose of the <code>return false</code> in the code is to cancel default action of the link: if the onclick event handler is executed, then there is no need to execute the default action of the link. But if javascript support is disabled or non-existent on the user's browser, then the onclick event handler is ignored and the browser loads the referenced resource in the target frame or window that has the name "PromoteFirefoxWindowName". If no frame nor window has the name "PromoteFirefoxWindowName", then the browser will create a new window and will name it "PromoteFirefoxWindowName".</p>

<p>More reading on the use of the target attribute:</p>

<p><a href="http://www.w3.org/TR/html401/present/frames.html#h-16.3.2">HTML 4.01 Target attribute specifications</a></p>

<p><a href="http://www.htmlhelp.com/faq/html/links.html#new-window">How do I create a link that opens a new window?</a></p>

<p>You can also parameterize the function to make it versatile, functional in more situations, therefore re-usable in scripts and webpages:</p>

<pre class="brush:js  language-js"><code class="language-js">&lt;script type="text/javascript"&gt;
var windowObjectReference = null; // global variable

function openRequestedPopup(strUrl, strWindowName) {
  if(windowObjectReference == null || windowObjectReference.closed) {
    windowObjectReference = window.open(strUrl, strWindowName,
           "resizable,scrollbars,status");
  } else {
    windowObjectReference.focus();
  };
}
&lt;/script&gt;

(...)

&lt;p&gt;&lt;a
 href="http://www.spreadfirefox.com/"
 target="PromoteFirefoxWindow"
 onclick="openRequestedPopup(this.href, this.target); return false;"
 title="This link will create a new window or will re-use an already opened one"
&gt;Promote Firefox adoption&lt;/a&gt;&lt;/p&gt;</code>
</pre>

<p>You can also make such function able to open only 1 secondary window and to reuse such single secondary window for other links in this manner:</p>

<pre class="brush:js  language-js"><code class="language-js">&lt;script type="text/javascript"&gt;
var windowObjectReference = null; // global variable
var PreviousUrl; /* global variable which will store the
                    url currently in the secondary window */

function openRequestedSinglePopup(strUrl) {
  if(windowObjectReference == null || windowObjectReference.closed) {
    windowObjectReference = window.open(strUrl, "SingleSecondaryWindowName",
         "resizable,scrollbars,status");
  } else if(PreviousUrl != strUrl) {
    windowObjectReference = window.open(strUrl, "SingleSecondaryWindowName",
      "resizable=yes,scrollbars=yes,status=yes");
    /* if the resource to load is different,
       then we load it in the already opened secondary window and then
       we bring such window back on top/in front of its parent window. */
    windowObjectReference.focus();
  } else {
    windowObjectReference.focus();
  };

  PreviousUrl = strUrl;
  /* explanation: we store the current url in order to compare url
     in the event of another call of this function. */
}
&lt;/script&gt;

(...)

&lt;p&gt;&lt;a
 href="http://www.spreadfirefox.com/"
 target="SingleSecondaryWindowName"
 onclick="openRequestedSinglePopup(this.href); return false;"
 title="This link will create a new window or will re-use an already opened one"
&gt;Promote Firefox adoption&lt;/a&gt;&lt;/p&gt;

&lt;p&gt;&lt;a
 href="http://www.mozilla.org/support/firefox/faq"
 target="SingleSecondaryWindowName"
 onclick="openRequestedSinglePopup(this.href); return false;"
 title="This link will create a new window or will re-use an already opened one"
&gt;Firefox FAQ&lt;/a&gt;&lt;/p&gt;</code>
</pre>

<h2 id="FAQ">FAQ</h2>

<dl>
 <dt>How can I prevent the confirmation message asking the user whether he wants to close the window?</dt>
 <dd>You can not. <strong>New windows not opened by javascript can not as a rule be closed by JavaScript.</strong> The JavaScript Console in Mozilla-based browsers will report the warning message: <code>"Scripts may not close windows that were not opened by script."</code> Otherwise the history of URLs visited during the browser session would be lost.<br>
 <a href="https://developer.mozilla.org/en-US/docs/DOM/window.close">More on the window.close()</a> method</dd>
 <dt>How can I bring back the window if it is minimized or behind another window?</dt>
 <dd>First check for the existence of the window object reference of such window and if it exists and if it has not been closed, then use the <a href="https://developer.mozilla.org/en-US/docs/DOM/window.focus">focus()</a> method. There is no other reliable way. You can examine an <a href="#Best_practices">example explaining how to use the focus() method</a>.</dd>
 <dt>How do I force a maximized window?</dt>
 <dd>You cannot. All browser manufacturers try to make the opening of new secondary windows noticed by users and noticeable by users to avoid confusion, to avoid disorienting users.</dd>
 <dt>How do I turn off window resizability or remove toolbars?</dt>
 <dd>You cannot force this. Users with Mozilla-based browsers have absolute control over window functionalities like resizability, scrollability and toolbars presence via user preferences in <code>about:config</code>. Since your users are the ones who are supposed to use such windows (and not you, being the web author), the best is to avoid interfering with their habits and preferences. We recommend to always set the resizability and scrollbars presence (if needed) to yes to insure accessibility to content and usability of windows. This is in the best interests of both the web author and the users.</dd>
 <dt>How do I resize a window to fit its content?</dt>
 <dd>You can not reliably because the users can prevent the window from being resized by unchecking the <code>Edit/Preferences/Advanced/Scripts &amp; Plug-ins/Allow Scripts to/ Move or resize existing windows</code> checkbox in Mozilla or <code>Tools/Options.../Content tab/Enable Javascript/Advanced button/Move or resize existing windows</code> checkbox in Firefox or by setting <code>dom.disable_window_move_resize</code> to <var>true</var> in <code>about:config</code> or by editing accordingly their <a href="http://www.mozilla.org/support/firefox/edit#user">user.js file</a>.<br>
 In general, users usually disable moving and resizing of existing windows because allowing authors' scripts to do so has been abused overwhelmingly in the past and the rare scripts that do not abuse such feature are often wrong, inaccurate when resizing the window. 99% of all those scripts disable window resizability and disable scrollbars when in fact they should enable both of these features to allow a cautious and sane fallback mechanism if their calculations are wrong.<br>
 The window method <a href="https://developer.mozilla.org/en-US/docs/DOM/window.sizeToContent">sizeToContent()</a> is also disabled if the user unchecks the preference <code>Move or resize existing windows</code> checkbox. Moving and resizing a window remotely on the user's screen via script will very often annoy the users, will disorient the user, and will be wrong at best. The web author expects to have full control of (and can decide about) every position and size aspects of the users' browser window ... which is simply not true.</dd>
 <dt>How do I open a referenced resource of a link in a new tab? or in a specific tab?</dt>
 <dd>To open a resource in a new tab see <a href="https://developer.mozilla.org/en-US/docs/XUL/tabbrowser">Tabbed browser</a>. Some <a href="https://developer.mozilla.org/en-US/Add-ons/Code_snippets/Tabbed_browser?redirectlocale=en-US&amp;redirectslug=Code_snippets%2FTabbed_browser">Code snippets</a> are available. If you are using the SDK, tabs are <a href="https://developer.mozilla.org/en-US/Add-ons/SDK/High-Level_APIs/tabs">handled a bit differently</a><br>
 <a href="http://kmeleon.sourceforge.net/">K-meleon 1.1</a>, a Mozilla-based browser, gives complete control and power to the user regarding how links are opened. Only the user can set his advanced preferences to do that. Some advanced extensions also give Mozilla and Firefox a lot of power over how referenced resources are loaded.<br>
 In a few years, the <a href="http://www.w3.org/TR/2004/WD-css3-hyperlinks-20040224/#target0">target property of the CSS3 hyperlink module</a> may be implemented (if CSS3 Hyperlink module as it is right now is approved). And even if and when this happens, you can expect developers of browsers with tab-browsing to give the user entire veto power and full control over how links can open web pages. How to open a link should always be entirely under the control of the user.</dd>
 <dt>How do I know whether a window I opened is still open?</dt>
 <dd>You can test for the existence of the window object reference which is the returned value in case of success of the window.open() call and then verify that <em>w</em><var>indowObjectReference</var>.closed return value is <var>false</var>.</dd>
 <dt>How can I tell when my window was blocked by a popup blocker?</dt>
 <dd>With the built-in popup blockers of Mozilla/Firefox and Internet Explorer 6 SP2, you have to check the return value of <code>window.open()</code>: it will be <var>null</var> if the window wasn't allowed to open. However, for most other popup blockers, there is no reliable way.</dd>
 <dt>What is the JavaScript relationship between the main window and the secondary window?</dt>
 <dd>The <code>window.open()</code> method gives a main window a reference to a secondary window; the <a href="https://developer.mozilla.org/en-US/docs/DOM/window.opener">opener</a> property gives a secondary window a reference to its main window.</dd>
 <dt>I can not access the properties of the new secondary window. I always get an error in the javascript console saying "Error: uncaught exception: Permission denied to get property &lt;property_name or method_name&gt;. Why is that?</dt>
 <dd>It is because of the cross-domain script security restriction (also referred as the "Same Origin Policy"). A script loaded in a window (or frame) from a distinct origin (domain name) <strong>cannot get nor set</strong> properties of another window (or frame) or the properties of any of its HTML objects coming from another distinct origin (domain name). Therefore, before executing a script targeting a secondary window, the browser in the main window will verify that the secondary window has the same domain name.<br>
 More reading on the cross-domain script security restriction: <a href="http://www.mozilla.org/projects/security/components/same-origin.html">http://www.mozilla.org/projects/secu...me-origin.html</a></dd>
</dl>

<h2 id="Usability_issues">Usability issues</h2>

<h3 id="Avoid_resorting_to_window.open.28.29">Avoid resorting to <code>window.open()</code></h3>

<p>Generally speaking, it is preferable to avoid resorting to window.open() for several reasons:</p>

<ul>
 <li>All Mozilla-based browsers offer <a href="https://developer.mozilla.org/en-US/docs/XUL/tabbrowser">tab-browsing</a> and this is the preferred mode of <a href="https://developer.mozilla.org/en-US/Add-ons/Code_snippets/Tabbed_browser?redirectlocale=en-US&amp;redirectslug=Code_snippets%2FTabbed_browser">opening referenced resources</a> (<a href="https://developer.mozilla.org/en-US/Add-ons/SDK/High-Level_APIs/tabs">SDK</a>)... not just in Mozilla-based browsers but in all other browsers offering tab-browsing. In other words, tab-capable browser users overall prefer opening new tabs than opening new windows in a majority of webpage situations. Tab-capable browsers have rapidly gained support and enthusiasm on internet in the last 3 years; this trend will not revert back. MSIE 7, released in October 2006, has full support for tab browsing.</li>
 <li>There are now <a href="https://addons.mozilla.org/seamonkey/browse/type:1/cat:48/sort:updated">several Mozilla extensions</a> (like Multizilla) and <a href="https://addons.update.mozilla.org/firefox/browse/type:1/cat:14/sort:updated">Firefox extensions</a> (like <a href="https://addons.mozilla.org/firefox/addon/158">Tabbrowser preferences</a>), features, settings and advanced preferences based on tab-browsing and based on converting window.open() calls into opening tabs, based on neutralizing window.open() calls, in particular in neutralizing unrequested openings of new windows (often referred as blocking unrequested popups or as blocking script-initiated windows opening automatically). Such features found in extensions include opening a link in a new window or not, in the same window, in a new tab or not, in "background" or not. Coding carelessly to open new windows can no longer be assured of success, can not succeed by force and, if it does, it will annoy a majority of users.</li>
 <li>New windows can have menubar missing, scrollbars missing, status bar missing, window resizability disabled, etc.; new tabs can not be missing those functionalities or toolbars (or at least, the toolbars which are present by default). Therefore, tab-browsing is preferred by a lot of users because the normal user-interface of the browser window they prefer is kept intact, remains stable.</li>
 <li>Opening new windows, even with reduced features, uses considerably a lot of the user's system resources (cpu, RAM) and involves considerably a lot of coding in the source code (security management, memory management, various code branchings sometimes quite complex, window frame/chrome/toolbars building, window positioning and sizing, etc.). Opening new tabs is less demanding on the user's system resources (and faster to achieve) than opening new windows.</li>
</ul>

<h3 id="Offer_to_open_a_link_in_a_new_window.2C_using_these_guidelines">Offer to open a link in a new window, using these guidelines</h3>

<p>If you want to offer to open a link in a new window, then follow tested and recommendable usability and accessibility guidelines:</p>

<h4 id="Never_use_this_form_of_code_for_links.3Ca_href.3D.22javascriptwindow.open.28....29.22_....3E"><em>Never</em> use this form of code for links: <code>&lt;a href="javascript:window.open(...)" ...&gt;</code></h4>

<p>"javascript:" links break accessibility and usability of webpages in every browser.</p>

<ul>
 <li>"javascript:" pseudo-links become dysfunctional when javascript support is disabled or inexistent. Several corporations allow their employees to surf on the web but under strict security policies: no javascript enabled, no java, no activeX, no Flash. For various reasons (security, public access, text browsers, etc..), about 5% to 10% of users on the web surf with javascript disabled.</li>
 <li>"javascript:" links will interfere with advanced features in tab-capable browsers: eg. middle-click on links, Ctrl+click on links, tab-browsing features in extensions, etc.</li>
 <li>"javascript:" links will interfere with the process of indexing webpages by search engines.</li>
 <li>"javascript:" links interfere with assistive technologies (e.g. voice browsers) and several web-aware applications (e.g. <abbr>PDAs</abbr> and mobile browsers).</li>
 <li>"javascript:" links also interfere with "mouse gestures" features implemented in browsers.</li>
 <li>Protocol scheme "javascript:" will be reported as an error by link validators and link checkers.</li>
</ul>

<p><strong>Further reading:</strong></p>

<ul>
 <li><a href="http://www.useit.com/alertbox/20021223.html">Top Ten Web-Design Mistakes of 2002</a>, 6. JavaScript in Links, Jakob Nielsen, December 2002</li>
 <li><a href="http://www.evolt.org/article/Links_and_JavaScript_Living_Together_in_Harmony/17/20938/">Links &amp; JavaScript Living Together in Harmony</a>, Jeff Howden, February 2002</li>
 <li><a href="http://jibbering.com/faq/#FAQ4_24">comp.lang.javascript newsgroup discussion FAQ on "javascript:" links</a></li>
</ul>

<h4 id="Never_use_.3Ca_href.3D.22.23.22_onclick.3D.22window.open.28....29.3B.22.3E">Never use <code>&lt;a href="#" onclick="window.open(...);"&gt;</code></h4>

<p>Such pseudo-link also breaks accessibility of links. <strong>Always use a real URL for the href attribute value</strong> so that if javascript support is disabled or inexistent or if the user agent does not support opening of secondary window (like MS-Web TV, text browsers, etc), then such user agents will still be able to load the referenced resource according to its default mode of opening/handling a referenced resource. This form of code also interferes with advanced features in tab-capable browsers: eg. middle-click on links, Ctrl+click on links, Ctrl+Enter on links, "mouse gestures" features.</p>

<h4 id="Always_identify_links_which_will_create_.28or_will_re-use.29_a_new.2C_secondary_window">Always identify links which will create (or will re-use) a new, secondary window</h4>

<p>Identify links that will open new windows in a way that helps navigation for users by coding the title attribute of the link, by adding an icon at the end of the link or by coding the cursor accordingly.</p>

<p>The purpose is to warn users in advance of context changes to minimize confusion on the user's part: changing the current window or popping up new windows can be very disorienting to users (Back toolbar button is disabled).</p>

<blockquote>
<p>"Users often don't notice that a new window has opened, especially if they are using a small monitor where the windows are maximized to fill up the screen. So a user who tries to return to the origin will be confused by a grayed out <em>Back</em> button."<br>
 quote from <a href="http://www.useit.com/alertbox/990530.html">The Top Ten <em>New</em> Mistakes of Web Design</a>: 2. Opening New Browser Windows, Jakob Nielsen, May 1999</p>
</blockquote>

<p>When extreme changes in context are explicitly identified before they occur, then the users can determine if they wish to proceed or so they can be prepared for the change: not only they will not be confused or feel disoriented, but more experienced users can better decide how to open such links (in a new window or not, in the same window, in a new tab or not, in "background" or not).</p>

<p><strong>References</strong></p>

<ul>
 <li>"If your link spawns a new window, or causes another windows to 'pop up' on your display, or move the focus of the system to a new FRAME or Window, then the nice thing to do is to tell the user that something like that will happen." <a href="http://www.w3.org/WAI/wcag-curric/sam77-0.htm">World Wide Web Consortium Accessibility Initiative regarding popups</a></li>
 <li>"Use link titles to provide users with a preview of where each link will take them, before they have clicked on it." <a href="http://www.useit.com/alertbox/991003.html">Ten Good Deeds in Web Design</a>, Jakob Nielsen, October 1999</li>
 <li><a href="http://www.useit.com/alertbox/980111.html">Using Link Titles to Help Users Predict Where They Are Going</a>, Jakob Nielsen, January 1998</li>
</ul>

<table class="standard-table">
 <tbody>
  <tr>
   <td class="header" colspan="4">Example "New Window" Icons &amp; Cursors</td>
  </tr>
  <tr>
   <td style="width: 25%;"><img alt="New window icon from yahoo.com" src="https://developer.mozilla.org/@api/deki/files/782/=NewwindowYahoo.png"></td>
   <td style="width: 25%;"><img alt="New window icon from microsoft.com" src="https://developer.mozilla.org/@api/deki/files/780/=NewwinMSIE.gif"></td>
   <td style="width: 25%;"><img alt="New window icon from webaim.org" src="https://developer.mozilla.org/@api/deki/files/296/=Popup_requested_new_window.gif"></td>
   <td style="width: 25%;"><img alt="New window icon from sun.com" src="https://developer.mozilla.org/@api/deki/files/811/=PopupImageSun.gif"></td>
  </tr>
  <tr>
   <td><img alt="New window icon from bbc.co.uk" src="https://developer.mozilla.org/@api/deki/files/795/=Opennews_rb.gif"></td>
   <td><img alt="New window icon from Accessible Internet Solutions" src="https://developer.mozilla.org/@api/deki/files/15/=AIS_NewWindowIcon.png"></td>
   <td><img alt="New window icon from accessify.com" src="https://developer.mozilla.org/@api/deki/files/809/=Pop-up-launcher.gif"></td>
   <td><img alt="New window icon from webstyleguide.com" src="https://developer.mozilla.org/@api/deki/files/417/=Webstyleguide_com_newwind.gif"></td>
  </tr>
  <tr>
   <td><img alt="New window icon from an unknown source" src="https://developer.mozilla.org/@api/deki/files/810/=Popicon_1.gif"></td>
   <td><img alt="New window icon from an unknown source" src="https://developer.mozilla.org/@api/deki/files/779/=New.gif"></td>
   <td><img alt="New window icon from an unknown source" src="https://developer.mozilla.org/@api/deki/files/419/=WillCreateOrRecycleNewWindow.gif"></td>
   <td><img alt="New window icon from gtalbot.org" src="https://developer.mozilla.org/@api/deki/files/287/=OpenRequestedPopup.png"></td>
  </tr>
  <tr>
   <td colspan="2"><img alt="New window cursor from draig.de" src="https://developer.mozilla.org/@api/deki/files/169/=Cursor_LinkNewWindowTargetBlank.png"></td>
   <td colspan="2"><img alt="New window cursor from mithgol.ru" src="https://developer.mozilla.org/@api/deki/files/170/=Cursor_newwindowSergeySokoloff.png"></td>
  </tr>
 </tbody>
</table>

<h4 id="Always_use_the_target_attribute">Always use the target attribute</h4>

<p>If javascript support is disabled or non-existent, then the user agent will create a secondary window accordingly or will render the referenced resource according to its handling of the target attribute: e.g. some user agents which can not create new windows, like MS Web TV, will fetch the referenced resource and append it at the end of the current document. The goal and the idea is to try to provide - <strong>not impose</strong> - to the user a way to open the referenced resource, a mode of opening the link. Your code should not interfere with the features of the browser at the disposal of the user and your code should not interfere with the final decision resting with the user.</p>

<h4 id="Do_not_use_target.3D.22_blank.22">Do not use <code>target="_blank"</code></h4>

<p>Always provide a meaningful name to your target attribute and try to reuse such target attribute in your page so that a click on another link may load the referenced resource in an already created and rendered window (therefore speeding up the process for the user) and therefore justifying the reason (and user system resources, time spent) for creating a secondary window in the first place. Using a single target attribute value and reusing it in links is much more user resources friendly as it only creates one single secondary window which is recycled. On the other hand, using "_blank" as the target attribute value will create several new and unnamed windows on the user's desktop which can not be recycled, reused. In any case, if your code is well done, it should not interfere with the user's final choice but rather merely offer him more choices, more ways to open links and more power to the tool he's using (a browser).</p>

<h2 id="Glossary">Glossary</h2>

<dl>
 <dt>Opener window, parent window, main window, first window</dt>
 <dd>Terms often used to describe or to identify the same window. It is the window from which a new window will be created. It is the window on which the user clicked a link which lead to the creation of another, new window.</dd>
 <dt>Sub-window, child window, secondary window, second window</dt>
 <dd>Terms often used to describe or to identify the same window. It is the new window which was created.</dd>
 <dt>Unrequested popup windows</dt>
 <dd>Script-initiated windows opening automatically without the user's consent.</dd>
</dl>

<h2 id="Specification">规范</h2>

<p>HTML5. See http://www.w3.org/TR/html5/browsers.html#dom-open for details.</p>

<h2 id="Notes">注意</h2>

<h3 id="Note_on_precedence">优先注意事项</h3>

<p>In cases where <code>left</code> and <code>screenX</code> (and/or <code>top</code> and <code>screenY</code>) have conflicting values, then <code>left</code> and <code>top</code> have precedence over <code>screenX</code> and <code>screenY</code> respectively. If <code>left</code> and <code>screenX</code> (and/or <code>top</code> and <code>screenY</code>) are defined in the <var>features</var> list, then <code>left</code> (and/or <code>top</code>) will be honored and rendered. In the following example the new window will be positioned at 100 pixels from the left side of the work area for applications of the user's operating system, not at 200 pixels.</p>

<pre class="brush:js  language-js"><code class="language-js">windowObjectReference = window.open(
  "http://news.bbc.co.uk/",
  "BBCWorldNewsWindowName",
  "left=100,screenX=200,resizable,scrollbars,status"
);</code></pre>

<p>If left is set but top has no value and screenY has a value, then left and screenY will be the coordinate positioning values of the secondary window.</p>

<p>outerWidth has precedence over width and width has precedence over innerWidth. outerHeight has precedence over height and height has precedence over innerHeight. In the following example, Mozilla-browsers will create a new window with an outerWidth of 600 pixels wide and will ignore the request of a width of 500 pixels and will also ignore the request of an innerWidth of 400 pixels.</p>

<pre class="brush:js  language-js"><code class="language-js">windowObjectReference = window.open(
  "http://www.wwf.org/",
  "WWildlifeOrgWindowName",
  "outerWidth=600,width=500,innerWidth=400,resizable,scrollbars,status"
);</code></pre>

<h3 id="Note_on_position_and_dimension_error_correction">Note on position and dimension error correction</h3>

<p>Requested position and requested dimension values in the <var>features</var> list will not be honored and <strong>will be corrected</strong> if any of such requested value does not allow the entire browser window to be rendered within the work area for applications of the user's operating system. <strong>No part of the new window can be initially positioned offscreen. This is by default in all Mozilla-based browser releases.</strong></p>

<p><a href="http://msdn2.microsoft.com/en-us/library/ms997645.aspx#xpsp_topic5">MSIE 6 SP2 has a similar error correction mechanism</a> but it is not activated by default in all security levels: a security setting can disable such error correction mechanism.</p>

<h3 id="Note_on_scrollbars">Note on scrollbars</h3>

<p>When content overflows window viewport dimensions, then scrollbar(s) (or some scrolling mechanism) are necessary to ensure that content can be accessed by users. Content can overflow window dimensions for several reasons which are outside the control of web authors:</p>

<ul>
 <li>user resizes the window</li>
 <li>user increases the text size of fonts via View/Text Zoom (%) menuitem in Mozilla or View/Text Size/Increase or Decrease in Firefox</li>
 <li>user sets a minimum font size for pages which is bigger than the font-size the web author requested. People over 40 years old or with particular viewing habit or reading preference often set a minimal font size in Mozilla-based browsers.</li>
 <li>web author is not aware of default margin (and/or border and/or padding) values applying to root element or body node in various browsers and various browser versions</li>
 <li>user uses an user stylesheet (<a href="http://www.mozilla.org/support/firefox/edit#content">userContent.css in Mozilla-based browsers</a>) for his viewing habits which increases document box dimensions (margin, padding, default font size)</li>
 <li>user can customize individually the size (height or width) of most toolbars via operating system settings. E.g. window resizing borders, height of browser titlebar, menubar, scrollbars, font size are entirely customizable by the user in Windows XP operating system. These toolbars dimensions can also be set via browser themes and skins or by operating system themes</li>
 <li>web author is unaware that the user default browser window has custom toolbar(s) for specific purpose(s); e.g.: prefs bar, web developer bar, accessibility toolbar, popup blocking and search toolbar, multi-feature toolbar, etc.</li>
 <li>user uses assistive technologies or add-on features which modify the operating system's work area for applications: e.g. MS-Magnifier</li>
 <li>user repositions and/or resizes directly or indirectly the operating system's work area for applications: e.g. user resizes the Windows taskbar, user positions the Windows taskbar on the left side (arabic language based) or right side (Hebrew language), user has a permanent MS-Office quick launch toolbar, etc.</li>
 <li>some operating system (Mac OS X) forces presence of toolbars which can then fool the web author's anticipations, calculations of the effective dimensions of the browser window</li>
</ul>

<h3 id="Note_on_status_bar">Note on status bar</h3>

<p>You should assume that a large majority of users' browsers will have the status bar or that a large majority of users will want to force the status bar presence: best is to always set this feature to yes. Also, if you specifically request to remove the status bar, then Firefox users will not be able to view the Site Navigation toolbar if it is installed. In Mozilla and in Firefox, all windows with a status bar have a window resizing grippy at its right-most side. The status bar also provides info on http connection, hypertext resource location, download progress bar, encryption/secure connection info with <abbr>SSL</abbr> connection (displaying a yellow padlock icon), internet/security zone icons, privacy policy/cookie icon, etc. <strong>Removing the status bar usually removes a lot of functionality, features and information considered useful (and sometimes vital) by the users.</strong></p>

<h3 id="Note_on_security_issues_of_the_status_bar_presence">Note on security issues of the status bar presence</h3>

<p>In MSIE 6 for XP SP2: For windows opened using <code>window.open()</code>:</p>

<blockquote>
<p>"For windows opened using window.open():<br>
 Expect the status bar to be present, and code for it. <strong>The status bar will be on by default</strong> and is 20-25 pixels in height. (...)"<br>
 quote from <a href="http://msdn2.microsoft.com/en-us/library/ms997645.aspx#xpsp_topic5">Fine-Tune Your Web Site for Windows XP Service Pack 2, Browser Window Restrictions in XP SP2</a></p>
</blockquote>

<blockquote>
<p>"(...) windows that are created using the window.open() method can be called by scripts and used to spoof a user interface or desktop or to hide malicious information or activity by sizing the window so that the status bar is not visible.<br>
 Internet Explorer windows provide visible security information to the user to help them ascertain the source of the Web page and the security of the communication with that page. When these elements are not in view, the user might think they are on a more trusted page or interacting with a system process when they are actually interacting with a malicious host. (...)<br>
 <strong>Script-initiated windows will be displayed fully, with the Internet Explorer title bar and status bar.</strong> (...)<br>
 Script management of Internet Explorer status bar<br>
 Detailed description<br>
 <strong>Internet Explorer has been modified to not turn off the status bar for any windows. The status bar is always visible for all Internet Explorer windows.</strong> (...) Without this change, windows that are created using the window.open() method can be called by scripts and spoof a user interface or desktop or hide malicious information or activity by hiding important elements of the user interface from the user.<br>
 The status bar is a security feature of Internet Explorer windows that provides Internet Explorer security zone information to the user. This zone cannot be spoofed (...)"<br>
 quote from <a href="http://technet.microsoft.com/en-us/library/bb457150.aspx#ECAA">Changes to Functionality in Microsoft Windows XP Service Pack 2, Internet Explorer Window Restrictions</a></p>
</blockquote>

<h3 id="Note_on_fullscreen">Note on fullscreen</h3>

<p>In MSIE 6 for XP SP2:</p>

<ul>
 <li>"window.open() with fullscreen=yes will now result in a maximized window, not a kiosk mode window."</li>
 <li>"The definition of the fullscreen=yes specification is changed to mean 'show the window as maximized,' which will keep the title bar, address bar, and status bar visible."</li>
</ul>

<p><em>References:</em></p>

<ul>
 <li><a href="http://msdn2.microsoft.com/en-us/library/ms997645.aspx#xpsp_topic5">Fine-Tune Your Web Site for Windows XP Service Pack 2</a></li>
 <li><a href="http://technet.microsoft.com/en-us/library/bb457150.aspx#ECAA">Changes to Functionality in Microsoft Windows XP Service Pack 2, Script sizing of Internet Explorer windows</a></li>
</ul>

<h3 id="Note_on_outerHeight_versus_height">Note on outerHeight versus height</h3>

<p><img alt="innerHeight vs outerHeight illustration" src="https://developer.mozilla.org/@api/deki/files/212/=FirefoxInnerVsOuterHeight.png"></p>

<h3 id="Note_on_refreshing_vs._opening_a_new_windowtab">Note on refreshing vs. opening a new window/tab</h3>

<p>If the <code>strWindowName</code> parameter is omitted, a new window or tab is opened. If a window with the same name already exists, the existing window is refreshed.</p>

<pre class="brush:js  language-js"><code class="language-js">//Always opens a new window/tab
window.open("map.php");

//Refreshes an existing window/tab that was opened with the same name, if one exists
window.open("map.php", "BiggerMap");</code>
</pre>

<h2 id="规范">规范</h2>

{{Specifications}}

<h2 id="Tutorials">教程</h2>

<ul>
 <li><a href="http://www.infimum.dk/HTML/JSwindows.html">JavaScript windows (tutorial)</a> by Lasse Reichstein Nielsen</li>
 <li><a href="http://accessify.com/features/tutorials/the-perfect-popup/">The perfect pop-up (tutorial)</a> by Ian Lloyd</li>
 <li><a href="http://www.gtalbot.org/FirefoxSection/Popup/PopupAndFirefox.html">Popup windows and Firefox (interactive demos)</a> by Gérard Talbot</li>
</ul>

<h2 id="References">参考文献</h2>

<ul>
 <li><a href="http://www.cs.tut.fi/%7Ejkorpela/www/links.html">Links Want To Be Links</a> by Jukka K. Korpela</li>
 <li><a href="http://www.evolt.org/article/Links_and_JavaScript_Living_Together_in_Harmony/17/20938/">Links &amp; JavaScript Living Together in Harmony</a> by Jeff Howden</li>
 <li><a href="https://codepen.io/gildata/pen/VrzXOb">demo</a></li>
</ul>