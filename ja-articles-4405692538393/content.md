<h2 class="origin">
    はじめに〜昨今のライブラリ事情〜
</h2>
<h2 class="trans">
    前言〜库的昨夜和今天〜
</h2>
<p class="origin">
    フロントエンド界隈のトレンドは流れが速く、キャッチアップしづらい側面がありましたが、最近は比較的安定しています。<br/>JavaScript のフレームワークやライブラリにも栄枯盛衰がありますが、近頃はReactやVue.jsなどが多くの開発者に利用されています。<br/>ライトな開発であればそのようなライブラリを導入せずともJavaScriptカスタマイズする上では問題はありませんが、<br/>ある程度規模が大きくなると、ライブラリに頼ったほうが効率的に開発することができます。
</p>
<p class="trans">
    前端的世界日新月异，新技术层出不穷，令人难以追逐。但就最近一段时间而言，相对还算稳定。<br>
    就拿 JavaScript 的框架来说，经过了一时的逐鹿中原、盛衰荣辱，React 和 Vue.js 的两大主流地位基本确立了下来。<br>
    如果说轻量级 JavaScript 自定义开发不导入框架也能信手拈来的话，<br>
    一旦规模达到一定程度，借助框架的力量来提升开发效率就显得必不可少了。
</p>
<p class="origin">
    <a href="https://developer.cybozu.io/hc/ja/articles/209681606">こちらの記事</a>ではVue.jsとkintoneの組み合わせの良さを紹介いたしました。<br/>今回はReactを使ってkintone JavaScriptカスタマイズに導入した場合、どのようになるかをみていただき、プロジェクトにフィットするものを選ぶための材料にしてもらえればと思います。
</p>
<p class="trans">
    现在我们来演示导入 React 的过程，其中如果有合适的经验或窍门正好能用在您的项目中，我们将感到十分荣幸。
</p>
<p class="origin">
    シリーズの記事一覧は<a href="https://developer.cybozu.io/hc/ja/articles/900005565903">こちら</a>。
</p>
<p class="trans del">
    因为没有系列文章的总览表，故不翻译。
</p>
<h2 class="origin">
    Reactとは、Reactの特徴
</h2>
<h2 class="trans">
    React 是什么、React 的特征
</h2>
<p class="origin">
    React は、FacebookとReactのコミュニティによって開発されているユーザインタフェース構築のためのJavaScriptライブラリです。
</p>
<p class="trans">
    React 是 Facebook 和 React社区为构筑用户界面而开发的 JavaScript 库。
</p>
<p class="origin">
    <a href="https://ja.reactjs.org/">React の公式サイト</a>に書かれている、3つの特徴を解説します。
</p>
<p class="trans">
    现在解说一下<a href="https://ja.reactjs.org/">React 的官方网站</a>上所记载的三个特征。
</p>
<h3 class="origin">
    宣言的な View
</h3>
<h3 class="trans">
    声明式
</h3>
<p class="origin">
    &nbsp;「宣言的」というのは条件やどのように動作するかなどが明確に示されている状態です。<br/>例えばjQueryは「手続き的」 で、DOM操作であれば、要素を取得しその要素に対し命令を積み上げていきます。<br/>コードのいろんな箇所から要素に対して命令をすることができるので、複雑に絡み合うとバグの温床になります。
</p>
<p class="trans">
    &nbsp;「声明式」所说的是条件或者动作所明确表示的状态。<br/>例如 jQuery 是「命令式」的，如果是 DOM 操作的话，就取得元素后对它进行命令的堆叠。<br/>代码中有很多地方都对某个元素进行命令的话，各种复杂的条件交织在一起时，便成了 bug 的温床。
</p>

<p class="origin">
    たとえば、「クリックしたとき、その要素の色を赤と青に交互に変更する」というものを書いてみます。
</p>
<p class="trans">
    举个例子，根据如下需求写出代码：“按下按钮后，元素的颜色在红色和绿色之间反复切换”
</p>
```javascript
const element = $('#target');
element.on('click', () => {
  if(this.backgroundColor === 'red') {
    this.backgroundColor = 'blue';
  } else {
    this.backgroundColor = 'red';
  }
});
```
<p class="origin">
    これだけですと、大した差はないかもしれませんが、jQueryの場合は、どこからでもイベントハンドラーを追加することができてしまいます。<br/>また、「今の要素の色は何色か？」というような状態もDOMで管理することになる（要素から現在の色を読み取る）ので、コード上でやることが増えていった場合、<br/>どんどん複雑になり、正常に動作させつづけることが難しくなります。<br/>Reactの場合はDOMと状態は分けて管理されるため、状態が自明です。
</p>
<p class="trans">
    只有很少的代码，可能怎么写区别都不大，拿 jQuery 来说，可以从任何地方追加事件的句柄。<br/>还有“这个元素现在是什么颜色？”类似这种状态也要用代码管理起来的话，<br/>渐渐的越来越复杂，到最后难以维系正常的动作。<br/>React 则会把 DOM 和状态分开管理，状态一目了然。
</p>
<h3 class="origin">
    コンポーネントベース
</h3>
<h3 class="trans">
    基于组件
</h3>
<p class="origin">
    Reactは、自分自身の状態を管理するカプセル化されたコンポーネントを作成し組み合わせることで、複雑なユーザインターフェイスを構築することができます。
</p>
<p class="trans">
    在 React 中，组件自身能管理状态，并用搭建胶囊化的组件的方式，来构筑复杂的用户界面。
</p>
<p class="origin">
    コンポーネントのロジックは、Template ではなく JavaScript そのもので書くことができるので、様々なデータをアプリケーション内で簡単に取り回すことができ、<br/>かつ DOM に状態を持たせないようにすることができます。
</p>
<p class="trans">
    组件的逻辑是，不用 Template 而是直接可以写 JavaScript 代码，以便在程序中简单地获取各种各样的数据<br/>并且可以让 DOM 不带自身的状态。
</p>
<p class="origin">
    上記サンプルコードも、「赤なのか青なのか」という情報は、color変数が保持しており、DOMの状態を意識する必要がありません。<br/>また、その状態管理やイベントハンドリングも一つにまとめたコンポーネントとすることができます。
</p>
<p class="trans">
    在上述的代码范例中，“是红还是绿”，这个情报保存在 color 变量中，不需要在意 DOM 的状态。<br/>。
</p>
<h3 class="origin">
    一度学習すれば、どこでも使える
</h3>
<h3 class="trans">
    一次学习，处处使用
</h3>
<p class="origin">
    React と組み合わせて使用する技術に制限はありません。<br/>React を使って新しい機能を追加する際に、既存のソースコードを書き換える必要はありません。
</p>
<p class="trans">
   React 可以和其他技术并存而不产生冲突。<br/>使用 React 追加新功能时也不必更换既有代码。
</p>
<p class="origin">
    React は サーバ上でもレンダー（サーバーサイドレンダリング）できますし、React Native を使うことでモバイルアプリケーションの中でも動きますので、一度覚えると流用が可能です。
</p>
<p class="trans">
    React 在自建服务器或租赁服务器上都可运作，React Native则可以使你的程序运行在手机上，所以一旦掌握了可以在各处使用。
</p>
<h2 class="origin">
    React を導入する際の検討ポイント
</h2>
<h2 class="trans">
    React 引入时的注意点
</h2>
<p class="origin">
    Reactには次のようなメリットとデメリットがありますので、導入の際は、これらを加味して検討すると良いでしょう。
</p>
<p class="trans">
    React 有以下优缺点，在引入的时候，最好综合考虑各方面因素再加以判断。
</p>
<h3 class="origin">
    メリット
</h3>
<h3 class="trans">
    优点
</h3>
<ul class=" list-paddingleft-2">
    <li>
        <p class="origin">
            &nbsp;jQueryやプレーンなJavaScriptと比較すると、宣言的に書くことができるのが一番の強みです。
        </p>
        <p class="trans">
            &nbsp;和jQuery或纯 JavaScript 相比较，最大的强项是可以写声明式。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p class="origin">
                定義されたコンポーネントは、コンポーネントが持つ状態（上述のサンプルコードでいう、useStateで宣言されたcolor変数）が変化するとコードの上から下まで都度、実行されます。<br/>これにより、何が起きているかが明確になります。例えばjQueryやプレーンなJavaScriptだと、<br/>DOMに対してどこからどの命令が起きるかはわからず、複雑性が増していき、コントロールが大変になっていきます。
            </p>
            <p class="trans">
                定义好的组件，其状态如果发生改变（按上述的范例代码来举例的话，就是用 useState 来声明的变量 color ），则代码各处都会得到一遍执行。<br/>这样，发生了一些什么事都会很明确。例如 jQuery或纯 JavaScript 的话，<br/>对于 DOM 发起的命令的源头和内容就不能把握，复杂性逐渐增加，最后达到难以控制的程度。
            </p>
        </li>
        <li>
            <p class="origin">
                一覧のカスタマイズビューの実装や、独自のボタン・要素を数多く扱いたいときなどに有効です。
            </p>
            <p class="trans">
                处理数量众多的元素，例如“列表的自定义视图”，或“自创的按钮”等非常高效。
            </p>
        </li>
    </ul>
    <li>
        <p class="origin">
            ブラックボックス的な部分がすくなく、自明です。
        </p>
        <p class="trans">
            暗箱操作的部分较少。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p class="origin">
                Vue.jsやその他ライブラリと比較したとき、Reactは特別なルールが少なく（Vue.jsでいうv-modelディレクティブなど）、何が行われているかがわかりやすいです。<br/>サンプルコードのとおり、イベントハンドリングや値がどうなるか、というのはプレーンなJavaScriptを書く感覚で、自分ですべて指定できます。
            </p>
            <p class="trans">
                和其他的框架例如 Vue.js 等比较的话、React 所规定的特殊规则较少（例如 Vue.js 中的 v-model 等语法）、比较容易明白正在执行些什么事情。<br/>正如范例代码所写的那样，事件句柄的值会怎么变化都在掌握之中，有点像在写纯 JavaScript 的那种感觉，什么都可以自己掌控。
            </p>
        </li>
    </ul>
    <li>
        <p class="origin">
            ReactはJavaScriptライブラリのなかではかなりの人気があり、学習もしやすくいろんなコンポーネントも公開されています。<br/>上述の通りいろんなところに流用可能です。
        </p>
        <p class="trans">
            React 在 JavaScript 框架中是非常有人气的，学习起来比较容易，而且公开了非常多好用的组件。<br/>就像上面所说的，可以在各种场合使用。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p class="origin">
                作り方にもよりますが、kintone JavaScriptカスタマイズ上で定義していたコンポーネントを、そのままモバイルアプリの作成にも流用できます。
            </p>
            <p class="trans">
                虽然制作的方式各有不同，kintone JavaScript 自定义所制作的组件，可以原封不动地用在手机上。
            </p>
        </li>
    </ul>
    <li>
        <p class="origin">
            部分的に導入することも可能です。
        </p>
        <p class="trans">
            可以部分导入。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p class="origin">
                一部のJavaScriptカスタマイズはプレーンなJavaScriptだが、複雑な箇所からReactを適用するといったことも可能です。
            </p>
            <p class="trans">
                一部分的 JavaScript 自定义是用纯 JavaScript 编写、复杂的地方采用 React 来写，这种方案也是可行的。
            </p>
        </li>
    </ul>
    <li>
        <p class="origin">
            UIとロジックが分離できるので、大規模な開発にも向いています。
        </p>
        <p class="trans">
            UI 和逻辑是分离的，适合大规模的项目。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p class="origin">
                特に、いろんなアプリからREST APIでデータを取得して加工する、などのロジック部分をUIから別けれるので、ロジックを書く箇所がすっきりします。
            </p>
            <p class="trans">
                特别是各种应用都会使用 REST API来取得数据并加工。这种逻辑部分和 UI 是分开的，显得很清晰。
            </p>
        </li>
    </ul>
</ul>
<h3 class="origin">
    デメリット
</h3>
<h3 class="trans">
    缺点
</h3>
<ul class=" list-paddingleft-2">
    <li>
        <p class="origin">
            宣言的にかけるがゆえに、記述量としては増える傾向にあります。
        </p>
        <p class="trans">
            因为是声明式的，记述的代码量会有增加的趋势。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p class="origin">
                どちらかというと、ずっと面倒を見ていくkintone環境などに向いていると思います。
            </p>
            <p class="trans">
                然而对于一直维护的 kintone 环境来说，反而式比较适合的。
            </p>
        </li>
    </ul>
    <li>
        <p class="origin">
            パフォーマンスを向上させるためにはメモ化をする必要があるなど、場合によっては多少難易度があがります。
        </p>
        <p class="trans">
           要运用到记忆化等技术进行性能提升时，根据情况不同多少有点难度。
        </p>
    </li>
    <li>
        <p class="origin">
            数行で済むようなちょっとしたJavaScriptカスタマイズであればプレーンなJavaScriptで事足ります。
        </p>
        <p class="trans">
            寥寥数行代码就能解决的事情，用纯 JavaScript 就已经足够了。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p class="origin">
                条件によってテキストの色をかえる、などのJavaScriptカスタマイズなどであればわざわざ導入する必要はありません。
            </p>
            <p class="trans">
                根据实际情况，如果只是文本变色等简单逻辑，没有必要刻意导入。
            </p>
        </li>
    </ul>
</ul>
<h2 class="origin">
    カスタマイズビューをReactで構築する
</h2>
<h2 class="trans">
    用 React 实现自定义视图
</h2>
<p class="origin">
    今回は、<a href="https://kintone-sol.cybozu.co.jp/apps/031-kokyaku-list.html">顧客リストアプリ</a>を利用し、カスタマイズビューを作成するサンプルコードを作ります。
</p>
<p class="trans">
    这次，我们将利用顾客列表中制作自定义视图作为范例代码。
</p>
<p class="origin">
    会社名が一覧として表示され、チェックできます。
</p>
<p class="trans">
    自定义完成后，将达到这样一个效果：
</p>
<p class="trans">
    显示公司名列表，并且可以选择。
</p>
<p class="origin">
    ボタンを押すと、現在選択されている会社名を表示できます。
</p>
<p class="trans">
    按下按钮后，显示现在选中的公司名。
</p>
<p>
    <img src="https://developer.cybozu.io/hc/article_attachments/4405684989593/customerDatabase.png" alt="顧客リストアプリの一覧" title="" style="box-sizing: border-box;border-width: 1px;border-style: solid;border-color: rgb(221, 221, 221);max-width: 800px;vertical-align: middle;cursor: pointer;height: auto"/>
</p>
<h3 class="origin">
    事前準備
</h3>
<h3 class="trans">
    事前准备
</h3>
<p class="origin">
    1.&nbsp;<a href="https://kintone-sol.cybozu.co.jp/apps/031-kokyaku-list.html">顧客リストアプリ</a>を追加する。
</p>
<p class="trans">
    1. 添加顾客列表应用<br/>
    新增一个应用，选择默认安装好的模板“顾客列表”。<br/>
    创建成功后，初始还没有数据，我们可以自行添加一些测试数据。
</p>
<p class="origin">
    2. カスタマイズビューを設定し、HTMLは下記を指定する。
</p>
<p class="trans">
    1. 设置自定义视图，指定 HTML 代码。
</p>
```html
<div id="target"></div>
```

<p class="trans">
3. 为了配合后面克隆项目中的配置，我们把公司名的字段代码从“单行文本框”改为“会社名”
</p>

<p>
    <img src="https://developer.cybozu.io/hc/article_attachments/4405692511641/customerDatabase_settings.png" alt="カスタマイズビューの設定画面" title="" style="box-sizing: border-box;border-width: 1px;border-style: solid;border-color: rgb(221, 221, 221);max-width: 800px;vertical-align: middle;cursor: pointer;height: auto"/>
</p>
<p>
    1. Githubからクローンしてコードを用意する。
</p>
<p>
    4. 从 Github上克隆代码。
</p>
<p>
    <a href="https://github.com/cybozudevnet/sample-kintone-webpack-for-intermediate">https://github.com/cybozudevnet/sample-kintone-webpack-for-intermediate</a>
</p>
<p class="origin">
    詳しくは<a href="https://developer.cybozu.io/hc/ja/articles/360040220451">第1回</a>の記事からためしてみてください。
</p>
<p class="trans">
    详情请参照<a href="https://cybozudev.kf5.com/hc/kb/article/1412604">第1篇</a>中的内容。
</p>
<p class="origin">
    &nbsp; 今回、Reactを試せるような設定になっています。
</p>
<p class="trans">
    &nbsp; 这次将按 React 的要求来设置。
</p>
<h3 class="origin">
    サンプルコード
</h3>
<h3 class="trans">
    范例代码
</h3>
<p class="origin">
    上記を実現するためのReactを使ったサンプルコードは下記のようになります。
</p>
<p class="trans">
    用 React 实现的代码如下
</p>
<p>
    /src/apps/react-sample/index.tsx
</p>

```javascript
import React, {useState} from 'react';
import ReactDOM from 'react-dom';

// 声明组件
const ChecklistComponent: React.FC<{records: KintoneTypes.SavedCustomer[]}> = ({records}) => {
  // 保管选中的ID
  const [selectedIds, setSelectedIds] = useState<string[]>([]);

  // 按钮按下时的句柄
  const buttonHandler = () => {
    if (selectedIds.length === 0) {
      alert('什么都没有选中');
      return;
    }
    // 显示选中的公司名
    alert(`${selectedIds.map((id) => records.find((r) => r.$id.value === id)?.会社名.value).join('\n')}`);
  };

  // 点击复选框时的句柄
  const checkboxHandler = (recordId: string) => (e:React.ChangeEvent<HTMLInputElement>) => {
    if (e.target.checked) {
      // 返回含选中复选框的ID的新数组
      setSelectedIds((current) => [...current, recordId]);
    } else {
      // 删除复选框去除时的ID
      setSelectedIds((current) => {
        // 确认已经选中的
        const targetIndex = current.indexOf(recordId);
        if (targetIndex === -1) return current;
        // 返回去掉该index的新数组
        return [...current.slice(0, targetIndex), ...current.slice(targetIndex + 1)];
      });
    }
  };

  // 返回元素的定义
  return <div style={{margin: '8px 16px'}}>
    <div><button onClick={buttonHandler}>显示选中的客户</button></div>
    {records.map((record) => {
      return <div style={{margin: '4px 8px'}} key={record.$id.value}>
        <label>
          <input type="checkbox" onChange={checkboxHandler(record.$id.value)} checked={selectedIds.includes(record.$id.value)}/>
          <span style={{paddingLeft: '4px'}}>{record.会社名.value}</span>
        </label>
      </div>;
    })}
  </div>;
};


kintone.events.on('app.record.index.show', async (event) => {
  const records = event.records as KintoneTypes.SavedCustomer[];

  const targetEl = document.querySelector('#target');
  if (targetEl == null) return;
  // 显示Component
  ReactDOM.render(<ChecklistComponent records={records} />, targetEl);
});
```

<p>
    <br/>
</p>
<h3 class="origin">
    コードの概要説明
</h3>
<h3 class="trans">
    代码的概要说明
</h3>
<p class="origin">
    大まかに1.コンポーネントの定義と、2.コンポーネントの表示に分けて説明します。
</p>
<p class="trans">
    大致分为1.组件的定义、2.组件的显示。
</p>
<p>
    这里，运用到了上次第六篇中介绍到的 TypeScript 。
</p>
<p>
    1. 组件的定义
</p>

```javascript
// 组件的定义
const ChecklistComponent: React.FC<{records: KintoneTypes.SavedCustomer[]}> = ({records}) => {
  // 保管选中的ID
  const [selectedIds, setSelectedIds] = useState<string[]>([]);

  // 按钮按下时的句柄
  const buttonHandler = () => {
    if (selectedIds.length === 0) {
      alert('什么都没有选中');
      return;
    }
    // 显示选中的公司名
    alert(`${selectedIds.map((id) => records.find((r) => r.$id.value === id)?.会社名.value).join('\n')}`);
  };

  // 返回含选中复选框的ID的新数组
  const checkboxHandler = (recordId: string) => (e:React.ChangeEvent<HTMLInputElement>) => {
    if (e.target.checked) {
      // 返回含选中复选框的ID的新数组
      setSelectedIds((current) => [...current, recordId]);
    } else {
      // 删除复选框去除时的ID
      setSelectedIds((current) => {
        // 确认已经选中的
        const targetIndex = current.indexOf(recordId);
        if (targetIndex === -1) return current;
        // 返回去掉该index的新数组
        return [...current.slice(0, targetIndex), ...current.slice(targetIndex + 1)];
      });
    }
  };

  //  返回元素的定义
  return <div style={{margin: '8px 16px'}}>
    <div><button onClick={buttonHandler}>显示选中的客户</button></div>
    {records.map((record) => {
      return <div style={{margin: '4px 8px'}} key={record.$id.value}>
        <label>
          <input type="checkbox" onChange={checkboxHandler(record.$id.value)} checked={selectedIds.includes(record.$id.value)}/>
          <span style={{paddingLeft: '4px'}}>{record.会社名.value}</span>
        </label>
      </div>;
    })}
  </div>;
};
```

<p class="origin">
    今回は、複数のチェックボックスを一つのコンポーネントとして定義しました。
</p>
<p class="trans">
    这里，把多选框定义为一个组件。
</p>
<p class="origin">
    Reactでは<a href="https://ja.reactjs.org/docs/introducing-jsx.html">JSX</a>を利用して、要素の定義ができます。36〜47行目のように、HTMLを書くような感覚でかけます。
</p>
<p class="trans">
    React用<a href="https://zh-hans.reactjs.org/docs/introducing-jsx.html">JSX</a>来定义组件，如下方代码所示，就有点像在写Html语言。
</p>

```javascript
  // 返回元素的定义
  return <div style={{margin: '8px 16px'}}>
    <div><button onClick={buttonHandler}>显示选中的客户</button></div>
    {records.map((record) => {
      return <div style={{margin: '4px 8px'}} key={record.$id.value}>
        <label>
          <input type="checkbox" onChange={checkboxHandler(record.$id.value)} checked={selectedIds.includes(record.$id.value)}/>
          <span style={{paddingLeft: '4px'}}>{record.会社名.value}</span>
        </label>
      </div>;
    })}
  </div>;
```

<p class="origin">
    ボタンを押したときのハンドラや、チェックボックスをおしたときのハンドラは、それぞれ10〜17行目、20〜34行目のように宣言します。
</p>
<p class="trans">
    按钮按下时的句柄，多选框选中时的句柄，在这里做申明。
</p>

```javascript
const buttonHandler = () => {
  if (selectedIds.length === 0) {
    alert('什么都没有选中。');
    return;
  }
  // 显示选中的公司名
  alert(`${selectedIds.map((id) => records.find((r) => r.$id.value === id)?.会社名.value).join('\n')}`);
};
```

```javascript
const checkboxHandler = (recordId: string) => (e:React.ChangeEvent<HTMLInputElement>) => {
  if (e.target.checked) {
    // 返回含选中复选框的ID的新数组
    setSelectedIds((current) => [...current, recordId]);
  } else {
    // 删除复选框去除时的ID
    setSelectedIds((current) => {
      // 确认已经选中的
      const targetIndex = current.indexOf(recordId);
      if (targetIndex === -1) return current;
      // 返回去掉该index的新数组
      return [...current.slice(0, targetIndex), ...current.slice(targetIndex + 1)];
    });
  }
};
```

<p class="origin">
    また、7行目にチェックボックスでチェックしたIDを保管するようのState（状態）を定義しています。useStateを使うことで状態を保持することができます。
</p>
<p class="trans">
    另外，第7行使用了 State （状态）保存了已选中的ID，使用 useState 可以保持住状态。
</p>

```javascript
const [selectedIds, setSelectedIds] = useState<string[]>([]);
```

<p class="origin">
    この内、selectedIdsは今保持しているIDがはいっており、setSelectedIdsでIDのセットができます。
</p>
<p class="trans">
    这里面 selectedIds 是存放已选的ID，setSelectedIds设置这次所选ID。
</p>
<p class="origin">
    このように、要素の定義と、そのハンドラの定義、状態をセットで書くことができ、一つのコンポーネントとして宣言できます。jQueryなどでは状態をclassなどで表現したりしますが、<br/>ReactではUIと切り分けて状態を保持できるのも大きな利点です。
</p>
<p class="trans">
    像这样，通过定义元素、定义事件的句柄等可以完整地申明一个组件。<br/>相较于jQuery这种是用 class 来表示状态，React把 UI 和状态分开存放的特点是一大优势。
</p>
<p class="origin">
    2. コンポーネントの表示
</p>
<p class="trans">
    2. 组件的显示
</p>

```javascript
kintone.events.on('app.record.index.show', async (event) => {
  const records = event.records as KintoneTypes.SavedCustomer[];

  const targetEl = document.querySelector('#target');
  if (targetEl == null) return;
  // 显示Component
  ReactDOM.render(<ChecklistComponent records={records} />, targetEl);
});
```

<p class="origin">
    1で定義したコンポーネントは、57行目にあるようにReactDOM.render()で表示することが可能です。
</p>
<p class="trans">
    在1中定义的组件，可以用 ReactDOM.render() 这个方法来显示
</p>

```javascript
ReactDOM.render(<ChecklistComponent records={records} />, targetEl);
```

<p class="origin">
    今回は一覧表示イベントで表示したいため、一覧表示イベントハンドラ内でそれを定義しています。
</p>
<p class="trans">
    这次主要想显示列表事件，所以就在列表的事件内逐一定义了。
</p>
<p class="origin">
    コンポーネントにはeventオブジェクトに入っているレコードの一覧を渡しています。
</p>
<p class="trans">
    把 event 对象内的记录列表传给了组件。
</p>
<p class="origin">
    今回のように、汎用的なコンポーネントをいくつか定義しておき、kintoneのイベントハンドラはそれを組み立てるだけの最低限で書くことも可能です。
</p>
<p class="trans">
    像这次这样，申明一些通用的组件，在 kintone 的事件句柄中自由组合这些组件，就可以以一个极小的代码量来完成这些需求。
</p>
<h2 class="origin">
    おわりに
</h2>
<h2 class="trans">
    结束语
</h2>
<p class="origin">
    JavaScriptカスタマイズは、今回のようにReactを活用したり、Vueなどの他フレームワークや、プレーンなJavaScriptも利用できるなど、様々なカスタマイズ方法があります。
</p>
<p class="trans">
    JavaScript 的自定义中，可以用本篇中所介绍的 React，也可以用 Vue 等其他的框架，也可以写纯 JavaScript。方法是多种多样的。
</p>
<p class="origin">
    自分のプロジェクトにあったカスタマイズ方法は何かを見定めて技術選定をすることで、JavaScriptカスタマイズの運用がスムーズになります。<br/>特にある程度カスタマイズし続ける可能性が見込まれそうな場合、ぜひ今回のようにReactなどの大きな規模にも耐えられるフレームワーク・ライブラリを利用してみるのもいいかと思います。
</p>
<p class="trans">
    根据自己项目的特点，选择合适的技术，可以使 JavaScript 的自定义工作更加柔顺。<br/>特别是有持续维护可能性的项目，非常推荐您使用本篇中所介绍的像 React 那样有大项目耐受性的框架。
</p>
<p class="origin">
    シリーズの記事一覧は<a href="https://developer.cybozu.io/hc/ja/articles/900005565903">こちら</a>。
</p>
<p class="trans del">
    因为没有系列文章的总览表，故不翻译。
</p>
<p class="origin">
    このTipsは、2021年9月版 kintone で確認したものになります。
</p>
<p class="trans">
    该Tips在 kintone 2021年9月版中进行过确认。
</p>