<!-- wp:heading -->
<h2 class="wp-block-heading">在开始之前</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p><mark><em>了解一下memos</em></mark></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p><strong>一款清爽且轻量级备忘录中心：memos</strong></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p style="padding-left: 40px;">这是一个采用 React+Tailwind+TypeScript+Go 开发的备忘录中心，相当于极简的微博。支持私有/公开备忘录、标签、互动式日历等功能，以及 Docker 部署。</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>完全开源、自托管的笔记解决方案，专为无缝部署和多平台访问而设计。体验轻松无痛的纯文本书写，并辅以强大的 Markdown 语法支持，以增强格式设置。</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2 class="wp-block-heading">主要特点!!!</h2>
<!-- /wp:heading -->

<!-- wp:list -->
<ul class="wp-block-list"><!-- wp:list-item -->
<li><strong>隐私第一</strong>🏠：掌控您的数据。所有运行时数据都安全地存储在您的本地数据库中。</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><strong>快速创建</strong>✍️：将内容保存为纯文本以便快速访问，并支持 Markdown 进行快速格式化和轻松共享。</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><strong>轻量但功能强大</strong>🤲：我们的应用程序采用 Go、React.js 和紧凑的架构构建，在轻量级软件包中提供强大的性能。</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><strong>可定制</strong>🧩：轻松定制您的服务器名称、图标、描述、系统样式和执行脚本，使其独一无二。</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><strong>开源</strong>🦦：Memos 拥抱开源的未来，所有代码均可在 GitHub 上获取，以实现透明度和协作。</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li><strong>免费使用</strong>💸：完全免费享受所有功能，任何内容均不收费。</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>1、在线体验 【<strong><a href="https://demo.usememos.com/">点击前往</a></strong>】</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>2、Github 开源 【<strong><a href="https://github.com/usememos/memos?tab=readme-ov-file">链接直达</a></strong>】</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>3、Docker 一键部署命令：</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:code -->
<pre class="wp-block-code"><code>docker run -d --name memos -p 5230:5230 -v ~/.memos/:/var/opt/memos neosmemo/memos:stable</code></pre>
<!-- /wp:code -->

<!-- wp:paragraph -->
<p>安装后通过ip+端口5230 即可打开访问！</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>我们需要：</p>
<!-- /wp:paragraph -->

<!-- wp:list -->
<ul class="wp-block-list"><!-- wp:list-item -->
<li>1.安装docker desktop</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>2.镜像源更换</li>
<!-- /wp:list-item -->

<!-- wp:list-item -->
<li>3.pull neosmemo/memos.</li>
<!-- /wp:list-item --></ul>
<!-- /wp:list -->

<!-- wp:heading -->
<h2 class="wp-block-heading">下载安装docker</h2>
<!-- /wp:heading -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><!-- wp:paragraph -->
<p>打开官网链接<a href="https://www.docker.com/">docker</a></p>
<!-- /wp:paragraph --></blockquote>
<!-- /wp:quote -->

<!-- wp:image {"id":539,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img class="wp-image-539" src="https://nsh.asia/wp-content/uploads/2024/10/1730192289-docker-1024x499.png" alt="" /></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>安装好之后</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>打开settings</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>打开docker engines，加入镜像源即可（自己找哈😄）</p>
<!-- /wp:paragraph -->

<!-- wp:heading -->
<h2 class="wp-block-heading">拉取 neosmemo/memos容器</h2>
<!-- /wp:heading -->

<!-- wp:quote -->
<blockquote class="wp-block-quote"><!-- wp:paragraph -->
<p>在powershell中运行一键安装也行(参考一下官方文档)</p>
<!-- /wp:paragraph --></blockquote>
<!-- /wp:quote -->

<!-- wp:image {"id":540,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img class="wp-image-540" src="https://nsh.asia/wp-content/uploads/2024/10/1730192301-目录后一句话安装-1024x344.png" alt="" /></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p><strong>或者</strong></p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":541,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img class="wp-image-541" src="https://nsh.asia/wp-content/uploads/2024/10/1730192307-配置-1024x587.png" alt="" /></figure>
<!-- /wp:image -->

<!-- wp:heading -->
<h2 class="wp-block-heading">然后打开网站（ip+5230端口）</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>网站界面优美，而且支持丰富的Markdown，可以用来自己备忘，写点东西</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":542,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img class="wp-image-542" src="https://nsh.asia/wp-content/uploads/2024/10/1730192314-0-1024x503.png" alt="" /></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p><mark>可以对比一下</mark></p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":543,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img class="wp-image-543" src="https://nsh.asia/wp-content/uploads/2024/10/1730192318-1-1024x511.png" alt="" /></figure>
<!-- /wp:image -->

<!-- wp:paragraph -->
<p>贴一下官方文档<a href="https://www.usememos.com/docs">What is Memos - Memos</a></p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>里面的Markdown生态丰富</p>
<!-- /wp:paragraph -->

<!-- wp:image {"id":544,"sizeSlug":"large","linkDestination":"none"} -->
<figure class="wp-block-image size-large"><img class="wp-image-544" src="https://nsh.asia/wp-content/uploads/2024/10/1730192324-丰富Markdown-297x1024.png" alt="" /></figure>
<!-- /wp:image -->

<!-- wp:heading -->
<h2 class="wp-block-heading">开始愉快的使用吧！！！</h2>
<!-- /wp:heading -->

<!-- wp:paragraph -->
<p>PS：本人于10.30日晚上成功搭建好了memos，大家可以体验一下，想要注册的评论回复我体验</p>
<!-- /wp:paragraph -->

<!-- wp:paragraph -->
<p>贴个链接<a href="https://note.nsh.asia/">Memos</a></p>
<!-- /wp:paragraph -->