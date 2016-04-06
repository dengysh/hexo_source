---
title: npm包管理
date: 2016-04-04 11:44:53
categories: npm
tags: [npm,hexo]
---
<div>
<h2>NPM是什么</h2>
</div>
<p>NPM（node package manager），通常称为node包管理器。顾名思义，它的主要功能就是管理node包，包括：安装、卸载、更新、查看、搜索、发布等。</p>
<p>npm的背后，是基于couchdb的一个数据库，详细记录了每个包的信息，包括作者、版本、依赖、授权信息等。它的一个很重要的作用就是：将开发者从繁琐的包管理工作（版本、依赖等）中解放出来，更加专注于功能的开发。</p>
<p>npm官网：<a href="https://npmjs.org/">https://npmjs.org/</a></p>
<!--more-->
<p>npm官方文档：<a href="https://npmjs.org/doc/README.html">https://npmjs.org/doc/README.html</a></p>
<div>
<h2>我们需要了解什么</h2>
</div>
<ol>
<li>npm的安装、卸载、升级、配置</li>

<li>npm的使用：package的安装、卸载、升级、查看、搜索、发布</li>
<li>npm包的安装模式：本地 vs 全局</li>
<li>package.json：包描述信息</li>
<li>package版本：常见版本声明形式</li>
</ol>
<div>
<h2>npm包安装模式</h2>
</div>
<p>在具体介绍npm包的管理之前，我们首先得来了解一下npm包的两种安装模式。</p>
<h3>本地安装 vs 全局安装（重要）</h3>
<p>node包的安装分两种：本地安装、全局安装。两者的区别如下，后面会通过简单例子说明</p>
<ul>
<li>本地安装：package会被下载到当前所在目录，也只能在当前目录下使用。</li>
<li>全局安装：package会被下载到到特定的系统目录下，安装的package能够在所有目录下使用。</li>
</ul>
<h3>npm install pkg - 本地安装</h3>
<p>运行如下命令，就会在当前目录下安装<code>grunt-cli</code>（grunt命令行工具）</p>
<div>
<pre><code>npm install grunt-cli</code></pre>
</div>
<p>安装结束后，当前目录下回多出一个<code>node_modules</code>目录，grunt-cli就安装在里面。同时注意控制台输出的信息：</p>
<div>
<pre><a href="mailto:grunt-cli@0.1.9">grunt-cli@0.1.9</a> node_modules/grunt-cli</pre>
<pre>├── <a href="mailto:resolve@0.3.1">resolve@0.3.1</a></pre>
<pre>├── <a href="mailto:nopt@1.0.10">nopt@1.0.10</a> (<a href="mailto:abbrev@1.0.4">abbrev@1.0.4</a>)</pre>
<pre>└── <a href="mailto:findup-sync@0.1.2">findup-sync@0.1.2</a> (<a href="mailto:lodash@1.0.1">lodash@1.0.1</a>, <a href="mailto:glob@3.1.21">glob@3.1.21</a>)</pre>
</div>
<p>简单说明一下：</p>
<ul>
<li>grunt-cli@0.1.9：当前安装的package为grunt-cli，版本为0.19</li>
<li>node_modules/grunt-cli：安装目录</li>
<li>resolve@0.3.1：依赖的包有resolve、nopt、findup-sync，它们各自的版本、依赖在后面的括号里列出来</li>
</ul>
<h3>npm install -g pkg- 全局安装</h3>
<p>上面已经安装了grunt-cli，然后你跑到其他目录下面运行如下命令</p>
<div>
<pre><code>grunt</code></pre>
</div>
<p>果断提示你grunt命令不存在，为什么呢？因为上面只是进行了<strong>本地安装</strong>，grunt命令只能在对应安装目录下使用。</p>
<div>
<pre><code>-bash: grunt: command not found</code></pre>
</div>
<p>如果为了使用grunt命令，每到一个目录下都得重新安装一次，那不抓狂才怪。肿么办呢？</p>
<p>很简单，采用全局安装就行了，很简单，加上参数<code>-g</code>就可以了</p>
<div>
<pre><code>npm install -g grunt-cli</code></pre>
</div>
<p>于是，在所有目录下都可以无压力使用<code>grunt</code>命令了。这个时候，你会注意到控制台输入的信息有点不同。主要的区别在于安装目录，现在变成了<code>/usr/local/lib/node_modules/grunt-cli</code>，<code>/usr/local/lib/node_modules/</code>也就是之前所说的全局安装目录啦。</p>
<div>
<pre><a href="mailto:grunt-cli@0.1.9">grunt-cli@0.1.9</a> /usr/local/lib/node_modules/grunt-cli</pre>
<pre>├── <a href="mailto:resolve@0.3.1">resolve@0.3.1</a></pre>
<pre>├── <a href="mailto:nopt@1.0.10">nopt@1.0.10</a> (<a href="mailto:abbrev@1.0.4">abbrev@1.0.4</a>)</pre>
<pre>└── <a href="mailto:findup-sync@0.1.2">findup-sync@0.1.2</a> (<a href="mailto:lodash@1.0.1">lodash@1.0.1</a>, <a href="mailto:glob@3.1.21">glob@3.1.21</a>)</pre>
</div>
<div>
<h2>npm包管理</h2>
</div>
<p>npm的包管理命令是使用频率最高的，所以也是我们需要牢牢记住并熟练使用的。其实无非也就是几个动作：安装、卸载、更新、查看、搜索、发布等。</p>
<h3>安装最新版本的grunt-cli</h3>
<div>
<pre><code>npm install grunt-cli</code></pre>
</div>
<h3>安装0.1.9版本的grunt-cli</h3>
<div>
<pre><code>npm install <a href="mailto:grunt-cli@%220.1.9">grunt-cli@"0.1.9</a>"</code></pre>
</div>
<h3>通过package.json进行安装</h3>
<p>如果我们的项目依赖了很多package，一个一个地安装那将是个体力活。我们可以将项目依赖的包都在package.json这个文件里声明，在搭建hexo时，就可以修改目录下的package.json，添加想要的包/hexo插件，然后一行命令就可以安装所有项目依赖的包。</p>
<div>
<pre><code>npm install</code></pre>
</div>
<h3>其他package安装命令</h3>
<p>运行如下命令，列出所有<code>npm install</code>可能的参数形式</p>
<div>
<pre><code>npm install --help</code></pre>
</div>
<p>输出如下，有兴趣的童鞋可以了解下</p>
<div>
<pre><code>npm install &lt;tarball file&gt;</code></pre>
<pre><code>npm install &lt;tarball url&gt;</code></pre>
<pre><code>npm install &lt;folder&gt;</code></pre>
<pre><code>npm install &lt;pkg&gt;</code></pre>
<pre><code>npm install &lt;pkg&gt;@&lt;tag&gt;</code></pre>
<pre><code>npm install &lt;pkg&gt;@&lt;version&gt;</code></pre>
<pre><code>npm install &lt;pkg&gt;@&lt;version range&gt;</code></pre>
</div>
<h3>卸载grunt-cli</h3>
<p>比如卸载grunt-cli</p>
<div>
<pre><code>npm uninstall grunt-cli</code></pre>
</div>
<h3>卸载0.1.9版本的grunt-cli</h3>
<div>
<pre><code>npm uninstall <a href="mailto:grunt-cli@%220.1.9">grunt-cli@"0.1.9</a>"</code></pre>
</div>
<h3>npm ls：查看安装了哪些包</h3>
<p>运行如下命令，就可以查看当前目录安装了哪些package</p>
<div>
<pre><code>npm ls</code></pre>
</div>
<p>输出如下</p>
<div>
<pre><code>/private/tmp/npm</code></pre>
<pre><code>└─┬ <a href="mailto:grunt-cli@0.1.9">grunt-cli@0.1.9</a></code></pre>
<pre><code>&nbsp; ├─┬ <a href="mailto:findup-sync@0.1.2">findup-sync@0.1.2</a></code></pre>
<pre><code>&nbsp; │ ├─┬ <a href="mailto:glob@3.1.21">glob@3.1.21</a></code></pre>
<pre><code>&nbsp; │ │ ├── <a href="mailto:graceful-fs@1.2.3">graceful-fs@1.2.3</a></code></pre>
<pre><code>&nbsp; │ │ ├── <a href="mailto:inherits@1.0.0">inherits@1.0.0</a></code></pre>
<pre><code>&nbsp; │ │ └─┬ <a href="mailto:minimatch@0.2.12">minimatch@0.2.12</a></code></pre>
<pre><code>&nbsp; │ │&nbsp;&nbsp; ├── <a href="mailto:lru-cache@2.3.0">lru-cache@2.3.0</a></code></pre>
<pre><code>&nbsp; │ │&nbsp;&nbsp; └── <a href="mailto:sigmund@1.0.0">sigmund@1.0.0</a></code></pre>
<pre><code>&nbsp; │ └── <a href="mailto:lodash@1.0.1">lodash@1.0.1</a></code></pre>
<pre><code>&nbsp; ├─┬ <a href="mailto:nopt@1.0.10">nopt@1.0.10</a></code></pre>
<pre><code>&nbsp; │ └── <a href="mailto:abbrev@1.0.4">abbrev@1.0.4</a></code></pre>
<pre><code>&nbsp; └── <a href="mailto:resolve@0.3.1">resolve@0.3.1</a></code></pre>
</div>
<p>同样，如果是要查看package的全局安装信息，加上<code>-g</code>就可以</p>
<pre><code>npm ls -g</code></pre>
<h3>npm ls pkg：查看特定package的信息</h3>
<p>运行如下命令，输出grunt-cli的信息</p>
<div>
<pre><code>npm ls grunt-cli</code></pre>
</div>
<p>输出的信息比较有限，只有安装目录、版本，如下：</p>
<div>
<pre><code>/private/tmp/npm</code></pre>
<pre><code>└── <a href="mailto:grunt-cli@0.1.9">grunt-cli@0.1.9</a> </code></pre>
</div>
<p>如果要查看更详细信息，可以通过<code>npm info pkg</code>，输出的信息非常详尽，包括作者、版本、依赖等。</p>
<div>
<pre><code>npm info grunt-cli</code></pre>
</div>
<h3>npm update pkg：package更新</h3>
<div>
<pre><code>npm update grunt-cli</code></pre>
</div>
<h3>npm search pgk：搜索</h3>
<p>输入如下命令</p>
<div>
<pre><code>npm search grunt-cli</code></pre>
</div>
<p>返回结果如下</p>
<div>
<pre><code>npm http GET <a href="http://registry.npmjs.org/-/all/since?stale=update_after&amp;startkey=1375519407838">http://registry.npmjs.org/-/all/since?stale=update_after&amp;startkey=1375519407838</a></code></pre>
<pre><code>npm http 200 <a href="http://registry.npmjs.org/-/all/since?stale=update_after&amp;startkey=1375519407838">http://registry.npmjs.org/-/all/since?stale=update_after&amp;startkey=1375519407838</a></code></pre>
<pre><code>NAME&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; DESCRIPTION&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; AUTHOR&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; DATE&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; KEYWORDS</code></pre>
<pre><code>grunt-cli&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; The grunt command line interface.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; =cowboy =tkellen&nbsp; 2013-07-27 02:24</code></pre>
<pre><code>grunt-cli-dev-exitprocess The grunt command line interface.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; =dnevnik&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 2013-03-11 16:19</code></pre>
<pre><code>grunt-client-compiler Grunt wrapper for client-compiler.&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; =rubenv&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 2013-03-26 09:15&nbsp; gruntplugin</code></pre>
<pre><code>grunt-clientside&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; Generate clientside js code from CommonJS modules&nbsp; =jga&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 2012-11-07 01:20&nbsp; gruntplugin</code></pre>
</div>
<h3>npm发布</h3>
<p>这个命令我自己也还没实际用过，不误导大家，语法如下，也可参考官方对于package发布的说明<a href="https://npmjs.org/doc/developers.html">https://npmjs.org/doc/developers.html</a>：</p>
<div>
<pre><code>npm publish &lt;tarball&gt;</code></pre>
<pre><code>npm publish &lt;folder&gt;</code></pre>
</div>
<div>
<h2>NPM配置</h2>
</div>
<p>npm的配置工作主要是通过<code>npm config</code>命令，主要包含增、删、改、查几个步骤，下面就以最为常用的proxy配置为例。</p>
<h3>设置proxy</h3>
<p>内网使用npm很头痛的一个问题就是代理，假设我们的代理是&nbsp;<a href="http://proxy.example.com:8080%EF%BC%8C%E9%82%A3%E4%B9%88%E5%91%BD%E4%BB%A4%E5%A6%82%E4%B8%8B%EF%BC%9A">http://proxy.example.com:8080，那么命令如下：</a></p>
<div>
<pre><code>npm config set proxy <a href="http://proxy.example.com:8080">http://proxy.example.com:8080</a></code></pre>
</div>
<p>由于<code>npm config set</code>命令比较常用，于是可以如下简写</p>
<div>
<pre><code>npm set proxy <a href="http://proxy.example.com:8080">http://proxy.example.com:8080</a>&nbsp;&nbsp;&nbsp; </code></pre>
</div>
<h3>查看proxy</h3>
<p>设置完，我们查看下当前代理设置</p>
<div>
<pre><code>npm config get proxy</code></pre>
</div>
<p>输出如下：</p>
<div>
<pre><code><a href="http://proxy.example.com:8080/">http://proxy.example.com:8080/</a></code></pre>
</div>
<p>同样可如下简写：</p>
<div>
<pre><code>npm get proxy</code></pre>
</div>
<h3>删除proxy</h3>
<p>代理不需要用到了，那删了吧</p>
<div>
<pre><code>npm delete proxy</code></pre>
</div>
<h3>查看所有配置</h3>
<div>
<pre><code>npm config list</code></pre>
</div>
<h3>直接修改配置文件</h3>
<p>有时候觉得一条配置一条配置地修改有些麻烦，就直接进配置文件修改了</p>
<div>
<pre><code>npm config edit</code></pre>
</div>
<div>
<h2>关于package.json</h2>
</div>
<p>这货在官网似乎没有详细的描述，其实就是包的描述信息啦。假设当我们下载了node应用，这个node应用依赖于A、B、C三个包，如果没有package.json，我们需要人肉安装这个三个包（如果对版本有特定要求就更悲剧了）：</p>
<div>
<pre><code>npm install A</code></pre>
<pre><code>npm install B</code></pre>
<pre><code>npm install C</code></pre>
</div>
<p>有了package.json，一行命令安装所有依赖。</p>
<div>
<pre><code>npm install</code></pre>
</div>
<h3>package.json字段简介</h3>
<p>字段相当多，但最重要的的是下面几个</p>
<ol>
<li>name: package的名字（由于他会成为url的一部分，所以 non-url-safe 的字母不会通过，也不允许出现"."、"_"），最好先在<a href="http://registry.npmjs.org/%E4%B8%8A%E6%90%9C%E4%B8%8B%E4%BD%A0%E5%8F%96%E7%9A%84%E5%90%8D%E5%AD%97%E6%98%AF%E5%90%A6%E5%B7%B2%E7%BB%8F%E5%AD%98%E5%9C%A8">http://registry.npmjs.org/上搜下你取的名字是否已经存在</a></li>
<li>version: package的版本，当package发生变化时，version也应该跟着一起变化，同时，你声明的版本需要通过semver的校验（semver可自行谷歌）</li>
<li>dependencies: package的应用依赖模块，即别人要使用这个package，至少需要安装哪些东东。应用依赖模块会安装到当前模块的node_modules目录下。</li>
<li>devDependencies：package的开发依赖模块，即别人要在这个package上进行开发</li>
<li>其他：参见官网</li>
</ol>
<div>
<h2>package版本</h2>
</div>
<p>在package.json里，你经常会在包名后看到类似"~0.1.0"这样的字符串，这就是包的版本啦。下面会列举最常见的版本声明形式，以及版本书写的要求：</p>
<h3>常见版本声明形式</h3>
<p>a、"~1.2.3" 是神马意思呢，看下面领悟</p>
<div>
<pre><code>"~1.2.3" = "&gt;=1.2.3 &lt;1.3.0"</code></pre>
<pre><code>"~1.2" = "&gt;=1.2.0 &lt;1.3.0"</code></pre>
<pre><code>"~1" = "&gt;=1.0.0 &lt;1.1.0"</code></pre>
</div>
<p>b、"1.x.x"是什么意思呢，继续自行领悟</p>
<div>
<pre><code>"1.2.x" = "&gt;=1.2.0 &lt;1.3.0"</code></pre>
<pre><code>"1.x.x" = "&gt;=1.0.0 &lt;2.0.0"</code></pre>
<pre><code>"1.2" = "1.2.x"</code></pre>
<pre><code>"1.x" = "1.x.x"</code></pre>
<pre><code>"1" = "1.x.x"</code></pre>
</div>
<h3>版本书写要求</h3>
<ol>
<li>版本可以v开头，比如 v1.0.1（v只是可选）</li>
<li>1.0.1-7，这里的7是所谓的&ldquo;构建版本号&rdquo;，不理是神马，反正版本大于1.0.1</li>
<li>1.0.1beta，或者1.0.1-beta，如果1.0.1后面不是 &ldquo;连字符加数字&rdquo; 这种形式，那么它是pre release 版本，即版本小于 1.0.1</li>
<li>根据b、c，有：0.1.2-7 &gt; 0.1.2-7-beta &gt; 0.1.2-6 &gt; 0.1.2 &gt; 0.1.2beta</li>
</ol>

<p>来自：http://www.cnblogs.com/chyingp/p/npm.html</p>




