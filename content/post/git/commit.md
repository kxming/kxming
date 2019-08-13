---
title: "代码提交规范"
date: 2019-08-13T19:48:32+08:00
categories:
- git
- commit
tags:
- git
- commit
keywords:
- git
- commit
#thumbnailImage: //example.com/image.jpg
---

<!--more-->
<div data-v-cc1b3b7a="" data-id="5c862170f265da2d8d6a13ad" itemprop="articleBody" class="article-content"><p>本文的目的是为了给想要快速搭建一套业内流行的<code>angular</code>团队<strong>代码提交规范</strong>（不是<code>angular</code>团队编写代码的规范）的小伙伴们提供一个简单清晰直白的教程。文章的内容不会深究每个环节的细节，但是会用通俗的话语让需要的小伙伴们了解每个环节的含义和作用，从而能做到从0到1的搭建起代码提交的工作流。</p>
<h2 class="heading" data-id="heading-0">1. 格式化 commit message</h2>
<p><code>commit message</code>的重要性我就不在这强调了，我们常规提交代码都是通过<code>git commit -m "xxx"</code>附上一句话来描述此次代码的改动，这样的方式对于一些影响范围大或者broken式的改动来说太过于简单随意。每个人都有自己习惯的提交代码方式，所以我们需要借助一个工具来生成符合规范的<code>commit message</code>并约束提交的人。</p>
<p><a target="_blank" href="https://link.juejin.im?target=https%3A%2F%2Fgithub.com%2Fcommitizen%2Fcz-cli" rel="nofollow noopener noreferrer">commitizen</a>是一个格式化<code>commit message</code>的工具，可以约束提交者按照制定的规范一步一步的填写<code>commit message</code>。</p>
<h3 class="heading" data-id="heading-1">局部安装</h3>
<p><code>npm i -D commitizen</code></p>
<h3 class="heading" data-id="heading-2">配置：</h3>
<p><code>package.json</code>中写入：</p>
<pre><code class="hljs bash copyable" lang="bash"><span class="hljs-string">"script"</span>: {
    ...,
    <span class="hljs-string">"commit"</span>: <span class="hljs-string">"git-cz"</span>,
}
<span class="copy-code-btn">复制代码</span></code></pre><p>这样我们就可以借助<code>commitizen</code>提供的<code>git-cz</code>，用<code>npm run commit</code>命令来替代<code>git commit</code>命令。</p>
<h2 class="heading" data-id="heading-3">2. 采用 angular 团队代码提交规范</h2>
<p>我们已经把可以生成指定<code>commit message</code>的工具<code>commitizen</code>安装好了，接下来要做的就是为<code>commitizen</code>制定一套填写规范。</p>
<p><a target="_blank" href="https://link.juejin.im?target=https%3A%2F%2Fgithub.com%2Fcommitizen%2Fcz-conventional-changelog" rel="nofollow noopener noreferrer">cz-conventional-changelog</a> is a commitizen adapter for the angular preset of conventional-changelog （一套适用于<code>commitizen</code>的<code>angular</code>团队规范）。目前采用比较广泛，那我们就直接给<code>commitizen</code>引用这套规范了。</p>
<h3 class="heading" data-id="heading-4">局部安装</h3>
<p><code>npm i -D cz-conventional-changelog</code></p>
<h3 class="heading" data-id="heading-5">配置：</h3>
<p><code>package.json</code>中写入：</p>
<pre><code class="hljs bash copyable" lang="bash"><span class="hljs-string">"config"</span>: {
    <span class="hljs-string">"commitizen"</span>: {
        <span class="hljs-string">"path"</span>: <span class="hljs-string">"node_modules/cz-conventional-changelog"</span>
    }
}
<span class="copy-code-btn">复制代码</span></code></pre><p>安装配置好以后，执行<code>npm run commit</code>就会出现如下引导式填写：</p>
<p></p><figure><img class="lazyload inited loaded" src="https://kxming.github.io/kxming/git/commit.jpg" data-width="718" data-height="293" src="https://user-gold-cdn.xitu.io/2019/3/11/1696b8d42fe7b57a?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure>
<figure><img class="lazyload inited loaded" src="https://kxming.github.io/kxming/git/commit1.jpg" data-width="683" data-height="186" src="https://user-gold-cdn.xitu.io/2019/3/11/1696b8d7fc2b2b89?imageView2/0/w/1280/h/960/format/webp/ignore-error/1"><figcaption></figcaption></figure><p></p>
<h2 class="heading" data-id="heading-6">3. 校验 commit message</h2>
<p>虽然之前两步已经约束了一套代码提交规范，但是还是有人不按照规范提交代码怎么办呢？这个时候就需要<a target="_blank" href="https://link.juejin.im?target=https%3A%2F%2Fgithub.com%2Fconventional-changelog%2Fcommitlint" rel="nofollow noopener noreferrer">commitlint</a>来帮助我们校验<code>commit message</code>，拒绝不符合规范的<code>commit message</code>。</p>
<p>与<code>eslint</code>类似，<code>commitlint</code>也需要一份校验的配置。别着急，这里有一份与<code>cz-conventional-changelog</code>规范（<code>angular</code>团队规范）配套的校验配置<a target="_blank" href="https://link.juejin.im?target=https%3A%2F%2Fgithub.com%2Fconventional-changelog%2Fcommitlint%2Ftree%2Fmaster%2F%2540commitlint%2Fconfig-conventional" rel="nofollow noopener noreferrer">@commitlint/config-conventional</a>来帮助我们检验<code>commit message</code>的合规性。</p>
<h3 class="heading" data-id="heading-7">局部安装</h3>
<p><code>npm i -D @commitlint/config-conventional @commitlint/cli</code></p>
<h3 class="heading" data-id="heading-8">配置</h3>
<p>安装完成以后，同时需要在项目根目录下创建配置文件<code>commit.config.js</code>或者<code>.commitlintrc.js</code>并写入：</p>
<pre><code class="hljs bash copyable" lang="bash">module.exports = { 
    extends: [
        <span class="hljs-string">'@commitlint/config-conventional'</span>
    ]
}
<span class="copy-code-btn">复制代码</span></code></pre><p>或者在<code>package.json</code>中写入：</p>
<pre><code class="hljs bash copyable" lang="bash"><span class="hljs-string">"commitlint"</span>: {
    <span class="hljs-string">"extends"</span>: [
        <span class="hljs-string">"@commitlint/config-conventional"</span>
    ]
  },
<span class="copy-code-btn">复制代码</span></code></pre><p><code>commitlint</code>就可以运用<code>config-conventional</code>这套校验配置。</p>
<h2 class="heading" data-id="heading-9">4. 配置校验时机</h2>
<p>到了第三步我们的代码提交约束规范已经基本成型了，最后一步要做的就是配置触发<code>commit message</code>校验的时机。</p>
<p>校验<code>commit message</code>的最佳姿势是<a target="_blank" href="https://link.juejin.im?target=https%3A%2F%2Fgit-scm.com%2Fbook%2Fen%2Fv2%2FCustomizing-Git-Git-Hooks" rel="nofollow noopener noreferrer">git hook</a>和<a target="_blank" href="https://link.juejin.im?target=https%3A%2F%2Fgithub.com%2Ftypicode%2Fhusky" rel="nofollow noopener noreferrer">husky</a>的结合。</p>
<p><code>husky</code>（哈士奇）是个什么东西呢？简单来说就是个能让你在每个git钩子中配置相应行为的一个工具。</p>
<h3 class="heading" data-id="heading-10">局部安装</h3>
<p><code>npm install husky --save-dev</code></p>
<h3 class="heading" data-id="heading-11">配置</h3>
<p>安装完成以后，同时需要在项目根目录下创建配置文件<code>.huskyrc</code>或者<code>.huskyrc.js</code>文件并写入：</p>
<pre><code class="hljs bash copyable" lang="bash">{
    <span class="hljs-string">"husky"</span>: {
        <span class="hljs-string">"hooks"</span>: {
            ...,
            <span class="hljs-string">"commit-msg"</span>: <span class="hljs-string">"commitlint -e <span class="hljs-variable">$GIT_PARAMS</span>"</span>
        }
    }
}
<span class="copy-code-btn">复制代码</span></code></pre><p>或者在<code>package.json</code>中写入：</p>
<pre><code class="hljs bash copyable" lang="bash"><span class="hljs-string">"husky"</span>: {
    <span class="hljs-string">"hooks"</span>: {
        ...,
        <span class="hljs-string">"commit-msg"</span>: <span class="hljs-string">"commitlint -e <span class="hljs-variable">$GIT_PARAMS</span>"</span>
    }
}
<span class="copy-code-btn">复制代码</span></code></pre><p>在<code>git commit-msg</code>这个钩子中会触发<code>commitlint</code>的操作。</p>
<h2 class="heading" data-id="heading-12">5. 自动化代码检查</h2>
<p>经过前三步已经打造好了基于<code>angular</code>团队代码提交规范的工作流了，但是如果我们还想在校验<code>commit message</code>的规范性的同时，校验此次提交代码的正确性呢？</p>
<p>借助 <a target="_blank" href="https://link.juejin.im?target=https%3A%2F%2Fgithub.com%2Fokonet%2Flint-staged" rel="nofollow noopener noreferrer">lint-staged</a> 可以让你每次只对你此次提交所在暂存区的文件（<code>git add</code>后的文件）进行一系列的检查、修复、格式化操等作。</p>
<h3 class="heading" data-id="heading-13">局部安装</h3>
<p><code>npm install -D lint-staged</code></p>
<h3 class="heading" data-id="heading-14">配置</h3>
<p>安装完成以后，同时需要在项目根目录下创建配置文件<code>.lintstagedrc</code>并写入：</p>
<pre><code class="hljs bash copyable" lang="bash">{
  <span class="hljs-string">"*.{js,vue}"</span>: [
    <span class="hljs-string">"eslint --fix"</span>,
    <span class="hljs-string">"git add"</span>
  ],
  <span class="hljs-string">"*.{html,vue,css,sass,scss}"</span>: [
    <span class="hljs-string">"stylelint --fix"</span>,
    <span class="hljs-string">"git add"</span>
  ]
}
<span class="copy-code-btn">复制代码</span></code></pre><p>或者在<code>package.json</code>中写入：</p>
<pre><code class="hljs bash copyable" lang="bash"><span class="hljs-string">"lint-staged"</span>: {
    <span class="hljs-string">"*.{js,vue}"</span>: [
    <span class="hljs-string">"eslint --fix"</span>,
    <span class="hljs-string">"git add"</span>
  ],
  <span class="hljs-string">"*.{html,vue,css,sass,scss}"</span>: [
    <span class="hljs-string">"stylelint --fix"</span>,
    <span class="hljs-string">"git add"</span>
  ]
}
<span class="copy-code-btn">复制代码</span></code></pre><p>在第三步创建的<code>husky</code>配置文件进行补充：</p>
<pre><code class="hljs bash copyable" lang="bash"><span class="hljs-string">"husky"</span>: {
    <span class="hljs-string">"hooks"</span>: {
        <span class="hljs-string">"pre-commit"</span>: <span class="hljs-string">"lint-staged"</span>,
        <span class="hljs-string">"commit-msg"</span>: <span class="hljs-string">"commitlint -e <span class="hljs-variable">$GIT_PARAMS</span>"</span>
    }
}
<span class="copy-code-btn">复制代码</span></code></pre><p>在<code>pre-commit</code>这个钩子中，<code>lint-staged</code>会执行<code>.lintstagedrc</code>配置的操作（列出来的配置的意思是对本次提交的<code>js</code>或者<code>vue</code>文件进行<code>eslint</code>检查并修复，并且把修复过后的文件再重新提交到暂存区）。</p>
<h2 class="heading" data-id="heading-15">6. 版本发布</h2>
<p>对于每次项目新版本的发布，我们需要更新相应的版本号并记录其中的改变。可以借助 <a target="_blank" href="https://link.juejin.im?target=https%3A%2F%2Fgithub.com%2Fconventional-changelog%2Fstandard-version" rel="nofollow noopener noreferrer">standard-version</a> 工具，来替代<code>npm run version</code>，并自动生成<code>CHANGELOG</code>。</p>
<h3 class="heading" data-id="heading-16">局部安装</h3>
<pre><code class="hljs bash copyable" lang="bash">npm install standard-version --save-dev
<span class="copy-code-btn">复制代码</span></code></pre><h3 class="heading" data-id="heading-17">配置</h3>
<pre><code class="hljs bash copyable" lang="bash"><span class="hljs-string">"scripts"</span>: {
    <span class="hljs-string">"release"</span>: <span class="hljs-string">"standard-version"</span>,
    ...
 }
<span class="copy-code-btn">复制代码</span></code></pre><p>执行<code>npm run release</code>指令实际执行了五个动作：</p>
<ol>
<li>修改<code>package.json</code>中的版本号</li>
<li>修改<code>package-lock.json</code>中的版本号</li>
<li>生成<code>CHANGELOG.md</code>文件</li>
<li>提交<code>package.json</code>、<code>package-lock.json</code>、<code>CHANGELOG.md</code>文件</li>
<li>给这次提交记录打上<code>tag</code></li>
</ol>
<p></p><figure><img class="lazyload inited" src="https://kxming.github.io/kxming/git/commit3.jpg" data-width="531" data-height="360" src="data:image/svg+xml;utf8,<?xml version=&quot;1.0&quot;?><svg xmlns=&quot;http://www.w3.org/2000/svg&quot; version=&quot;1.1&quot; width=&quot;531&quot; height=&quot;360&quot;></svg>"><figcaption></figcaption></figure><p></p>
<p>如果发布的是首个版本，则可以运行如下指令：</p>
<pre><code class="hljs bash copyable" lang="bash">npm run release -- --firse-release
<span class="copy-code-btn">复制代码</span></code></pre><p>如果需要发布预发布版本，则可以使用<code>--prerelease/-p</code>标志来添加预发布版本号：</p>
<pre><code class="hljs bash copyable" lang="bash"><span class="hljs-comment"># 当前版本为 1.0.0</span>
npm run release -- --prerelease  <span class="hljs-comment"># 版本为 1.0.1-0</span>
npm run release -- --prerelease beta  <span class="hljs-comment"># 版本为 1.0.1-beta.1</span>
<span class="copy-code-btn">复制代码</span></code></pre><p>如果是正常的版本迭代，则可以使用<code>--release-as/-r</code>标志来指定版本：</p>
<pre><code class="hljs bash copyable" lang="bash"><span class="hljs-comment"># 当前版本为 1.0.0</span>
npm run release -- --release-as patch  <span class="hljs-comment"># 版本为 1.0.1，npm run release默认行为</span>
npm run release -- --release-as minor  <span class="hljs-comment"># 版本为 1.1.0</span>
npm run release -- --release-as major  <span class="hljs-comment"># 版本为 2.0.0</span>
npm run release -- --release-as 2.0.1  <span class="hljs-comment"># 版本为 2.0.1</span>
npm run release -- --release-as 2.0.1-alpha.0  <span class="hljs-comment"># 版本为 2.0.1-alpha.0</span>
<span class="copy-code-btn">复制代码</span></code></pre><blockquote>
<p>一般项目要上线新版本的时候，需要把<code>release</code>分支合到<code>master</code>，合完分支以后执行<code>npm run release</code>指令给这次发布打上<code>tag</code>并记录修改是一个良好的维护版本迭代的好习惯。</p>
</blockquote>
<h2 class="heading" data-id="heading-18">最后</h2>
<p>一个完整的基于<code>angular</code>团队代码提交规范的工作流已经打造完成，如果有不适应<code>angular</code>这套规范的话也可以自定义一套规范，这里就不再赘述了。当然，有的小伙伴觉得这么写<code>commit</code>很麻烦，但是一个好的提交规范习惯有助于整个团队在项目中高效率的开发，所以赶紧在自己项目中用起来吧！</p>
</div>