<h1>
    教你搭建一个能轻松自创开发工具，并且集免上传代码，实时调试，自动发布，独立测试，按需部署于一体的神奇开发环境
</h1>
<h2>
    Index<br/>
</h2>
<ul class="anchor-link list-paddingleft-2">
    <li>
        <p>
            <a href="#step1">前言</a>
        </p>
    </li>
    <li>
        <p>
            &nbsp;&nbsp;&nbsp;&nbsp;<a href="#step1.1"></a>
        </p>
    </li>
    <li>
        <p>
            &nbsp;&nbsp;&nbsp;&nbsp;<a href="#step1.2"></a>
        </p>
    </li>
    <li>
        <p>
            <a href="#step2"></a>
        </p>
    </li>
    <li>
        <p>
            &nbsp;&nbsp;&nbsp;&nbsp;<a href="#step2.1"></a>
        </p>
    </li>
    <li>
        <p>
            &nbsp;&nbsp;&nbsp;&nbsp;<a href="#step2.2"></a>
        </p>
    </li>
    <li>
        <p>
            <a href="#step3"></a>
        </p>
    </li>
    <li>
        <p>
            &nbsp;&nbsp;&nbsp;&nbsp;<a href="#step3.1"></a>
        </p>
    </li>
    <li>
        <p>
            &nbsp;&nbsp;&nbsp;&nbsp;<a href="#step3.2"></a>
        </p>
    </li>
    <li>
        <p>
            &nbsp;&nbsp;&nbsp;&nbsp;<a href="#step3.3"></a>
        </p>
    </li>
    <li>
        <p>
            <a href="#step4"></a>
        </p>
    </li>
</ul>
<h2>
    前言
</h2>
<p>
    在 kintone 的日常开发中，经常有小伙伴碰到一系列的问题，包括但不限于以下：
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            每次改完代码都需要上传到 kintone 后台，才能看到效果，琐碎耗时
        </p>
    </li>
    <li>
        <p>
            团队开发需要打造一些小工具，以提升效率，但是工具开发本身也是一件耗时的事情，而且部署和版本迭代也是个难题
        </p>
    </li>
    <li>
        <p>
            有时候需要在真实环境下进行小范围试运行，但是上传自定义代码后会影响到所有人
        </p>
    </li>
    <li>
        <p>
            一个大范围使用的应用，不同的小团队和个人有不同的定制化需求，如何做到在一定范围内小规模部署？
        </p>
    </li>
</ul>
<p>
    以上这些问题其实可以通过一系列的环境搭建来解决，今天我们就来一步步实践演示一下如何去搭建这样一个环境。
</p>
<h2>
    原理介绍
</h2>
<p>
    首先我们来了解一下这个开发环境是基于什么样的基础搭建起来的。这对我们理解它的运作原理非常有帮助，如果后期有改造需求的话，这些内容将会非常有帮助。
</p>
<p>
    首先，上传 kintone 后台的自定义代码是有执行时间点的，它基本上是会在 kintone 的一些基础内容加载完之后执行，但是按 WEB 的标准来说，他的执行时间点在【开始加载页面内容】之后，在【结束加载页面内容】之前。
</p>
<p>
    在知道了这点原理之后，就有一个想法冒了出来：“即使不上传代码到 kintone 后台，只要在相同的时间点执行相应的代码，应该有办法模拟相同的 kintone 自定义开发吧？”
</p>
<p>
    是的，答案是的确有办法可以做到。我们依赖的是 Chrome 浏览器提供的 Extension 所赋予我们的能力。Extension 旨在以 API 形式提供很多浏览器扩展能力开放给开发者，而开发者可以根据实际需求来制作自己的 Extension。而 Extension 其中的一项能力就是 把 JS 注入到网页中，而且它提供的注入时间点也能正好满足 kinone 自定义代码的执行时机。这样基础条件就具备了。
</p>
<p>
    虽然我们可以制作 Extension 来做到所有事情，但是 Extension 的制作需要额外的学习，而且最麻烦的是 Extension 的发布需要通过官方商店的审核，虽然可以通过手动导入开发模式来解决，但是版本控制等一系列的问题导致这种方式效率低下，在实际运用层面变得不可行。
</p>
<p>
    好在有一款叫做 Tampermonkey （以下简称TM）的 Extension，它的作用是可以在网页中注入 JS，它在注入 JS 方面继承了 Extension的能力，就像通过一个中转站，TM 本身只要安装一次，而注入的具体代码就可以随心所欲的改变，不需要经过审核，这样就可以做到快速迭代，而且不需要学习额外的知识。
</p>
<p>
    现在理论基础有了，工具也有了，可以说是万事俱备只欠东风了。接下来我们就来一步步实践一下。
</p>
<h2>
    制作开发环境
</h2>
<p>
    要制作一个东西，我们在动手之前，最好对它应该具备什么样的功能做到心理有数。我们先总结一下功能列表。分为两个部分：主要功能和可选功能。主要功能就是最核心的功能，如果没有这些功能，那么这个环境就没有存在的必要了。可选功能则是一些锦上添花的东西，根据实际需求可以取舍的。
</p>
<p>
    主要功能：
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            编辑器后立即在浏览器体现效果。也就是免除一切的代码上传等操作。
        </p>
        <p>
            TM 的 Header 信息必须是自动生成，免去人工编写。
        </p>
    </li>
</ul>
<p>
    可选功能：
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            分离开发环境和生产环境。
        </p>
    </li>
    <li>
        <p>
            代码风格约束，整理，检查。
        </p>
    </li>
    <li>
        <p>
            git 版本控制相关。比如：忽略文件种类。
        </p>
        <p>
            代码风格约束，整理，检查。
        </p>
        <p>
            服务器自动编译，方便发布商店。
        </p>
        <p>
            处理各种资源。比如图片、CSS、HTML 等。
        </p>
        <p>
            处理 TypeScript 的能力。
        </p>
    </li>
</ul>
<p>
    以上这些功能，我们发现和开发一款前端脚手架非常相似，如果要我们自己从头开始制作是非常费时费力的，好在开源社区的力量是很强大的，已经有网友开源了<a href="https://github.com/forestsheep911/capricious-monkey">他的仓库</a>，我们可以直接拿来用。
</p>
<p class="operaCheck">
    注意：开源社区所提供的内容，请大家遵守开源协议。Cybozu 不对其功能和安全性负责。
</p>

<h2>
    实践演示
</h2>
<p>
    刚开始看到这个仓库，肯定是比较陌生的，下面我将带你一步一步的操作，最后再加入一个小功能，去实际体验一下如何使用这个开发环境。
</p>
<h3>
    安装 TM 并设置
</h3>
<p>
    1. 首先我们先来安装 TM。如果你用的是 Chrome 浏览器，那么你可以直接在 Chrome 商店中搜索 Tampermonkey，然后点击添加到 Chrome 即可。如果你是其他浏览器，那你可以从 <a href="https://www.tampermonkey.net/">的官网上找到相应的安装方式。</a>
</p>
<p>
    2. 然后我们必须设置一下 TM。步骤如下：
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            再扩展程序中找到TM，点击三个点，点击管理扩展程序。 
        </p>
        <img src="https://file.notion.so/f/s/465eac64-6ffe-4f2d-98c9-d27bb952e9b3/Untitled.png?id=331f2454-cbe3-400e-b1fa-f7493b518040&table=block&spaceId=84e1d4ff-7133-47d5-ae3b-9d0c38b7fd94&expirationTimestamp=1690264800000&signature=c0rFFget3D2LVM6HWgqpCkO1ZGLCmw61c01tYLzQciI&downloadName=Untitled.png">
    </li>
    <li>
        <p>
            找到【允许访问文件地址】并打开。
        </p>
        <img src="https://file.notion.so/f/s/0b7ee7e1-153f-4f99-bc58-42c58dededa8/Untitled.png?id=c3847909-11d3-4af2-83b8-73ce51235864&table=block&spaceId=84e1d4ff-7133-47d5-ae3b-9d0c38b7fd94&expirationTimestamp=1690264800000&signature=5UNVV4_yuFnS12V0QwSVkuZ7fNJWy6YXFD52lp2KpRc&downloadName=Untitled.png">
    </li>
</ul>
<h3>
    安装模板
</h3>
<p>
    1. 打开之前介绍的<a href="https://github.com/forestsheep911/capricious-monkey">仓库地址</a>，点击右上角的【Use this template】，再选【create a new repository】。如果是没有看到这个按钮，很可能是你没有登录 github。
    <img src="https://file.notion.so/f/s/eafb5d6d-9bae-402f-9007-fb010499e7a4/Untitled.png?id=92b5defa-2a54-4a57-bf7c-c853f9c52788&table=block&spaceId=84e1d4ff-7133-47d5-ae3b-9d0c38b7fd94&expirationTimestamp=1690272000000&signature=PeS7qx6ycWXAi4swYrZmr3Oliqw2JZTu3faJF3V9x8w&downloadName=Untitled.png">
</p>
<p>
    2. 创建好自己的仓库后，再 clone 到本地。然后可以用 vscode 等开发工具打开此目录。
    <img src="https://file.notion.so/f/s/eafb5d6d-9bae-402f-9007-fb010499e7a4/Untitled.png?id=92b5defa-2a54-4a57-bf7c-c853f9c52788&table=block&spaceId=84e1d4ff-7133-47d5-ae3b-9d0c38b7fd94&expirationTimestamp=1690272000000&signature=PeS7qx6ycWXAi4swYrZmr3Oliqw2JZTu3faJF3V9x8w&downloadName=Untitled.png">
</p>
<p>
    3. 打开 package.json，修改 name， version， description， author， repository 等信息。这些信息在编译的时候会被搬运脚本中，所以你不想之后再去每次都修改的话，这里应该填上正确的信息。
</p>
<p>
    4. 安装依赖。使用 【npm i】或者【yarn】安装依赖。选择你喜欢的方式即可。
</p>
<p>
    5. 打开 /config/dev.meta.js 文件，找到 match。match 这个配置项的意思是对哪些域名生效。例如
    ``` json
    {
        match: [
            'https://*.cybozu.cn/k/*',
            'https://*.cybozu.com/k/*',
            'https://*.cybozu-dev.com/k/*',
            'https://*.kintone.com/k/*',
        ],
    }
    ```
<h3>
    编写代码执行脚本
</h3>
<p>
    1. 打开并编辑 /src/app.ts，如果你要编写 js，改后缀名即可。
    我们来演示一个放大用户头像照片的小功能，只要鼠标放在用户选择或者发言者的头像上时，照片就会放大显示。
    代码如下：
</p>
<p>
    ``` javascript
    const app = () => {
        setTimeout(() => {
          const readUnread = document.querySelectorAll('div.gaia-argoui-toggleswitch-option')
          if (readUnread.length >= 2) {
            readUnread[0].addEventListener('mouseup', function () {
              showAvatar()
            })
            readUnread[1].addEventListener('mouseup', function () {
              showAvatar()
            })
          }
        }, 2000)
        showAvatar()
        window.addEventListener('hashchange', function () {
          setTimeout(() => {
            showAvatar()
          }, 2000)
        })
        function showAvatar() {
          setTimeout(() => {
            const findusericon = document.querySelectorAll(
              'span.User-cybozu, .itemlist-userImage-gaia, a.recordlist-username-gaia, .ocean-ntf-ntfitem-img > span, span.itemlist-userImage-gaia, .ocean-ui-comments-commentbase-entity div, .ocean-ntf-menuitem-img > span',
            )
            if (findusericon.length != 0) {
              findusericon.forEach(function (element) {
                const usericon = document.createElement('img')
                usericon.style.display = 'none'
                element.addEventListener('mouseenter', function (e) {
                  document.body.appendChild(usericon)
                  const thisSpan = e.target as HTMLElement
                  const innerImg = thisSpan.querySelector('img') as HTMLImageElement
                  if (innerImg) {
                    usericon.src = innerImg.src.replace(/SMALL|NORMAL/g, 'ORIGINAL')
                  }
                  const spanBackground = thisSpan.style.backgroundImage
                  if (spanBackground) {
                    const imgUrlRex = RegExp(/https.*png/g)
                    const resultUrl = imgUrlRex.exec(spanBackground)
                    console.log(resultUrl)
                    if (resultUrl && resultUrl.length > 0) {
                      usericon.src = resultUrl[0].replace(/SIZE_\d+/g, 'ORIGINAL')
                    }
                  }
      
                  usericon.onload = function () {
                    usericon.style.position = 'fixed'
                    usericon.style.display = 'block'
                    const me = e as MouseEvent
                    const leftOffset = me.clientX > window.innerWidth / 2 ? 0.25 : 0.75
                    usericon.style.width = window.innerWidth / 4 + 'px'
                    usericon.style.left = (window.innerWidth - usericon.width) * leftOffset + 'px'
                    usericon.style.top = (window.innerHeight - usericon.height) / 2 + 'px'
                    usericon.style.zIndex = '9999'
                  }
                })
      
                element.addEventListener('mouseout', function () {
                  if (usericon) {
                    usericon.remove()
                  }
                })
              })
            }
          }, 2000)
        }
      }
      
      export default app
    ```
</p>
<p>
    2. 在终端里输入 【npm run dev】，显示正确编译后，找到 /dist/dev/****.header.js 文件，复制里面的全部内容。( **** 为你给项目起的名字) <br>
    【*.script.js】才是真正的全部代码，【*.header.js】文件只是简单拷贝了它的头部，方便全选复制而已。因为在 TM 中只要把头部复制进去就可以了。
</p>
<p>
    3. 切换到浏览器，打开 TM 图标，选择添加脚本。
    <img src="https://file.notion.so/f/s/ef4ee65c-93cc-4ac3-84d4-a13524b484b4/Untitled.png?id=06ef49e4-8b8e-476a-90dc-e1330860af82&table=block&spaceId=84e1d4ff-7133-47d5-ae3b-9d0c38b7fd94&expirationTimestamp=1690279200000&signature=agNNINRc4b2dquJel-zD9dYvQQBLVRaBF-cvGyG5OGI&downloadName=Untitled.png">
</p>
<p>
    4. 粘贴在 2 中复制的内容。然后保存。以后每次修改代码，只要保存，就会自动编译更新。TM 中的脚本无需再更新。
    <img src="https://file.notion.so/f/s/a88e6461-03f7-43c3-ae24-ccd0fea3bc78/Untitled.png?id=29cab88b-186e-48ab-86d5-86f5e882d915&table=block&spaceId=84e1d4ff-7133-47d5-ae3b-9d0c38b7fd94&expirationTimestamp=1690279200000&signature=AggJXAk4uBWZUuyojxy8H8uZiMZCHBhKaB6wb4gkVxo&downloadName=Untitled.png">
</p>
<h3>
    实际效果
</h3>
<p>
    实际效果如下，是不是很方便呢？
</p>
<img src="https://file.notion.so/f/s/70a5f214-3439-47b6-a8ae-a9d212d307c4/Untitled.png?id=441a272d-e1e3-491f-a8a0-54b05fcff881&table=block&spaceId=84e1d4ff-7133-47d5-ae3b-9d0c38b7fd94&expirationTimestamp=1690279200000&signature=RXKAE-rUT-pM4LycG2_LcRMDZfNP9N-h8HRy4XriExc&downloadName=Untitled.png">