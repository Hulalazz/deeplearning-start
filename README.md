# deeplearning-start

<!DOCTYPE html>

<html class="theme">

<head>
    <meta charset="utf-8">
    
    <meta name="description" content="Cmd Markdown 编辑阅读器，支持实时同步预览，区分写作和阅读模式，支持在线存储，分享文稿网址。">
    <meta name="author" content="Jiawei Zhang">

    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    
    <title>零基础入门深度学习(1) - 感知器 - 作业部落 Cmd Markdown 编辑阅读器</title>


    <link href="https://www.zybuluo.com/static/img/favicon.png" type="image/x-icon" rel="icon">

    <link href="https://www.zybuluo.com/static/assets/1bc053c8.base.lib.min.css" rel="stylesheet" media="screen">


    
    <!-- id="prettify-style" will be used to get the link element below and change href to change prettify code, so it can't be in beginmin/endmin block. -->
    <link id="prettify-style" href="https://www.zybuluo.com/static/editor/libs/google-code-prettify/prettify-cmd.css" type="text/css" rel="stylesheet">
    <!--
    <link id="mermaid-style" href="https://www.zybuluo.com/static/editor/libs/mermaid/mermaid.forest.css" type="text/css" rel="stylesheet">
    -->
    <link href="https://www.zybuluo.com/static/assets/mdeditor/45c7d56d.layout.min.css" rel="stylesheet" media="screen">


    

    <script>
      (function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
      (i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
      m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
      })(window,document,'script','//www.google-analytics.com/analytics.js','ga');

      ga('create', 'UA-44461741-1', 'zybuluo.com');
      ga('send', 'pageview');
    </script>
</head>

<body class="theme">

    <div id="global-prompt-alert" class="hide alert alert-warning">
        <span id="global-prompt-message"></span>
        <a id="close-global-prompt-alert" href="">[关闭]</a>
    </div>

    <!-- zybuluo's body -->
    







<!-- mdeditor's body -->






<div id="editor-reader-full" class="editor-reader-full-shown" style="position: static;">
    <div id="reader-full-topInfo" class="reader-full-topInfo-shown">
        <span>
            <code>@hanbingtao</code>
        </span>
        <code><span class="article-updated-date">2017-08-28T11:35:23.000000Z</span></code>
        <code><span>字数 </span><span class="article-characters">5679</span></code>
        <code><span>阅读 </span><span class="article-read">140843</span></code>
    </div>
    <div id="wmd-preview" class="wmd-preview wmd-preview-full-reader"><div class="md-section-divider"></div><div class="md-section-divider"></div><h1 data-anchor-id="1uus" id="零基础入门深度学习1-感知器">零基础入门深度学习(1) - 感知器</h1><p data-anchor-id="clw6"><code>机器学习</code> <code>深度学习入门</code></p><hr><p data-anchor-id="4s1h"><img src="http://upload-images.jianshu.io/upload_images/2256672-06627c71f0d8c0dc.jpg" alt=""></p><blockquote data-anchor-id="49jw" class="white-blockquote">
  <p>无论即将到来的是大数据时代还是人工智能时代，亦或是传统行业使用人工智能在云上处理大数据的时代，作为一个有理想有追求的程序员，不懂深度学习（Deep Learning）这个超热的技术，会不会感觉马上就out了？现在救命稻草来了，《零基础入门深度学习》系列文章旨在讲帮助爱编程的你从零基础达到入门级水平。零基础意味着你不需要太多的数学知识，只要会写程序就行了，没错，这是专门为程序员写的文章。虽然文中会有很多公式你也许看不懂，但同时也会有更多的代码，程序员的你一定能看懂的（我周围是一群狂热的Clean Code程序员，所以我写的代码也不会很差）。</p>
</blockquote><div class="md-section-divider"></div><h2 data-anchor-id="tct5" id="文章列表">文章列表</h2><p data-anchor-id="39pi"><a href="https://www.zybuluo.com/hanbingtao/note/433855" target="_blank">零基础入门深度学习(1) - 感知器</a> <br>
<a href="https://www.zybuluo.com/hanbingtao/note/448086" target="_blank">零基础入门深度学习(2) - 线性单元和梯度下降</a> <br>
<a href="https://www.zybuluo.com/hanbingtao/note/476663" target="_blank">零基础入门深度学习(3) - 神经网络和反向传播算法</a> <br>
<a href="https://www.zybuluo.com/hanbingtao/note/485480" target="_blank">零基础入门深度学习(4) - 卷积神经网络</a> <br>
<a href="https://zybuluo.com/hanbingtao/note/541458" target="_blank">零基础入门深度学习(5) - 循环神经网络</a> <br>
<a href="https://zybuluo.com/hanbingtao/note/581764" target="_blank">零基础入门深度学习(6) - 长短时记忆网络(LSTM)</a> <br>
<a href="https://zybuluo.com/hanbingtao/note/626300" target="_blank">零基础入门深度学习(7) - 递归神经网络</a></p><div class="md-section-divider"></div><h2 data-anchor-id="p3bc" id="深度学习是啥">深度学习是啥</h2><p data-anchor-id="ij0c">在人工智能领域，有一个方法叫机器学习。在机器学习这个方法里，有一类算法叫神经网络。神经网络如下图所示：</p><p data-anchor-id="bm8i"><img src="http://upload-images.jianshu.io/upload_images/2256672-c6f640c11a06ac2e.png" alt="" title=""></p><p data-anchor-id="l9z0">上图中每个圆圈都是一个神经元，每条线表示神经元之间的连接。我们可以看到，上面的神经元被分成了多层，层与层之间的神经元有连接，而层内之间的神经元没有连接。最左边的层叫做<strong>输入层</strong>，这层负责接收输入数据；最右边的层叫<strong>输出层</strong>，我们可以从这层获取神经网络输出数据。输入层和输出层之间的层叫做<strong>隐藏层</strong>。</p><p data-anchor-id="s1bw">隐藏层比较多（大于2）的神经网络叫做深度神经网络。而深度学习，就是使用深层架构（比如，深度神经网络）的机器学习方法。</p><p data-anchor-id="t4bg">那么深层网络和浅层网络相比有什么优势呢？简单来说深层网络能够表达力更强。事实上，一个仅有一个隐藏层的神经网络就能拟合任何一个函数，但是它需要很多很多的神经元。而深层网络用少得多的神经元就能拟合同样的函数。也就是为了拟合一个函数，要么使用一个浅而宽的网络，要么使用一个深而窄的网络。而后者往往更节约资源。</p><p data-anchor-id="szvi">深层网络也有劣势，就是它不太容易训练。简单的说，你需要大量的数据，很多的技巧才能训练好一个深层网络。这是个手艺活。</p><div class="md-section-divider"></div><h2 data-anchor-id="r9m3" id="感知器">感知器</h2><p data-anchor-id="6ag5">看到这里，如果你还是一头雾水，那也是很正常的。为了理解神经网络，我们应该先理解神经网络的组成单元——<strong>神经元</strong>。神经元也叫做<strong>感知器</strong>。感知器算法在上个世纪50-70年代很流行，也成功解决了很多问题。并且，感知器算法也是非常简单的。</p><div class="md-section-divider"></div><h3 data-anchor-id="k7nn" id="感知器的定义">感知器的定义</h3><p data-anchor-id="tf0a">下图是一个感知器：</p><p data-anchor-id="ijil"><img src="http://upload-images.jianshu.io/upload_images/2256672-801d65e79bfc3162.png" alt="" title=""></p><p data-anchor-id="y0ke">可以看到，一个感知器有如下组成部分：</p><ul data-anchor-id="3svx">
<li><p><strong>输入权值</strong> 一个感知器可以接收多个输入<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-1-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -770.2000693679926 10402.348014081319 1040.4001387359851" style="width: 24.194ex; height: 2.419ex; vertical-align: -0.726ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28"></use><g transform="translate(389,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="809" y="-213"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2C" x="1415" y="0"></use><g transform="translate(1861,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-32" x="809" y="-213"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2C" x="2887" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2E" x="3332" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2E" x="3777" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2E" x="4222" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2C" x="4668" y="0"></use><g transform="translate(5113,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-6E" x="809" y="-213"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2223" x="6488" y="0"></use><g transform="translate(7044,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-69" x="809" y="-213"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2208" x="8239" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJFRAK-52" x="9184" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="10012" y="0"></use></g></svg></span><script type="math/tex" id="MathJax-Element-1">(x_1, x_2,...,x_n\mid x_i\in\Re)</script>，每个输入上有一个<strong>权值</strong><span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-2-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -706.2000693679926 3112.3609484555077 883.8854201102238" style="width: 7.258ex; height: 2.056ex; vertical-align: -0.484ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-77"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-69" x="1013" y="-213"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2208" x="1338" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJFRAK-52" x="2283" y="0"></use></g></svg></span><script type="math/tex" id="MathJax-Element-2">w_i\in\Re</script>，此外还有一个<strong>偏置项</strong><span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-3-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -714.2000693679926 2481.0555555555557 775.4001387359851" style="width: 5.806ex; height: 1.815ex; vertical-align: -0.242ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-62"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2208" x="707" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJFRAK-52" x="1652" y="0"></use></g></svg></span><script type="math/tex" id="MathJax-Element-3">b\in\Re</script>，就是上图中的<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-4-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -463.20006936799257 1170.406943983867 648.6635947032757" style="width: 2.661ex; height: 1.452ex; vertical-align: -0.484ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-77"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30" x="1013" y="-213"></use></g></svg></span><script type="math/tex" id="MathJax-Element-4">w_0</script>。</p></li>
<li><p><strong>激活函数</strong> 感知器的激活函数可以有很多选择，比如我们可以选择下面这个<strong>阶跃函数</strong><span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-5-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -725.2000693679926 550.5 950.4001387359851" style="width: 1.331ex; height: 2.177ex; vertical-align: -0.605ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-66"></use></g></svg></span><script type="math/tex" id="MathJax-Element-5">f</script>来作为激活函数：</p></li>
</ul><div class="md-section-divider"></div><p data-anchor-id="19qi"><span class="MathJax_Preview"></span><div class="MathJax_SVG_Display" role="textbox" aria-readonly="true" style="text-align: center;"><span class="MathJax_SVG" id="MathJax-Element-6-Frame" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -1469.7000693679925 45885.250887096765 2439.400138735985" style="width: 106.573ex; height: 5.685ex; vertical-align: -2.298ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><g transform="translate(17595,0)"><g transform="translate(-15,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-66"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28" x="550" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-7A" x="940" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="1408" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D" x="2075" y="0"></use><g transform="translate(3132,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJSZ3-7B"></use><g transform="translate(917,0)"><g transform="translate(-15,0)"><g transform="translate(0,550)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-7A" x="2500" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3E" x="3246" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30" x="4303" y="0"></use></g><g transform="translate(0,-650)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-6F" x="2500" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-74" x="2986" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-68" x="3347" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-65" x="3924" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-72" x="4390" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-77" x="4842" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-69" x="5558" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-73" x="5904" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-65" x="6373" y="0"></use></g></g></g></g></g></g><g transform="translate(43805,0)"><g id="mjx-eqn-1"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="389" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="890" y="0"></use></g></g></g></svg></span></div><script type="math/tex; mode=display" id="MathJax-Element-6">
f(z)=\begin{equation}\begin{cases}1\qquad z>0\\0\qquad otherwise\end{cases}\end{equation}
</script></p><ul data-anchor-id="mqrd">
<li><strong>输出</strong> 感知器的输出由下面这个公式来计算</li>
</ul><div class="md-section-divider"></div><p data-anchor-id="e47i"><span class="MathJax_Preview"></span><div class="MathJax_SVG_Display" role="textbox" aria-readonly="true" style="text-align: center;"><span class="MathJax_SVG" id="MathJax-Element-7-Frame" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -904.613537109928 11955.605089605735 1288.3956226069529" style="width: 27.823ex; height: 3.024ex; vertical-align: -0.968ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-79"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D" x="775" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-66" x="1831" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28" x="2382" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-77" x="2771" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2219" x="3716" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-78" x="4439" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2B" x="5189" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-62" x="6190" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="6619" y="0"></use><g transform="translate(9009,0)"><text font-family="STIXGeneral,'Arial Unicode MS',serif" font-style="" font-weight="" stroke="none" transform="scale(52.08314516129032) matrix(1 0 0 -1 0 0)">公</text></g><g transform="translate(9842,0)"><text font-family="STIXGeneral,'Arial Unicode MS',serif" font-style="" font-weight="" stroke="none" transform="scale(52.08314516129032) matrix(1 0 0 -1 0 0)">式</text></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28" x="10676" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="11065" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="11566" y="0"></use></g></svg></span></div><script type="math/tex; mode=display" id="MathJax-Element-7">
y=f(\mathrm{w}\bullet\mathrm{x}+b)\qquad 公式(1)
</script> </p><p data-anchor-id="mfpj">如果看完上面的公式一下子就晕了，不要紧，我们用一个简单的例子来帮助理解。</p><div class="md-section-divider"></div><h4 data-anchor-id="uwb5" id="例子用感知器实现and函数">例子：用感知器实现<code>and</code>函数</h4><p data-anchor-id="9ro9">我们设计一个感知器，让它来实现<code>and</code>运算。程序员都知道，<code>and</code>是一个二元函数（带有两个参数<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-8-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -462.20006936799257 1026.406943983867 632.1072455171717" style="width: 2.419ex; height: 1.452ex; vertical-align: -0.484ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="809" y="-213"></use></g></svg></span><script type="math/tex" id="MathJax-Element-8">x_1</script>和<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-9-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -462.20006936799257 1026.406943983867 632.1072455171717" style="width: 2.419ex; height: 1.452ex; vertical-align: -0.484ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-32" x="809" y="-213"></use></g></svg></span><script type="math/tex" id="MathJax-Element-9">x_2</script>），下面是它的<strong>真值表</strong>：</p><table data-anchor-id="o8fw" class="table table-striped-white table-bordered">
<thead>
<tr>
 <th><span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-10-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -462.20006936799257 1026.406943983867 632.1072455171717" style="width: 2.419ex; height: 1.452ex; vertical-align: -0.484ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="809" y="-213"></use></g></svg></span><script type="math/tex" id="MathJax-Element-10">x_1</script></th>
 <th><span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-11-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -462.20006936799257 1026.406943983867 632.1072455171717" style="width: 2.419ex; height: 1.452ex; vertical-align: -0.484ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-32" x="809" y="-213"></use></g></svg></span><script type="math/tex" id="MathJax-Element-11">x_2</script></th>
 <th><span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-12-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -463.20006936799257 497.5 688.4001387359851" style="width: 1.21ex; height: 1.573ex; vertical-align: -0.605ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-79"></use></g></svg></span><script type="math/tex" id="MathJax-Element-12">y</script></th>
</tr>
</thead>
<tbody><tr>
 <td>0</td>
 <td>0</td>
 <td>0</td>
</tr>
<tr>
 <td>0</td>
 <td>1</td>
 <td>0</td>
</tr>
<tr>
 <td>1</td>
 <td>0</td>
 <td>0</td>
</tr>
<tr>
 <td>1</td>
 <td>1</td>
 <td>1</td>
</tr>
</tbody></table><p data-anchor-id="b6m3">为了计算方便，我们用0表示<strong>false</strong>，用1表示<strong>true</strong>。这没什么难理解的，对于C语言程序员来说，这是天经地义的。</p><p data-anchor-id="arbf">我们令<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-13-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -714.2000693679926 12279.813887967732 928.4001387359851" style="width: 28.548ex; height: 2.177ex; vertical-align: -0.605ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-77"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="1013" y="-213"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D" x="1448" y="0"></use><g transform="translate(2504,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2E" x="500" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-35" x="779" y="0"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3B" x="3783" y="0"></use><g transform="translate(4229,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-77"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-32" x="1013" y="-213"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D" x="5677" y="0"></use><g transform="translate(6733,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2E" x="500" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-35" x="779" y="0"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3B" x="8013" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-62" x="8458" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D" x="9165" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2212" x="10221" y="0"></use><g transform="translate(11000,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2E" x="500" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-38" x="779" y="0"></use></g></g></svg></span><script type="math/tex" id="MathJax-Element-13">w_1=0.5;w_2=0.5;b=-0.8</script>，而激活函数<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-14-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -725.2000693679926 550.5 950.4001387359851" style="width: 1.331ex; height: 2.177ex; vertical-align: -0.605ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-66"></use></g></svg></span><script type="math/tex" id="MathJax-Element-14">f</script>就是前面写出来的<strong>阶跃函数</strong>，这时，感知器就相当于<code>and</code>函数。不明白？我们验算一下：</p><p data-anchor-id="6w5u">输入上面真值表的第一行，即<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-15-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -686.2000693679926 6167.091665745511 900.4001387359851" style="width: 14.274ex; height: 2.056ex; vertical-align: -0.605ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="809" y="-213"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D" x="1304" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30" x="2360" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3B" x="2860" y="0"></use><g transform="translate(3306,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-32" x="809" y="-213"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D" x="4610" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30" x="5666" y="0"></use></g></svg></span><script type="math/tex" id="MathJax-Element-15">x_1=0;x_2=0</script>，那么根据公式(1)，计算输出： <br>
<span class="MathJax_Preview"></span><div class="MathJax_SVG_Display" role="textbox" aria-readonly="true" style="text-align: center;"><span class="MathJax_SVG" id="MathJax-Element-16-Frame" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -3398.7000693679925 45885.250887096765 6297.400138735985" style="width: 106.573ex; height: 14.637ex; vertical-align: -6.774ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><g transform="translate(16670,0)"><g transform="translate(-15,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-79" x="0" y="2579"></use></g><g transform="translate(761,0)"><g transform="translate(0,2579)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-66" x="1056" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28" x="1606" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-77" x="1996" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2219" x="2941" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-78" x="3663" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2B" x="4414" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-62" x="5415" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="5844" y="0"></use></g><g transform="translate(0,1277)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-66" x="1056" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28" x="1606" y="0"></use><g transform="translate(1996,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-77"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="1013" y="-213"></use></g><g transform="translate(3166,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="809" y="-213"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2B" x="4415" y="0"></use><g transform="translate(5416,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-77"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-32" x="1013" y="-213"></use></g><g transform="translate(6586,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-32" x="809" y="-213"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2B" x="7835" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-62" x="8835" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="9265" y="0"></use></g><g transform="translate(0,-25)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-66" x="1056" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28" x="1606" y="0"></use><g transform="translate(1996,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2E" x="500" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-35" x="779" y="0"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-D7" x="3498" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30" x="4498" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2B" x="5221" y="0"></use><g transform="translate(6222,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2E" x="500" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-35" x="779" y="0"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-D7" x="7723" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30" x="8724" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2212" x="9447" y="0"></use><g transform="translate(10448,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2E" x="500" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-38" x="779" y="0"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="11727" y="0"></use></g><g transform="translate(0,-1327)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-66" x="1056" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28" x="1606" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2212" x="1996" y="0"></use><g transform="translate(2774,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2E" x="500" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-38" x="779" y="0"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="4054" y="0"></use></g><g transform="translate(0,-2629)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30" x="1056" y="0"></use></g></g></g><g transform="translate(43805,0)"><g transform="translate(0,2579)"><g id="mjx-eqn-2"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-32" x="389" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="890" y="0"></use></g></g><g transform="translate(0,1277)"><g id="mjx-eqn-3"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-33" x="389" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="890" y="0"></use></g></g><g transform="translate(0,-25)"><g id="mjx-eqn-4"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-34" x="389" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="890" y="0"></use></g></g><g transform="translate(0,-1327)"><g id="mjx-eqn-5"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-35" x="389" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="890" y="0"></use></g></g><g transform="translate(0,-2629)"><g id="mjx-eqn-6"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-36" x="389" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="890" y="0"></use></g></g></g></g></svg></span></div><script type="math/tex; mode=display" id="MathJax-Element-16">
\begin{align}
y&=f(\mathrm{w}\bullet\mathrm{x}+b)\\
&=f(w_1x_1+w_2x_2+b)\\
&=f(0.5\times0+0.5\times0-0.8)\\
&=f(-0.8)\\
&=0
\end{align}
</script> <br>
也就是当<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-17-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -462.20006936799257 1026.406943983867 632.1072455171717" style="width: 2.419ex; height: 1.452ex; vertical-align: -0.484ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="809" y="-213"></use></g></svg></span><script type="math/tex" id="MathJax-Element-17">x_1</script><span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-18-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -462.20006936799257 1026.406943983867 632.1072455171717" style="width: 2.419ex; height: 1.452ex; vertical-align: -0.484ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-32" x="809" y="-213"></use></g></svg></span><script type="math/tex" id="MathJax-Element-18">x_2</script>都为0的时候，<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-19-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -463.20006936799257 497.5 688.4001387359851" style="width: 1.21ex; height: 1.573ex; vertical-align: -0.605ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-79"></use></g></svg></span><script type="math/tex" id="MathJax-Element-19">y</script>为0，这就是<strong>真值表</strong>的第一行。读者可以自行验证上述真值表的第二、三、四行。</p><div class="md-section-divider"></div><h4 data-anchor-id="xkok" id="例子用感知器实现or函数">例子：用感知器实现<code>or</code>函数</h4><p data-anchor-id="csvj">同样，我们也可以用感知器来实现<code>or</code>运算。仅仅需要把偏置项<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-20-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -714.2000693679926 429.5 745.4001387359851" style="width: 0.968ex; height: 1.694ex; vertical-align: -0.121ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-62"></use></g></svg></span><script type="math/tex" id="MathJax-Element-20">b</script>的值设置为-0.3就可以了。我们验算一下，下面是<code>or</code>运算的<strong>真值表</strong>：</p><table data-anchor-id="c02l" class="table table-striped-white table-bordered">
<thead>
<tr>
 <th><span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-21-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -462.20006936799257 1026.406943983867 632.1072455171717" style="width: 2.419ex; height: 1.452ex; vertical-align: -0.484ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="809" y="-213"></use></g></svg></span><script type="math/tex" id="MathJax-Element-21">x_1</script></th>
 <th><span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-22-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -462.20006936799257 1026.406943983867 632.1072455171717" style="width: 2.419ex; height: 1.452ex; vertical-align: -0.484ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-32" x="809" y="-213"></use></g></svg></span><script type="math/tex" id="MathJax-Element-22">x_2</script></th>
 <th><span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-23-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -463.20006936799257 497.5 688.4001387359851" style="width: 1.21ex; height: 1.573ex; vertical-align: -0.605ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-79"></use></g></svg></span><script type="math/tex" id="MathJax-Element-23">y</script></th>
</tr>
</thead>
<tbody><tr>
 <td>0</td>
 <td>0</td>
 <td>0</td>
</tr>
<tr>
 <td>0</td>
 <td>1</td>
 <td>1</td>
</tr>
<tr>
 <td>1</td>
 <td>0</td>
 <td>1</td>
</tr>
<tr>
 <td>1</td>
 <td>1</td>
 <td>1</td>
</tr>
</tbody></table><p data-anchor-id="w0ao">我们来验算第二行，这时的输入是<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-24-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -686.2000693679926 6167.091665745511 900.4001387359851" style="width: 14.274ex; height: 2.056ex; vertical-align: -0.605ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="809" y="-213"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D" x="1304" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30" x="2360" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3B" x="2860" y="0"></use><g transform="translate(3306,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-32" x="809" y="-213"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D" x="4610" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="5666" y="0"></use></g></svg></span><script type="math/tex" id="MathJax-Element-24">x_1=0;x_2=1</script>，带入公式(1)：</p><div class="md-section-divider"></div><p data-anchor-id="tx74"><span class="MathJax_Preview"></span><div class="MathJax_SVG_Display" role="textbox" aria-readonly="true" style="text-align: center;"><span class="MathJax_SVG" id="MathJax-Element-25-Frame" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -3398.7000693679925 45885.250887096765 6297.400138735985" style="width: 106.573ex; height: 14.637ex; vertical-align: -6.774ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><g transform="translate(16670,0)"><g transform="translate(-15,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-79" x="0" y="2579"></use></g><g transform="translate(761,0)"><g transform="translate(0,2579)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-66" x="1056" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28" x="1606" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-77" x="1996" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2219" x="2941" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-78" x="3663" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2B" x="4414" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-62" x="5415" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="5844" y="0"></use></g><g transform="translate(0,1277)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-66" x="1056" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28" x="1606" y="0"></use><g transform="translate(1996,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-77"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="1013" y="-213"></use></g><g transform="translate(3166,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="809" y="-213"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2B" x="4415" y="0"></use><g transform="translate(5416,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-77"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-32" x="1013" y="-213"></use></g><g transform="translate(6586,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-32" x="809" y="-213"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2B" x="7835" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-62" x="8835" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="9265" y="0"></use></g><g transform="translate(0,-25)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-66" x="1056" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28" x="1606" y="0"></use><g transform="translate(1996,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2E" x="500" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-35" x="779" y="0"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-D7" x="3498" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="4498" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2B" x="5221" y="0"></use><g transform="translate(6222,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2E" x="500" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-35" x="779" y="0"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-D7" x="7723" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30" x="8724" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2212" x="9447" y="0"></use><g transform="translate(10448,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2E" x="500" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-33" x="779" y="0"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="11727" y="0"></use></g><g transform="translate(0,-1327)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-66" x="1056" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28" x="1606" y="0"></use><g transform="translate(1996,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2E" x="500" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-32" x="779" y="0"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="3275" y="0"></use></g><g transform="translate(0,-2629)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="1056" y="0"></use></g></g></g><g transform="translate(43305,0)"><g transform="translate(500,2579)"><g id="mjx-eqn-7"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-37" x="389" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="890" y="0"></use></g></g><g transform="translate(500,1277)"><g id="mjx-eqn-8"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-38" x="389" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="890" y="0"></use></g></g><g transform="translate(500,-25)"><g id="mjx-eqn-9"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-39" x="389" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="890" y="0"></use></g></g><g transform="translate(0,-1327)"><g id="mjx-eqn-10"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="389" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30" x="890" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="1390" y="0"></use></g></g><g transform="translate(0,-2629)"><g id="mjx-eqn-11"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="389" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="890" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="1390" y="0"></use></g></g></g></g></svg></span></div><script type="math/tex; mode=display" id="MathJax-Element-25">
\begin{align}
y&=f(\mathrm{w}\bullet\mathrm{x}+b)\\
&=f(w_1x_1+w_2x_2+b)\\
&=f(0.5\times1+0.5\times0-0.3)\\
&=f(0.2)\\
&=1
\end{align}
</script></p><p data-anchor-id="jb25">也就是当<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-26-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -686.2000693679926 6167.091665745511 900.4001387359851" style="width: 14.274ex; height: 2.056ex; vertical-align: -0.605ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="809" y="-213"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D" x="1304" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-30" x="2360" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3B" x="2860" y="0"></use><g transform="translate(3306,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-32" x="809" y="-213"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D" x="4610" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="5666" y="0"></use></g></svg></span><script type="math/tex" id="MathJax-Element-26">x_1=0;x_2=1</script>时，<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-27-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -463.20006936799257 497.5 688.4001387359851" style="width: 1.21ex; height: 1.573ex; vertical-align: -0.605ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-79"></use></g></svg></span><script type="math/tex" id="MathJax-Element-27">y</script>为1，即<code>or</code><strong>真值表</strong>第二行。读者可以自行验证其它行。</p><div class="md-section-divider"></div><h3 data-anchor-id="6dzj" id="感知器还能做什么">感知器还能做什么</h3><p data-anchor-id="tye7">事实上，感知器不仅仅能实现简单的布尔运算。它可以拟合任何的线性函数，任何<strong>线性分类</strong>或<strong>线性回归</strong>问题都可以用感知器来解决。前面的布尔运算可以看作是<strong>二分类</strong>问题，即给定一个输入，输出0（属于分类0）或1（属于分类1）。如下面所示，<code>and</code>运算是一个线性分类问题，即可以用一条直线把分类0（false，红叉表示）和分类1（true，绿点表示）分开。</p><p data-anchor-id="4kw6"><img src="http://upload-images.jianshu.io/upload_images/2256672-acff576747ef4259.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/360" alt="" title=""></p><p data-anchor-id="g2i2">然而，感知器却不能实现异或运算，如下图所示，异或运算不是线性的，你无法用一条直线把分类0和分类1分开。</p><p data-anchor-id="m7df"><img src="http://upload-images.jianshu.io/upload_images/2256672-9b651d237936781c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/360" alt="" title=""></p><div class="md-section-divider"></div><h3 data-anchor-id="7loz" id="感知器的训练">感知器的训练</h3><p data-anchor-id="lffc">现在，你可能困惑前面的权重项和偏置项的值是如何获得的呢？这就要用到感知器训练算法：将权重项和偏置项初始化为0，然后，利用下面的<strong>感知器规则</strong>迭代的修改<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-28-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -463.20006936799257 1060.805392899952 640.8854201102238" style="width: 2.419ex; height: 1.452ex; vertical-align: -0.484ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-77"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-69" x="1013" y="-213"></use></g></svg></span><script type="math/tex" id="MathJax-Element-28">w_i</script>和<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-29-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -714.2000693679926 429.5 745.4001387359851" style="width: 0.968ex; height: 1.694ex; vertical-align: -0.121ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-62"></use></g></svg></span><script type="math/tex" id="MathJax-Element-29">b</script>，直到训练完成。</p><div class="md-section-divider"></div><p data-anchor-id="2b83"><span class="MathJax_Preview"></span><div class="MathJax_SVG_Display" role="textbox" aria-readonly="true" style="text-align: center;"><span class="MathJax_SVG" id="MathJax-Element-30-Frame" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -1445.7000693679925 45885.250887096765 2391.400138735985" style="width: 106.573ex; height: 5.565ex; vertical-align: -2.298ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><g transform="translate(19719,0)"><g transform="translate(-15,0)"><g transform="translate(0,626)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-77"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-69" x="1013" y="-213"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-62" x="631" y="-676"></use></g><g transform="translate(1324,0)"><g transform="translate(0,626)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2190"></use><g transform="translate(1278,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-77"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-69" x="1013" y="-213"></use></g><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2B" x="2561" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-394" x="3562" y="0"></use><g transform="translate(4395,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-77"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-69" x="1013" y="-213"></use></g></g><g transform="translate(0,-676)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2190"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-62" x="1278" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2B" x="1930" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-394" x="2930" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-62" x="3764" y="0"></use></g></g></g><g transform="translate(43305,0)"><g transform="translate(0,626)"><g id="mjx-eqn-12"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="389" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-32" x="890" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="1390" y="0"></use></g></g><g transform="translate(0,-676)"><g id="mjx-eqn-13"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="389" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-33" x="890" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="1390" y="0"></use></g></g></g></g></svg></span></div><script type="math/tex; mode=display" id="MathJax-Element-30">
\begin{align}
w_i&\gets w_i+\Delta w_i \\
b&\gets b+\Delta b
\end{align}
</script></p><p data-anchor-id="61qw">其中: <br>
<span class="MathJax_Preview"></span><div class="MathJax_SVG_Display" role="textbox" aria-readonly="true" style="text-align: center;"><span class="MathJax_SVG" id="MathJax-Element-31-Frame" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -1445.7000693679925 45885.250887096765 2391.400138735985" style="width: 106.573ex; height: 5.565ex; vertical-align: -2.298ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><g transform="translate(19361,0)"><g transform="translate(-15,0)"><g transform="translate(0,626)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-394"></use><g transform="translate(833,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-77"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-69" x="1013" y="-213"></use></g></g><g transform="translate(631,-676)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-394"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-62" x="833" y="0"></use></g></g><g transform="translate(2157,0)"><g transform="translate(0,626)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-3B7" x="1056" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28" x="1559" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-74" x="1949" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2212" x="2533" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-79" x="3533" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="4031" y="0"></use><g transform="translate(4420,0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-69" x="809" y="-213"></use></g></g><g transform="translate(0,-676)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-3D"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-3B7" x="1056" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28" x="1559" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-74" x="1949" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-2212" x="2533" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-79" x="3533" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="4031" y="0"></use></g></g></g><g transform="translate(43305,0)"><g transform="translate(0,626)"><g id="mjx-eqn-14"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="389" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-34" x="890" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="1390" y="0"></use></g></g><g transform="translate(0,-676)"><g id="mjx-eqn-15"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-28"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-31" x="389" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-35" x="890" y="0"></use><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-29" x="1390" y="0"></use></g></g></g></g></svg></span></div><script type="math/tex; mode=display" id="MathJax-Element-31">
\begin{align}
\Delta w_i&=\eta(t-y)x_i \\
\Delta b&=\eta(t-y)
\end{align}
</script></p><p data-anchor-id="j7tk"><span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-32-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -463.20006936799257 1060.805392899952 640.8854201102238" style="width: 2.419ex; height: 1.452ex; vertical-align: -0.484ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-77"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-69" x="1013" y="-213"></use></g></svg></span><script type="math/tex" id="MathJax-Element-32">w_i</script>是与输入<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-33-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -462.20006936799257 916.8053928999522 639.8854201102238" style="width: 2.177ex; height: 1.452ex; vertical-align: -0.484ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-69" x="809" y="-213"></use></g></svg></span><script type="math/tex" id="MathJax-Element-33">x_i</script>对应的权重项，<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-34-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -714.2000693679926 429.5 745.4001387359851" style="width: 0.968ex; height: 1.694ex; vertical-align: -0.121ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-62"></use></g></svg></span><script type="math/tex" id="MathJax-Element-34">b</script>是偏置项。事实上，可以把<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-35-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -714.2000693679926 429.5 745.4001387359851" style="width: 0.968ex; height: 1.694ex; vertical-align: -0.121ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-62"></use></g></svg></span><script type="math/tex" id="MathJax-Element-35">b</script>看作是值永远为1的输入<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-36-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -462.20006936799257 976.2023625196222 639.8854201102238" style="width: 2.298ex; height: 1.452ex; vertical-align: -0.484ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-78"></use><use transform="scale(0.7071067811865476)" xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-62" x="809" y="-213"></use></g></svg></span><script type="math/tex" id="MathJax-Element-36">x_b</script>所对应的权重。<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-37-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -646.2000693679926 361.5 677.4001387359851" style="width: 0.847ex; height: 1.573ex; vertical-align: -0.121ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-74"></use></g></svg></span><script type="math/tex" id="MathJax-Element-37">t</script>是训练样本的<strong>实际值</strong>，一般称之为<strong>label</strong>。而<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-38-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -463.20006936799257 497.5 688.4001387359851" style="width: 1.21ex; height: 1.573ex; vertical-align: -0.605ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-79"></use></g></svg></span><script type="math/tex" id="MathJax-Element-38">y</script>是感知器的输出值，它是根据<strong>公式(1)</strong>计算得出。<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-39-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -463.20006936799257 503.5 699.4001387359851" style="width: 1.21ex; height: 1.573ex; vertical-align: -0.605ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-3B7"></use></g></svg></span><script type="math/tex" id="MathJax-Element-39">\eta</script>是一个称为<strong>学习速率</strong>的常数，其作用是控制每一步调整权的幅度。</p><p data-anchor-id="jd8j">每次从训练数据中取出一个样本的输入向量<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-40-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -451.20006936799257 528.5 471.40013873598514" style="width: 1.21ex; height: 1.089ex; vertical-align: -0.121ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMAIN-78"></use></g></svg></span><script type="math/tex" id="MathJax-Element-40">\mathrm{x}</script>，使用感知器计算其输出<span class="MathJax_Preview"></span><span class="MathJax_SVG" id="MathJax-Element-41-Frame" role="textbox" aria-readonly="true" style="font-size: 100%; display: inline-block;"><svg xmlns:xlink="http://www.w3.org/1999/xlink" viewBox="0 -463.20006936799257 497.5 688.4001387359851" style="width: 1.21ex; height: 1.573ex; vertical-align: -0.605ex; margin: 1px 0px;"><g stroke="black" fill="black" stroke-width="0" transform="matrix(1 0 0 -1 0 0)"><use xmlns:xlink="http://www.w3.org/1999/xlink" xlink:href="#MJMATHI-79"></use></g></svg></span><script type="math/tex" id="MathJax-Element-41">y</script>，再根据上面的规则来调整权重。每处理一个样本就调整一次权重。经过多轮迭代后（即全部的训练数据被反复处理多轮），就可以训练出感知器的权重，使之实现目标函数。</p><div class="md-section-divider"></div><h3 data-anchor-id="3rtk" id="编程实战实现感知器">编程实战：实现感知器</h3><blockquote data-anchor-id="iudd" class="white-blockquote">
  <p>完整代码请参考GitHub: <a href="https://github.com/hanbt/learn_dl/blob/master/perceptron.py" target="_blank">https://github.com/hanbt/learn_dl/blob/master/perceptron.py</a> (python2.7)</p>
</blockquote><p data-anchor-id="yjjs">对于程序员来说，没有什么比亲自动手实现学得更快了，而且，很多时候一行代码抵得上千言万语。接下来我们就将实现一个感知器。</p><p data-anchor-id="i4zr">下面是一些说明：</p><ul data-anchor-id="9wft">
<li>使用python语言。python在机器学习领域用的很广泛，而且，写python程序真的很轻松。</li>
<li>面向对象编程。面向对象是特别好的管理复杂度的工具，应对复杂问题时，用面向对象设计方法很容易将复杂问题拆解为多个简单问题，从而解救我们的大脑。</li>
<li>没有使用numpy。numpy实现了很多基础算法，对于实现机器学习算法来说是个必备的工具。但为了降低读者理解的难度，下面的代码只用到了基本的python（省去您去学习numpy的时间）。</li>
</ul><p data-anchor-id="5eia">下面是感知器类的实现，非常简单。去掉注释只有27行，而且还包括为了美观（每行不超过60个字符）而增加的很多换行。</p><div class="md-section-divider"></div><pre class="prettyprint linenums prettyprinted" data-anchor-id="pjgg" style=""><ol class="linenums"><li class="L0"><code class="language-python"><span class="kwd">class</span><span class="pln"> </span><span class="typ">Perceptron</span><span class="pun">(</span><span class="pln">object</span><span class="pun">):</span></code></li><li class="L1"><code class="language-python"><span class="pln">    </span><span class="kwd">def</span><span class="pln"> __init__</span><span class="pun">(</span><span class="pln">self</span><span class="pun">,</span><span class="pln"> input_num</span><span class="pun">,</span><span class="pln"> activator</span><span class="pun">):</span></code></li><li class="L2"><code class="language-python"><span class="pln">        </span><span class="str">'''</span></code></li><li class="L3"><code class="language-python"><span class="str">        初始化感知器，设置输入参数的个数，以及激活函数。</span></code></li><li class="L4"><code class="language-python"><span class="str">        激活函数的类型为double -&gt; double</span></code></li><li class="L5"><code class="language-python"><span class="str">        '''</span></code></li><li class="L6"><code class="language-python"><span class="pln">        self</span><span class="pun">.</span><span class="pln">activator </span><span class="pun">=</span><span class="pln"> activator</span></code></li><li class="L7"><code class="language-python"><span class="pln">        </span><span class="com"># 权重向量初始化为0</span></code></li><li class="L8"><code class="language-python"><span class="pln">        self</span><span class="pun">.</span><span class="pln">weights </span><span class="pun">=</span><span class="pln"> </span><span class="pun">[</span><span class="lit">0.0</span><span class="pln"> </span><span class="kwd">for</span><span class="pln"> _ </span><span class="kwd">in</span><span class="pln"> range</span><span class="pun">(</span><span class="pln">input_num</span><span class="pun">)]</span></code></li><li class="L9"><code class="language-python"><span class="pln">        </span><span class="com"># 偏置项初始化为0</span></code></li><li class="L0"><code class="language-python"><span class="pln">        self</span><span class="pun">.</span><span class="pln">bias </span><span class="pun">=</span><span class="pln"> </span><span class="lit">0.0</span></code></li><li class="L1"><code class="language-python"></code></li><li class="L2"><code class="language-python"><span class="pln">    </span><span class="kwd">def</span><span class="pln"> __str__</span><span class="pun">(</span><span class="pln">self</span><span class="pun">):</span></code></li><li class="L3"><code class="language-python"><span class="pln">        </span><span class="str">'''</span></code></li><li class="L4"><code class="language-python"><span class="str">        打印学习到的权重、偏置项</span></code></li><li class="L5"><code class="language-python"><span class="str">        '''</span></code></li><li class="L6"><code class="language-python"><span class="pln">        </span><span class="kwd">return</span><span class="pln"> </span><span class="str">'weights\t:%s\nbias\t:%f\n'</span><span class="pln"> </span><span class="pun">%</span><span class="pln"> </span><span class="pun">(</span><span class="pln">self</span><span class="pun">.</span><span class="pln">weights</span><span class="pun">,</span><span class="pln"> self</span><span class="pun">.</span><span class="pln">bias</span><span class="pun">)</span></code></li><li class="L7"><code class="language-python"></code></li><li class="L8"><code class="language-python"></code></li><li class="L9"><code class="language-python"><span class="pln">    </span><span class="kwd">def</span><span class="pln"> predict</span><span class="pun">(</span><span class="pln">self</span><span class="pun">,</span><span class="pln"> input_vec</span><span class="pun">):</span></code></li><li class="L0"><code class="language-python"><span class="pln">        </span><span class="str">'''</span></code></li><li class="L1"><code class="language-python"><span class="str">        输入向量，输出感知器的计算结果</span></code></li><li class="L2"><code class="language-python"><span class="str">        '''</span></code></li><li class="L3"><code class="language-python"><span class="pln">        </span><span class="com"># 把input_vec[x1,x2,x3...]和weights[w1,w2,w3,...]打包在一起</span></code></li><li class="L4"><code class="language-python"><span class="pln">        </span><span class="com"># 变成[(x1,w1),(x2,w2),(x3,w3),...]</span></code></li><li class="L5"><code class="language-python"><span class="pln">        </span><span class="com"># 然后利用map函数计算[x1*w1, x2*w2, x3*w3]</span></code></li><li class="L6"><code class="language-python"><span class="pln">        </span><span class="com"># 最后利用reduce求和</span></code></li><li class="L7"><code class="language-python"><span class="pln">        </span><span class="kwd">return</span><span class="pln"> self</span><span class="pun">.</span><span class="pln">activator</span><span class="pun">(</span></code></li><li class="L8"><code class="language-python"><span class="pln">            reduce</span><span class="pun">(</span><span class="kwd">lambda</span><span class="pln"> a</span><span class="pun">,</span><span class="pln"> b</span><span class="pun">:</span><span class="pln"> a </span><span class="pun">+</span><span class="pln"> b</span><span class="pun">,</span></code></li><li class="L9"><code class="language-python"><span class="pln">                   map</span><span class="pun">(</span><span class="kwd">lambda</span><span class="pln"> </span><span class="pun">(</span><span class="pln">x</span><span class="pun">,</span><span class="pln"> w</span><span class="pun">):</span><span class="pln"> x </span><span class="pun">*</span><span class="pln"> w</span><span class="pun">,</span><span class="pln">  </span></code></li><li class="L0"><code class="language-python"><span class="pln">                       zip</span><span class="pun">(</span><span class="pln">input_vec</span><span class="pun">,</span><span class="pln"> self</span><span class="pun">.</span><span class="pln">weights</span><span class="pun">))</span></code></li><li class="L1"><code class="language-python"><span class="pln">                </span><span class="pun">,</span><span class="pln"> </span><span class="lit">0.0</span><span class="pun">)</span><span class="pln"> </span><span class="pun">+</span><span class="pln"> self</span><span class="pun">.</span><span class="pln">bias</span><span class="pun">)</span></code></li><li class="L2"><code class="language-python"></code></li><li class="L3"><code class="language-python"><span class="pln">    </span><span class="kwd">def</span><span class="pln"> train</span><span class="pun">(</span><span class="pln">self</span><span class="pun">,</span><span class="pln"> input_vecs</span><span class="pun">,</span><span class="pln"> labels</span><span class="pun">,</span><span class="pln"> iteration</span><span class="pun">,</span><span class="pln"> rate</span><span class="pun">):</span></code></li><li class="L4"><code class="language-python"><span class="pln">        </span><span class="str">'''</span></code></li><li class="L5"><code class="language-python"><span class="str">        输入训练数据：一组向量、与每个向量对应的label；以及训练轮数、学习率</span></code></li><li class="L6"><code class="language-python"><span class="str">        '''</span></code></li><li class="L7"><code class="language-python"><span class="pln">        </span><span class="kwd">for</span><span class="pln"> i </span><span class="kwd">in</span><span class="pln"> range</span><span class="pun">(</span><span class="pln">iteration</span><span class="pun">):</span></code></li><li class="L8"><code class="language-python"><span class="pln">            self</span><span class="pun">.</span><span class="pln">_one_iteration</span><span class="pun">(</span><span class="pln">input_vecs</span><span class="pun">,</span><span class="pln"> labels</span><span class="pun">,</span><span class="pln"> rate</span><span class="pun">)</span></code></li><li class="L9"><code class="language-python"></code></li><li class="L0"><code class="language-python"><span class="pln">    </span><span class="kwd">def</span><span class="pln"> _one_iteration</span><span class="pun">(</span><span class="pln">self</span><span class="pun">,</span><span class="pln"> input_vecs</span><span class="pun">,</span><span class="pln"> labels</span><span class="pun">,</span><span class="pln"> rate</span><span class="pun">):</span></code></li><li class="L1"><code class="language-python"><span class="pln">        </span><span class="str">'''</span></code></li><li class="L2"><code class="language-python"><span class="str">        一次迭代，把所有的训练数据过一遍</span></code></li><li class="L3"><code class="language-python"><span class="str">        '''</span></code></li><li class="L4"><code class="language-python"><span class="pln">        </span><span class="com"># 把输入和输出打包在一起，成为样本的列表[(input_vec, label), ...]</span></code></li><li class="L5"><code class="language-python"><span class="pln">        </span><span class="com"># 而每个训练样本是(input_vec, label)</span></code></li><li class="L6"><code class="language-python"><span class="pln">        samples </span><span class="pun">=</span><span class="pln"> zip</span><span class="pun">(</span><span class="pln">input_vecs</span><span class="pun">,</span><span class="pln"> labels</span><span class="pun">)</span></code></li><li class="L7"><code class="language-python"><span class="pln">        </span><span class="com"># 对每个样本，按照感知器规则更新权重</span></code></li><li class="L8"><code class="language-python"><span class="pln">        </span><span class="kwd">for</span><span class="pln"> </span><span class="pun">(</span><span class="pln">input_vec</span><span class="pun">,</span><span class="pln"> label</span><span class="pun">)</span><span class="pln"> </span><span class="kwd">in</span><span class="pln"> samples</span><span class="pun">:</span></code></li><li class="L9"><code class="language-python"><span class="pln">            </span><span class="com"># 计算感知器在当前权重下的输出</span></code></li><li class="L0"><code class="language-python"><span class="pln">            output </span><span class="pun">=</span><span class="pln"> self</span><span class="pun">.</span><span class="pln">predict</span><span class="pun">(</span><span class="pln">input_vec</span><span class="pun">)</span></code></li><li class="L1"><code class="language-python"><span class="pln">            </span><span class="com"># 更新权重</span></code></li><li class="L2"><code class="language-python"><span class="pln">            self</span><span class="pun">.</span><span class="pln">_update_weights</span><span class="pun">(</span><span class="pln">input_vec</span><span class="pun">,</span><span class="pln"> output</span><span class="pun">,</span><span class="pln"> label</span><span class="pun">,</span><span class="pln"> rate</span><span class="pun">)</span></code></li><li class="L3"><code class="language-python"></code></li><li class="L4"><code class="language-python"><span class="pln">    </span><span class="kwd">def</span><span class="pln"> _update_weights</span><span class="pun">(</span><span class="pln">self</span><span class="pun">,</span><span class="pln"> input_vec</span><span class="pun">,</span><span class="pln"> output</span><span class="pun">,</span><span class="pln"> label</span><span class="pun">,</span><span class="pln"> rate</span><span class="pun">):</span></code></li><li class="L5"><code class="language-python"><span class="pln">        </span><span class="str">'''</span></code></li><li class="L6"><code class="language-python"><span class="str">        按照感知器规则更新权重</span></code></li><li class="L7"><code class="language-python"><span class="str">        '''</span></code></li><li class="L8"><code class="language-python"><span class="pln">        </span><span class="com"># 把input_vec[x1,x2,x3,...]和weights[w1,w2,w3,...]打包在一起</span></code></li><li class="L9"><code class="language-python"><span class="pln">        </span><span class="com"># 变成[(x1,w1),(x2,w2),(x3,w3),...]</span></code></li><li class="L0"><code class="language-python"><span class="pln">        </span><span class="com"># 然后利用感知器规则更新权重</span></code></li><li class="L1"><code class="language-python"><span class="pln">        delta </span><span class="pun">=</span><span class="pln"> label </span><span class="pun">-</span><span class="pln"> output</span></code></li><li class="L2"><code class="language-python"><span class="pln">        self</span><span class="pun">.</span><span class="pln">weights </span><span class="pun">=</span><span class="pln"> map</span><span class="pun">(</span></code></li><li class="L3"><code class="language-python"><span class="pln">            </span><span class="kwd">lambda</span><span class="pln"> </span><span class="pun">(</span><span class="pln">x</span><span class="pun">,</span><span class="pln"> w</span><span class="pun">):</span><span class="pln"> w </span><span class="pun">+</span><span class="pln"> rate </span><span class="pun">*</span><span class="pln"> delta </span><span class="pun">*</span><span class="pln"> x</span><span class="pun">,</span></code></li><li class="L4"><code class="language-python"><span class="pln">            zip</span><span class="pun">(</span><span class="pln">input_vec</span><span class="pun">,</span><span class="pln"> self</span><span class="pun">.</span><span class="pln">weights</span><span class="pun">))</span></code></li><li class="L5"><code class="language-python"><span class="pln">        </span><span class="com"># 更新bias</span></code></li><li class="L6"><code class="language-python"><span class="pln">        self</span><span class="pun">.</span><span class="pln">bias </span><span class="pun">+=</span><span class="pln"> rate </span><span class="pun">*</span><span class="pln"> delta</span></code></li></ol></pre><p data-anchor-id="clua">接下来，我们利用这个感知器类去实现<code>and</code>函数。</p><div class="md-section-divider"></div><pre class="prettyprint linenums prettyprinted" data-anchor-id="l2u0" style=""><ol class="linenums"><li class="L0"><code class="language-python"><span class="kwd">def</span><span class="pln"> f</span><span class="pun">(</span><span class="pln">x</span><span class="pun">):</span></code></li><li class="L1"><code class="language-python"><span class="pln">    </span><span class="str">'''</span></code></li><li class="L2"><code class="language-python"><span class="str">    定义激活函数f</span></code></li><li class="L3"><code class="language-python"><span class="str">    '''</span></code></li><li class="L4"><code class="language-python"><span class="pln">    </span><span class="kwd">return</span><span class="pln"> </span><span class="lit">1</span><span class="pln"> </span><span class="kwd">if</span><span class="pln"> x </span><span class="pun">&gt;</span><span class="pln"> </span><span class="lit">0</span><span class="pln"> </span><span class="kwd">else</span><span class="pln"> </span><span class="lit">0</span></code></li><li class="L5"><code class="language-python"></code></li><li class="L6"><code class="language-python"></code></li><li class="L7"><code class="language-python"><span class="kwd">def</span><span class="pln"> get_training_dataset</span><span class="pun">():</span></code></li><li class="L8"><code class="language-python"><span class="pln">    </span><span class="str">'''</span></code></li><li class="L9"><code class="language-python"><span class="str">    基于and真值表构建训练数据</span></code></li><li class="L0"><code class="language-python"><span class="str">    '''</span></code></li><li class="L1"><code class="language-python"><span class="pln">    </span><span class="com"># 构建训练数据</span></code></li><li class="L2"><code class="language-python"><span class="pln">    </span><span class="com"># 输入向量列表</span></code></li><li class="L3"><code class="language-python"><span class="pln">    input_vecs </span><span class="pun">=</span><span class="pln"> </span><span class="pun">[[</span><span class="lit">1</span><span class="pun">,</span><span class="lit">1</span><span class="pun">],</span><span class="pln"> </span><span class="pun">[</span><span class="lit">0</span><span class="pun">,</span><span class="lit">0</span><span class="pun">],</span><span class="pln"> </span><span class="pun">[</span><span class="lit">1</span><span class="pun">,</span><span class="lit">0</span><span class="pun">],</span><span class="pln"> </span><span class="pun">[</span><span class="lit">0</span><span class="pun">,</span><span class="lit">1</span><span class="pun">]]</span></code></li><li class="L4"><code class="language-python"><span class="pln">    </span><span class="com"># 期望的输出列表，注意要与输入一一对应</span></code></li><li class="L5"><code class="language-python"><span class="pln">    </span><span class="com"># [1,1] -&gt; 1, [0,0] -&gt; 0, [1,0] -&gt; 0, [0,1] -&gt; 0</span></code></li><li class="L6"><code class="language-python"><span class="pln">    labels </span><span class="pun">=</span><span class="pln"> </span><span class="pun">[</span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">]</span></code></li><li class="L7"><code class="language-python"><span class="pln">    </span><span class="kwd">return</span><span class="pln"> input_vecs</span><span class="pun">,</span><span class="pln"> labels    </span></code></li><li class="L8"><code class="language-python"></code></li><li class="L9"><code class="language-python"></code></li><li class="L0"><code class="language-python"><span class="kwd">def</span><span class="pln"> train_and_perceptron</span><span class="pun">():</span></code></li><li class="L1"><code class="language-python"><span class="pln">    </span><span class="str">'''</span></code></li><li class="L2"><code class="language-python"><span class="str">    使用and真值表训练感知器</span></code></li><li class="L3"><code class="language-python"><span class="str">    '''</span></code></li><li class="L4"><code class="language-python"><span class="pln">    </span><span class="com"># 创建感知器，输入参数个数为2（因为and是二元函数），激活函数为f</span></code></li><li class="L5"><code class="language-python"><span class="pln">    p </span><span class="pun">=</span><span class="pln"> </span><span class="typ">Perceptron</span><span class="pun">(</span><span class="lit">2</span><span class="pun">,</span><span class="pln"> f</span><span class="pun">)</span></code></li><li class="L6"><code class="language-python"><span class="pln">    </span><span class="com"># 训练，迭代10轮, 学习速率为0.1</span></code></li><li class="L7"><code class="language-python"><span class="pln">    input_vecs</span><span class="pun">,</span><span class="pln"> labels </span><span class="pun">=</span><span class="pln"> get_training_dataset</span><span class="pun">()</span></code></li><li class="L8"><code class="language-python"><span class="pln">    p</span><span class="pun">.</span><span class="pln">train</span><span class="pun">(</span><span class="pln">input_vecs</span><span class="pun">,</span><span class="pln"> labels</span><span class="pun">,</span><span class="pln"> </span><span class="lit">10</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0.1</span><span class="pun">)</span></code></li><li class="L9"><code class="language-python"><span class="pln">    </span><span class="com">#返回训练好的感知器</span></code></li><li class="L0"><code class="language-python"><span class="pln">    </span><span class="kwd">return</span><span class="pln"> p</span></code></li><li class="L1"><code class="language-python"></code></li><li class="L2"><code class="language-python"></code></li><li class="L3"><code class="language-python"><span class="kwd">if</span><span class="pln"> __name__ </span><span class="pun">==</span><span class="pln"> </span><span class="str">'__main__'</span><span class="pun">:</span><span class="pln"> </span></code></li><li class="L4"><code class="language-python"><span class="pln">    </span><span class="com"># 训练and感知器</span></code></li><li class="L5"><code class="language-python"><span class="pln">    and_perception </span><span class="pun">=</span><span class="pln"> train_and_perceptron</span><span class="pun">()</span></code></li><li class="L6"><code class="language-python"><span class="pln">    </span><span class="com"># 打印训练获得的权重</span></code></li><li class="L7"><code class="language-python"><span class="pln">    </span><span class="kwd">print</span><span class="pln"> and_perception</span></code></li><li class="L8"><code class="language-python"><span class="pln">    </span><span class="com"># 测试</span></code></li><li class="L9"><code class="language-python"><span class="pln">    </span><span class="kwd">print</span><span class="pln"> </span><span class="str">'1 and 1 = %d'</span><span class="pln"> </span><span class="pun">%</span><span class="pln"> and_perception</span><span class="pun">.</span><span class="pln">predict</span><span class="pun">([</span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">])</span></code></li><li class="L0"><code class="language-python"><span class="pln">    </span><span class="kwd">print</span><span class="pln"> </span><span class="str">'0 and 0 = %d'</span><span class="pln"> </span><span class="pun">%</span><span class="pln"> and_perception</span><span class="pun">.</span><span class="pln">predict</span><span class="pun">([</span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">])</span></code></li><li class="L1"><code class="language-python"><span class="pln">    </span><span class="kwd">print</span><span class="pln"> </span><span class="str">'1 and 0 = %d'</span><span class="pln"> </span><span class="pun">%</span><span class="pln"> and_perception</span><span class="pun">.</span><span class="pln">predict</span><span class="pun">([</span><span class="lit">1</span><span class="pun">,</span><span class="pln"> </span><span class="lit">0</span><span class="pun">])</span></code></li><li class="L2"><code class="language-python"><span class="pln">    </span><span class="kwd">print</span><span class="pln"> </span><span class="str">'0 and 1 = %d'</span><span class="pln"> </span><span class="pun">%</span><span class="pln"> and_perception</span><span class="pun">.</span><span class="pln">predict</span><span class="pun">([</span><span class="lit">0</span><span class="pun">,</span><span class="pln"> </span><span class="lit">1</span><span class="pun">])</span></code></li></ol></pre><p data-anchor-id="y2uc">将上述程序保存为perceptron.py文件，通过命令行执行这个程序，其运行结果为：</p><p data-anchor-id="o6n4"><img src="http://upload-images.jianshu.io/upload_images/2256672-1e66158656366b57.png" alt="" title=""></p><p data-anchor-id="ymd7">神奇吧！感知器竟然完全实现了<code>and</code>函数。读者可以尝试一下利用感知器实现其它函数。</p><div class="md-section-divider"></div><h2 data-anchor-id="mj9j" id="小结">小结</h2><p data-anchor-id="nl0f">终于看（写）到小结了...，大家都累了。对于零基础的你来说，走到这里应该已经很烧脑了吧。没关系，休息一下。值得高兴的是，你终于已经走出了深度学习入门的第一步，这是巨大的进步；坏消息是，这仅仅是最简单的部分，后面还有无数艰难险阻等着你。不过，你学的困难往往意味着别人学的也困难，掌握一门高门槛的技艺，进可糊口退可装逼，是很值得的。</p><p data-anchor-id="0lwc">下一篇文章，我们将讨论另外一种感知器：<strong>线性单元</strong>，并由此引出一种可能是最最重要的优化算法：<strong>梯度下降</strong>算法。</p><div class="md-section-divider"></div><h2 data-anchor-id="wc4s" id="参考资料">参考资料</h2><ol data-anchor-id="dct2">
<li>Tom M. Mitchell, "机器学习", 曾华军等译, 机械工业出版社</li>
</ol></div>
    <div class="remark-icons">
    </div>
</div>

<!--in page preview buttons. -->
<div class="in-page-preview-buttons in-page-preview-buttons-full-reader">
    <ul>
        <li class="in-page-button dropdown" id="preview-toc-button" title="内容目录 Ctrl+Alt+O">
            <span class="dropdown-toggle icon-list" data-toggle="dropdown"></span>
            <div id="toc-list" class="dropdown-menu theme pull-right"> <!-- Add theme means this element will be changed when apply theme color. -->
                <h3>内容目录</h3>
                <hr>
                <div class="table-of-contents"></div>
            </div>
        </li>
    </ul>
</div>

<div id="reader-full-toolbar" class="reader-full-toolbar-shown" style="padding-top: 0;">
    <ul id="reader-full-toolbar-home" class="preview-button-row">
        <li class="preview-button-full-reader" id="preview-editor-button" title="撰写文本 Ctrl+Alt+M">
            <span class="icon-pencil"></span>
        </li>
    </ul>
    <ul id="preview-button-row" class="preview-button-row">
        <li class="preview-button-full-reader dropdown" id="preview-list-button" title="文本列表 Ctrl+Alt+F">
            <span class="dropdown-toggle icon-reorder" data-toggle="dropdown"></span>
            <ul id="file-list" class="dropdown-menu theme-black pull-right" role="menu">
                    <li>
                    <ul class="tag-list">
                        <li class="tag-item item" tag-name="机器学习">
                            <span class="pull-left"><i class="icon-tag"></i><span class="tag-name">机器学习</span></span>
                            <span class="tag-count pull-right">7</span>
                            <div class="clearfix"></div>
                        </li>
                            
    <li class="file-item item" file-created-date="2017-02-27T16:59:57.000000Z">
        <a tabindex="-1" href="https://www.zybuluo.com/hanbingtao/note/626300" title="【已发布】 2017-08-29T15:41:15.000000Z">
        <i class="icon-share-sign"></i>
        <span id="626300">零基础入门深度学习(7) - 递归神经网络</span>
        </a>
    </li>

                            
    <li class="file-item item" file-created-date="2017-01-08T15:28:36.000000Z">
        <a tabindex="-1" href="https://www.zybuluo.com/hanbingtao/note/581764" title="【已发布】 2017-08-28T11:55:38.000000Z">
        <i class="icon-share-sign"></i>
        <span id="581764">零基础入门深度学习(6) - 长短时记忆网络(LSTM)</span>
        </a>
    </li>

                            
    <li class="file-item item" file-created-date="2016-11-05T11:16:51.000000Z">
        <a tabindex="-1" href="https://www.zybuluo.com/hanbingtao/note/541458" title="【已发布】 2017-08-28T11:54:33.000000Z">
        <i class="icon-share-sign"></i>
        <span id="541458">零基础入门深度学习(5) - 循环神经网络</span>
        </a>
    </li>

                            
    <li class="file-item item" file-created-date="2016-10-09T12:30:46.000000Z">
        <a tabindex="-1" href="https://www.zybuluo.com/hanbingtao/note/485480" title="【已发布】 2017-08-28T11:53:32.000000Z">
        <i class="icon-share-sign"></i>
        <span id="485480">零基础入门深度学习(4) - 卷积神经网络</span>
        </a>
    </li>

                            
    <li class="file-item item" file-created-date="2016-08-24T13:39:25.000000Z">
        <a tabindex="-1" href="https://www.zybuluo.com/hanbingtao/note/476663" title="【已发布】 2017-10-17T14:25:55.000000Z">
        <i class="icon-share-sign"></i>
        <span id="476663">零基础入门深度学习(3) - 神经网络和反向传播算法</span>
        </a>
    </li>

                            
    <li class="file-item item" file-created-date="2016-07-25T17:44:30.000000Z">
        <a tabindex="-1" href="https://www.zybuluo.com/hanbingtao/note/448086" title="【已发布】 2017-08-28T11:40:02.000000Z">
        <i class="icon-share-sign"></i>
        <span id="448086">零基础入门深度学习(2) - 线性单元和梯度下降</span>
        </a>
    </li>

                            
    <li class="file-item item" file-created-date="2016-07-12T03:10:42.000000Z">
        <a tabindex="-1" href="https://www.zybuluo.com/hanbingtao/note/433855" title="【已发布】 2017-08-28T11:35:23.000000Z">
        <i class="icon-share-sign"></i>
        <span id="433855" class="whiter-on-black">零基础入门深度学习(1) - 感知器</span>
        </a>
    </li>

                    </ul>
                    </li>
                    <li>
                    <ul class="tag-list">
                        <li class="tag-item item" tag-name="深度学习入门">
                            <span class="pull-left"><i class="icon-tag"></i><span class="tag-name">深度学习入门</span></span>
                            <span class="tag-count pull-right">7</span>
                            <div class="clearfix"></div>
                        </li>
                            
    <li class="file-item item" file-created-date="2017-02-27T16:59:57.000000Z">
        <a tabindex="-1" href="https://www.zybuluo.com/hanbingtao/note/626300" title="【已发布】 2017-08-29T15:41:15.000000Z">
        <i class="icon-share-sign"></i>
        <span id="626300">零基础入门深度学习(7) - 递归神经网络</span>
        </a>
    </li>

                            
    <li class="file-item item" file-created-date="2017-01-08T15:28:36.000000Z">
        <a tabindex="-1" href="https://www.zybuluo.com/hanbingtao/note/581764" title="【已发布】 2017-08-28T11:55:38.000000Z">
        <i class="icon-share-sign"></i>
        <span id="581764">零基础入门深度学习(6) - 长短时记忆网络(LSTM)</span>
        </a>
    </li>

                            
    <li class="file-item item" file-created-date="2016-11-05T11:16:51.000000Z">
        <a tabindex="-1" href="https://www.zybuluo.com/hanbingtao/note/541458" title="【已发布】 2017-08-28T11:54:33.000000Z">
        <i class="icon-share-sign"></i>
        <span id="541458">零基础入门深度学习(5) - 循环神经网络</span>
        </a>
    </li>

                            
    <li class="file-item item" file-created-date="2016-10-09T12:30:46.000000Z">
        <a tabindex="-1" href="https://www.zybuluo.com/hanbingtao/note/485480" title="【已发布】 2017-08-28T11:53:32.000000Z">
        <i class="icon-share-sign"></i>
        <span id="485480">零基础入门深度学习(4) - 卷积神经网络</span>
        </a>
    </li>

                            
    <li class="file-item item" file-created-date="2016-08-24T13:39:25.000000Z">
        <a tabindex="-1" href="https://www.zybuluo.com/hanbingtao/note/476663" title="【已发布】 2017-10-17T14:25:55.000000Z">
        <i class="icon-share-sign"></i>
        <span id="476663">零基础入门深度学习(3) - 神经网络和反向传播算法</span>
        </a>
    </li>

                            
    <li class="file-item item" file-created-date="2016-07-25T17:44:30.000000Z">
        <a tabindex="-1" href="https://www.zybuluo.com/hanbingtao/note/448086" title="【已发布】 2017-08-28T11:40:02.000000Z">
        <i class="icon-share-sign"></i>
        <span id="448086">零基础入门深度学习(2) - 线性单元和梯度下降</span>
        </a>
    </li>

                            
    <li class="file-item item" file-created-date="2016-07-12T03:10:42.000000Z">
        <a tabindex="-1" href="https://www.zybuluo.com/hanbingtao/note/433855" title="【已发布】 2017-08-28T11:35:23.000000Z">
        <i class="icon-share-sign"></i>
        <span id="433855" class="whiter-on-black">零基础入门深度学习(1) - 感知器</span>
        </a>
    </li>

                    </ul>
                    </li>
            </ul>
            <ul id="file-list-topbar" class="dropdown-menu theme-black pull-right" role="menu">
                <li id="search-file-bar">
                    <i class="icon-search icon-large"></i>
                    <input type="text" id="search-file-textbox" placeholder="搜索 hanbingtao 的文稿标题， * 显示全部">
                    <i class="icon-level-down icon-rotate-90 icon-large"></i>
                </li>
                <li id="tag-file-bar">
                    以下【标签】将用于标记这篇文稿：
                </li>
            </ul>
        </li>
        <li class="preview-button-full-reader" id="preview-theme-button" title="主题切换 Ctrl+Alt+Y">
            <span class="icon-adjust"></span>
        </li>
        <li class="preview-button-full-reader" id="preview-fullscreen-button" title="全屏模式 F11">
            <span class="icon-fullscreen"></span>
        </li>
        <li class="preview-button-full-reader wmd-spacer"></li>
        <li class="preview-button-full-reader dropdown" id="preview-about-button" title="关于本站">
            <span class="dropdown-toggle icon-info-sign" data-toggle="dropdown" data-hover="dropdown" data-delay="100" data-close-others="true"></span>
            <ul id="about-menu" class="dropdown-menu theme-black pull-right" role="menu">
                <li title="下载全平台客户端"><a tabindex="-1" href="https://www.zybuluo.com/cmd" target="_blank"><i class="icon-laptop"></i>下载客户端</a></li>
                <li title="@ghosert"><a tabindex="-1" href="http://www.weibo.com/ghosert" target="_blank"><i class="icon-weibo"></i>关注开发者</a></li>
                <li title=""><a tabindex="-1" href="https://github.com/ghosert/cmd-editor/issues" target="_blank"><i class="icon-github-alt"></i>报告问题，建议</a></li>
                <li title="support@zybuluo.com"><a tabindex="-1" href="mailto:support@zybuluo.com" target="_blank"><i class="icon-envelope"></i>联系我们</a></li>
            </ul>
        </li>
    </ul>
</div>
<ul id="reader-full-toolbar-tail" class="reader-full-toolbar-tail-shown">
    <li class="preview-button-full-reader" id="preview-hidden-button" title="隐藏工具栏 Ctrl+Alt+I">
        <span class="icon-chevron-sign-right"></span>
    </li>
</ul>






<!-- side remark, hidden when loading. -->
<div class="remark-list side-remark-hidden">
    <div class="remark-items">
    </div>
    <div class="leave-remark unselectable"><span class='icon-plus-sign-alt'></span><span>添加新批注</span></div>
    <div class="new-remark">
        <!-- clone the template $('.new-remark-reply').html() to here.-->
        <div class="remark-notice">在作者公开此批注前，只有你和作者可见。</div>
    </div>
</div>

<!-- template for new remark/reply -->
<div class="new-remark-reply side-remark-hidden">
    <div class="remark-head"><a><img src="https://www.zybuluo.com/static/img/default-head.jpg"></a></div>
    <div class="remark-author unselectable"></div>
    <div class="remark-editor" contentEditable="true" spellcheck="false"></div>
    <!-- this will be filled up by js.
    <div class="inline-error">402/400</div> for new remark
    <div class="inline-error">202/200</div> for new reply
    -->
    <div class="remark-footer unselectable">
        <button class="remark-save btn-link">保存</button>
        <button class="remark-cancel btn-link">取消</button>
    </div>
</div>

<!-- template for .remark-item/.remark-reply -->
<div class="remark-item-reply side-remark-hidden">
    <div class="remark-head"><a><img src="https://www.zybuluo.com/static/img/default-head.jpg"></a></div>
    <div class="remark-author unselectable"></div>
    <div class="remark-delete-link unselectable"><span class="icon-remove"></span></div> <!--This is mainly for deleting remark-reply, shown when author/remark hovering on remark-reply.-->
    <div class="remark-editor" contentEditable="true" spellcheck="false"></div>
    <!-- this will be filled up by js.
    <div class="inline-error">402/400</div> for new remark
    <div class="inline-error">202/200</div> for new reply
    -->
    <div class="remark-footer unselectable">
        <button class="remark-edit btn-link">修改</button>
        <button class="remark-save btn-link">保存</button>
        <button class="remark-cancel btn-link">取消</button>
        <button class="remark-delete btn-link">删除</button>
    </div>
</div>

<!-- template for remark-item-->
<div class="remark-item side-remark-hidden" data-rand-id="" data-version-id="">
    <div class="remark-published-link unselectable"><span class="icon-link icon-rotate-90"></span></div>
    <ul class="remark-options theme unselectable">
        <li class="remark-private"><span class="icon-eye-close"></span><span>私有</span></li>
        <li class="remark-public"><span class="icon-group"></span><span>公开</span></li>
        <li class="remark-delete"><span class="icon-remove"></span><span>删除</span></li>
    </ul>

    <!-- clone the template $('.remark-item-reply').html() to here.-->

    <button class="remark-reply-view-more btn-link">查看更早的 5 条回复</button>
    <div class="remark-replies">
        <!--
        <div class="remark-reply">
            clone the template $('.remark-item-reply').html() to here.
        </div>
        -->
    </div>

    <div class="leave-reply unselectable"><span>回复批注</span></div>
    <div class="new-reply">
        <!-- clone the template $('.new-remark-reply').html() to here.-->
    </div>
</div>

<!-- jiawzhang NOTICE: .remark-icons will be put to mdeditor.mako and user_note.mako, where next to .wmd-preview -->
<!-- <div class="remark-icons"></div> -->

<!-- template for remark-icon -->
<div class="remark-icon unselectable side-remark-hidden remark-icon-empty" style="display: none;">
    <span class="icon-stack">
        <i class="glyph-comment"></i>
        <span class="remark-count"></span>
    </span>
</div>


<!-- canvas, hidden always, this is used to convert svg to canvas and then convert canvas to png. -->
<canvas id="svg-canvas-image" class="editor-reader-hidden-always"></canvas>

<!-- This is the image panel to hold enlarged image/svg. -->
<div id="large-image-panel">
    <img id="large-image"/>
</div>


    


    <!-- Hidden Popup Modal -->
    <div id="notification-popup-window" class="modal hide fade theme" tabindex="-1" role="dialog" aria-labelledby="notification-title" aria-hidden="true">
        <div class="modal-header theme">
            <button type="button" class="close" data-dismiss="modal" aria-hidden="true">×</button>
            <h3 id="notification-title">通知</h3>
        </div>
        <div class="modal-body theme">
            <p></p>
        </div>
        <div class="modal-footer theme">
            <button id="notification-cancel" class="btn" data-dismiss="modal" aria-hidden="true">取消</button>
            <button id="notification-confirm" class="btn btn-primary">确认</button>
        </div>
    </div>

    <!-- zybuluo's foot -->

    <script src="https://www.zybuluo.com/static/assets/288313bb.base.lib.min.js"></script>

    <script>
        Namespace('com.zybuluo.base');
        com.zybuluo.base.initData = {
            globalPromptUrl: "https://www.zybuluo.com/global/prompt",
        };
    </script>

    
    <!--mathjax-->
    <!--blacker: 1 below means font weight.-->
    <script type="text/x-mathjax-config">
        MathJax.Hub.Config({ tex2jax: { inlineMath: [['$','$'], ["\\(","\\)"]], processEscapes: true }, TeX: { equationNumbers: { autoNumber: "AMS" } }, messageStyle: "none", SVG: { blacker: 1 }});
    </script>
    <script src="https://www.zybuluo.com/static/editor/libs/mathJax.js"></script>
    <!--mathjax source code is here: https://github.com/mathjax/MathJax.-->
    <script src="https://www.zybuluo.com/static/MathJax/MathJax.js?config=TeX-AMS-MML_SVG"></script>

    <script>
        Namespace('com.zybuluo.mdeditor.layout');
        com.zybuluo.mdeditor.layout.initData = {
            // '' means not logged in, otherwise the logged in username, for mdeditor.mako, this value will be reset in render.js otherwise, for user_note.mako, it's rendered by server side.
            loggedInUsername: '',
            isPageOwner: 'False' === 'True' ? true : false,
            loginComeFromUrl: 'https://www.zybuluo.com/login?return_to=https%3A%2F%2Fwww.zybuluo.com%2Fhanbingtao%2Fnote%2F433855',
            noteRemarksUrl: "https://www.zybuluo.com/note/433855/remarks", 
            newNoteRemarkUrl: "https://www.zybuluo.com/note/433855/remark/new", 
            updateNoteRemarkUrl: "https://www.zybuluo.com/note/433855/remark/update", 
            deleteNoteRemarkUrl: "https://www.zybuluo.com/note/433855/remark/delete", 
            publishNoteRemarkUrl: "https://www.zybuluo.com/note/433855/remark/publish", 
            newNoteRemarkReplyUrl: "https://www.zybuluo.com/note/433855/remark_reply/new", 
            updateNoteRemarkReplyUrl: "https://www.zybuluo.com/note/433855/remark_reply/update", 
            deleteNoteRemarkReplyUrl: "https://www.zybuluo.com/note/433855/remark_reply/delete", 
        };

        // BEGIN: pace.js configuration
        window.paceOptions = {
            // disable others, enable for ajax call only,
            ajax: true,
            document: false,
            elements: false,
            eventLag: false,
        };
        // jiawzhang NOTICE: to make sure pace.js is working for any ajax call especially the jquery ajax, add 'Pace.restart()' into jquery ajax call like '$.post'
        // Originally, pace 0.5.6 doesn't support jquery ajax, see details in: https://github.com/HubSpot/pace/issues/29
        // END: pace.js configuration

    </script>

    <script src="https://www.zybuluo.com/static/assets/mdeditor/7a70106e.layout.lib.min.js"></script>

    <script src="https://www.zybuluo.com/static/assets/mdeditor/dc648f35.layout.min.js"></script>



    

    <!-- https://www.zybuluo.com/static/assets/mdeditor/user_note.lib.min.js -->
    <!-- -->

    <script>
        Namespace('com.zybuluo.mdeditor.user_note');
        com.zybuluo.mdeditor.user_note.initData = {
            isLoggedIn: 'False',
            mdeditorUrl: "https://www.zybuluo.com/mdeditor",
            passwordPassed: 'True' === 'True' ? true : false,
        };
    </script>

    <script src="https://www.zybuluo.com/static/assets/mdeditor/6cd3112e.user_note.min.js"></script>



</body>
</html>
    
