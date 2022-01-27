<h2>
    はじめに〜昨今のライブラリ事情〜
</h2>
<p style="color:#ff7722">
    フロントエンド界隈のトレンドは流れが速く、キャッチアップしづらい側面がありましたが、最近は比較的安定しています。<br/>JavaScript のフレームワークやライブラリにも栄枯盛衰がありますが、近頃はReactやVue.jsなどが多くの開発者に利用されています。<br/>ライトな開発であればそのようなライブラリを導入せずともJavaScriptカスタマイズする上では問題はありませんが、<br/>ある程度規模が大きくなると、ライブラリに頼ったほうが効率的に開発することができます。
</p>
<p style="color:#43a255">
    前端的变化非常快，有着令人难以把握的一面。
</p>
<p>
    <a href="https://developer.cybozu.io/hc/ja/articles/209681606">こちらの記事</a>ではVue.jsとkintoneの組み合わせの良さを紹介いたしました。<br/>今回はReactを使ってkintone JavaScriptカスタマイズに導入した場合、どのようになるかをみていただき、プロジェクトにフィットするものを選ぶための材料にしてもらえればと思います。
</p>
<p>
    シリーズの記事一覧は<a href="https://developer.cybozu.io/hc/ja/articles/900005565903">こちら</a>。
</p>
<h2>
    Reactとは、Reactの特徴
</h2>
<p>
    React は、FacebookとReactのコミュニティによって開発されているユーザインタフェース構築のためのJavaScriptライブラリです。
</p>
<p>
    <a href="https://ja.reactjs.org/">React の公式サイト</a>に書かれている、3つの特徴を解説します。
</p>
<h3>
    宣言的な View
</h3>
<p>
    &nbsp;「宣言的」というのは条件やどのように動作するかなどが明確に示されている状態です。<br/>例えばjQueryは「手続き的」 で、DOM操作であれば、要素を取得しその要素に対し命令を積み上げていきます。<br/>コードのいろんな箇所から要素に対して命令をすることができるので、複雑に絡み合うとバグの温床になります。
</p>
<p>
    たとえば、「クリックしたとき、その要素の色を赤と青に交互に変更する」というものを書いてみます。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            jQuery
        </p>
    </li>
</ul>
<p>
    <br/>
</p>
<table>
    <tbody>
        <tr class="firstRow">
            <td></td>
            <td>
                const element = $(&#39;#target&#39;);
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                element.on(&#39;click&#39;, () =&gt; {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                if(this.backgroundColor === &#39;red&#39;) {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                this.backgroundColor = &#39;blue&#39;;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                } else {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                this.backgroundColor = &#39;red&#39;;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                }
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                });
            </td>
        </tr>
    </tbody>
</table>
<p>
    &nbsp;Copyクリップボードにコピーしました
</p>
<p>
    <br/>
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            React
        </p>
    </li>
</ul>
<p>
    <br/>
</p>
<table>
    <tbody>
        <tr class="firstRow">
            <td></td>
            <td>
                const Element = () =&gt; {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                const [color, setColor] = useState(&#39;red&#39;);
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                const clickHandler = () =&gt; color === &#39;red&#39; ? setColor(&#39;blue&#39;) : setColor(&#39;red&#39;);
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                return &lt;div styles={{ backgroundColor: color}} onClick={clickHandler}&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                };
            </td>
        </tr>
    </tbody>
</table>
<p>
    &nbsp;Copyクリップボードにコピーしました
</p>
<p>
    <br/>
</p>
<p>
    これだけですと、大した差はないかもしれませんが、jQueryの場合は、どこからでもイベントハンドラーを追加することができてしまいます。<br/>また、「今の要素の色は何色か？」というような状態もDOMで管理することになる（要素から現在の色を読み取る）ので、コード上でやることが増えていった場合、<br/>どんどん複雑になり、正常に動作させつづけることが難しくなります。<br/>Reactの場合はDOMと状態は分けて管理されるため、状態が自明です。
</p>
<h3>
    コンポーネントベース
</h3>
<p>
    Reactは、自分自身の状態を管理するカプセル化されたコンポーネントを作成し組み合わせることで、複雑なユーザインターフェイスを構築することができます。
</p>
<p>
    コンポーネントのロジックは、Template ではなく JavaScript そのもので書くことができるので、様々なデータをアプリケーション内で簡単に取り回すことができ、<br/>かつ DOM に状態を持たせないようにすることができます。
</p>
<p>
    上記サンプルコードも、「赤なのか青なのか」という情報は、color変数が保持しており、DOMの状態を意識する必要がありません。<br/>また、その状態管理やイベントハンドリングも一つにまとめたコンポーネントとすることができます。
</p>
<h3>
    一度学習すれば、どこでも使える
</h3>
<p>
    React と組み合わせて使用する技術に制限はありません。<br/>React を使って新しい機能を追加する際に、既存のソースコードを書き換える必要はありません。
</p>
<p>
    React は サーバ上でもレンダー（サーバーサイドレンダリング）できますし、React Native を使うことでモバイルアプリケーションの中でも動きますので、一度覚えると流用が可能です。
</p>
<h2>
    React を導入する際の検討ポイント
</h2>
<p>
    Reactには次のようなメリットとデメリットがありますので、導入の際は、これらを加味して検討すると良いでしょう。
</p>
<h3>
    メリット
</h3>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            &nbsp;jQueryやプレーンなJavaScriptと比較すると、宣言的に書くことができるのが一番の強みです。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p>
                定義されたコンポーネントは、コンポーネントが持つ状態（上述のサンプルコードでいう、useStateで宣言されたcolor変数）が変化するとコードの上から下まで都度、実行されます。<br/>これにより、何が起きているかが明確になります。例えばjQueryやプレーンなJavaScriptだと、<br/>DOMに対してどこからどの命令が起きるかはわからず、複雑性が増していき、コントロールが大変になっていきます。
            </p>
        </li>
        <li>
            <p>
                一覧のカスタマイズビューの実装や、独自のボタン・要素を数多く扱いたいときなどに有効です。
            </p>
        </li>
    </ul>
    <li>
        <p>
            ブラックボックス的な部分がすくなく、自明です。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p>
                Vue.jsやその他ライブラリと比較したとき、Reactは特別なルールが少なく（Vue.jsでいうv-modelディレクティブなど）、何が行われているかがわかりやすいです。<br/>サンプルコードのとおり、イベントハンドリングや値がどうなるか、というのはプレーンなJavaScriptを書く感覚で、自分ですべて指定できます。
            </p>
        </li>
    </ul>
    <li>
        <p>
            ReactはJavaScriptライブラリのなかではかなりの人気があり、学習もしやすくいろんなコンポーネントも公開されています。<br/>上述の通りいろんなところに流用可能です。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p>
                作り方にもよりますが、kintone JavaScriptカスタマイズ上で定義していたコンポーネントを、そのままモバイルアプリの作成にも流用できます。
            </p>
        </li>
    </ul>
    <li>
        <p>
            部分的に導入することも可能です。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p>
                一部のJavaScriptカスタマイズはプレーンなJavaScriptだが、複雑な箇所からReactを適用するといったことも可能です。
            </p>
        </li>
    </ul>
    <li>
        <p>
            UIとロジックが分離できるので、大規模な開発にも向いています。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p>
                特に、いろんなアプリからREST APIでデータを取得して加工する、などのロジック部分をUIから別けれるので、ロジックを書く箇所がすっきりします。
            </p>
        </li>
    </ul>
</ul>
<h3>
    デメリット
</h3>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            宣言的にかけるがゆえに、記述量としては増える傾向にあります。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p>
                どちらかというと、ずっと面倒を見ていくkintone環境などに向いていると思います。
            </p>
        </li>
    </ul>
    <li>
        <p>
            パフォーマンスを向上させるためにはメモ化をする必要があるなど、場合によっては多少難易度があがります。
        </p>
    </li>
    <li>
        <p>
            数行で済むようなちょっとしたJavaScriptカスタマイズであればプレーンなJavaScriptで事足ります。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p>
                条件によってテキストの色をかえる、などのJavaScriptカスタマイズなどであればわざわざ導入する必要はありません。
            </p>
        </li>
    </ul>
</ul>
<h2>
    カスタマイズビューをReactで構築する
</h2>
<p>
    今回は、<a href="https://kintone-sol.cybozu.co.jp/apps/031-kokyaku-list.html">顧客リストアプリ</a>を利用し、カスタマイズビューを作成するサンプルコードを作ります。
</p>
<p>
    会社名が一覧として表示され、チェックできます。
</p>
<p>
    ボタンを押すと、現在選択されている会社名を表示できます。
</p>
<p>
    <img src="https://developer.cybozu.io/hc/article_attachments/4405684989593/customerDatabase.png" alt="顧客リストアプリの一覧" title="" style="box-sizing: border-box;border-width: 1px;border-style: solid;border-color: rgb(221, 221, 221);max-width: 800px;vertical-align: middle;cursor: pointer;height: auto"/>
</p>
<h3>
    事前準備
</h3>
<p>
    1.&nbsp;<a href="https://kintone-sol.cybozu.co.jp/apps/031-kokyaku-list.html">顧客リストアプリ</a>を追加する。
</p>
<p>
    1. カスタマイズビューを設定し、HTMLは下記を指定する。
</p>
<pre>&lt;div id=&quot;target&quot;&gt;&lt;/div&gt;</pre>
<p>
    &nbsp;Copyクリップボードにコピーしました
</p>
<p>
    <img src="https://developer.cybozu.io/hc/article_attachments/4405692511641/customerDatabase_settings.png" alt="カスタマイズビューの設定画面" title="" style="box-sizing: border-box;border-width: 1px;border-style: solid;border-color: rgb(221, 221, 221);max-width: 800px;vertical-align: middle;cursor: pointer;height: auto"/>
</p>
<p>
    3. Githubからクローンしてコードを用意する。
</p>
<p>
    <a href="https://github.com/cybozudevnet/sample-kintone-webpack-for-intermediate">https://github.com/cybozudevnet/sample-kintone-webpack-for-intermediate</a>
</p>
<p>
    詳しくは<a href="https://developer.cybozu.io/hc/ja/articles/360040220451">第1回</a>の記事からためしてみてください。
</p>
<p>
    &nbsp; 今回、Reactを試せるような設定になっています。
</p>
<h3>
    サンプルコード
</h3>
<p>
    上記を実現するためのReactを使ったサンプルコードは下記のようになります。
</p>
<p>
    /src/apps/react-sample/index.tsx
</p>
<p>
    <br/>
</p>
<table>
    <tbody>
        <tr class="firstRow">
            <td></td>
            <td>
                import React, {useState} from &#39;react&#39;;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                import ReactDOM from &#39;react-dom&#39;;
            </td>
        </tr>
        <tr>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td>
                // Componentの定義
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                const ChecklistComponent: React.FC&lt;{records: KintoneTypes.SavedCustomer[]}&gt; = ({records}) =&gt; {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                // チェックしたIDを保管する
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                const [selectedIds, setSelectedIds] = useState&lt;string[]&gt;([]);
            </td>
        </tr>
        <tr>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td>
                // ボタンを押したときのハンドラ
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                const buttonHandler = () =&gt; {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                if (selectedIds.length === 0) {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                alert(&#39;何も選択されていません。&#39;);
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                return;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                }
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                // なにか選択されていれば、会社名を表示する。
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                alert(`${selectedIds.map((id) =&gt; records.find((r) =&gt; r.$id.value === id)?.会社名.value).join(&#39;\n&#39;)}`);
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                };
            </td>
        </tr>
        <tr>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td>
                // チェックボックスを押したときのハンドラ
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                const checkboxHandler = (recordId: string) =&gt; (e:React.ChangeEvent&lt;HTMLInputElement&gt;) =&gt; {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                if (e.target.checked) {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                // チェックされた場合、チェックしたIDを含めて新しい配列を返却
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                setSelectedIds((current) =&gt; [...current, recordId]);
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                } else {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                // チェックを外された場合、チェックしたIDを消す
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                setSelectedIds((current) =&gt; {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                // すでに選ばれているか念の為確認
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                const targetIndex = current.indexOf(recordId);
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                if (targetIndex === -1) return current;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                // 該当のindexを切り取って新しい配列を返却
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                return [...current.slice(0, targetIndex), ...current.slice(targetIndex + 1)];
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                });
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                }
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                };
            </td>
        </tr>
        <tr>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td>
                // 要素の定義と返却
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                return &lt;div style={{margin: &#39;8px 16px&#39;}}&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;div&gt;&lt;button onClick={buttonHandler}&gt;選択されている顧客を表示する&lt;/button&gt;&lt;/div&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                {records.map((record) =&gt; {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                return &lt;div style={{margin: &#39;4px 8px&#39;}} key={record.$id.value}&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;label&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;input type=&quot;checkbox&quot; onChange={checkboxHandler(record.$id.value)} checked={selectedIds.includes(record.$id.value)}/&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;span style={{paddingLeft: &#39;4px&#39;}}&gt;{record.会社名.value}&lt;/span&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;/label&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;/div&gt;;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                })}
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;/div&gt;;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                };
            </td>
        </tr>
        <tr>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td>
                kintone.events.on(&#39;app.record.index.show&#39;, async (event) =&gt; {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                const records = event.records as KintoneTypes.SavedCustomer[];
            </td>
        </tr>
        <tr>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td>
                const targetEl = document.querySelector(&#39;#target&#39;);
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                if (targetEl == null) return;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                // Componentを描画
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                ReactDOM.render(&lt;ChecklistComponent records={records} /&gt;, targetEl);
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                });
            </td>
        </tr>
    </tbody>
</table>
<p>
    &nbsp;Copyクリップボードにコピーしました
</p>
<p>
    <br/>
</p>
<h3>
    コードの概要説明
</h3>
<p>
    大まかに1.コンポーネントの定義と、2.コンポーネントの表示に分けて説明します。
</p>
<p>
    今回は、前回第六章で説明したTypeScriptも利用したコードになります。
</p>
<p>
    1. コンポーネントの定義
</p>
<p>
    <br/>
</p>
<table>
    <tbody>
        <tr class="firstRow">
            <td></td>
            <td>
                // Componentの定義
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                const ChecklistComponent: React.FC&lt;{records: KintoneTypes.SavedCustomer[]}&gt; = ({records}) =&gt; {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                // チェックしたIDを保管する
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                const [selectedIds, setSelectedIds] = useState&lt;string[]&gt;([]);
            </td>
        </tr>
        <tr>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td>
                // ボタンを押したときのハンドラ
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                const buttonHandler = () =&gt; {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                if (selectedIds.length === 0) {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                alert(&#39;何も選択されていません。&#39;);
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                return;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                }
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                // なにか選択されていれば、会社名を表示する。
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                alert(`${selectedIds.map((id) =&gt; records.find((r) =&gt; r.$id.value === id)?.会社名.value).join(&#39;\n&#39;)}`);
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                };
            </td>
        </tr>
        <tr>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td>
                // チェックボックスを押したときのハンドラ
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                const checkboxHandler = (recordId: string) =&gt; (e:React.ChangeEvent&lt;HTMLInputElement&gt;) =&gt; {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                if (e.target.checked) {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                // チェックされた場合、チェックしたIDを含めて新しい配列を返却
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                setSelectedIds((current) =&gt; [...current, recordId]);
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                } else {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                // チェックを外された場合、チェックしたIDを消す
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                setSelectedIds((current) =&gt; {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                // すでに選ばれているか念の為確認
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                const targetIndex = current.indexOf(recordId);
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                if (targetIndex === -1) return current;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                // 該当のindexを切り取って新しい配列を返却
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                return [...current.slice(0, targetIndex), ...current.slice(targetIndex + 1)];
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                });
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                }
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                };
            </td>
        </tr>
        <tr>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td>
                // 要素の定義と返却
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                return &lt;div style={{margin: &#39;8px 16px&#39;}}&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;div&gt;&lt;button onClick={buttonHandler}&gt;選択されている顧客を表示する&lt;/button&gt;&lt;/div&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                {records.map((record) =&gt; {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                return &lt;div style={{margin: &#39;4px 8px&#39;}} key={record.$id.value}&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;label&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;input type=&quot;checkbox&quot; onChange={checkboxHandler(record.$id.value)} checked={selectedIds.includes(record.$id.value)}/&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;span style={{paddingLeft: &#39;4px&#39;}}&gt;{record.会社名.value}&lt;/span&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;/label&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;/div&gt;;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                })}
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;/div&gt;;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                };
            </td>
        </tr>
    </tbody>
</table>
<p>
    &nbsp;Copyクリップボードにコピーしました
</p>
<p>
    <br/>
</p>
<p>
    今回は、複数のチェックボックスを一つのコンポーネントとして定義しました。
</p>
<p>
    Reactでは<a href="https://ja.reactjs.org/docs/introducing-jsx.html">JSX</a>を利用して、要素の定義ができます。36〜47行目のように、HTMLを書くような感覚でかけます。
</p>
<table>
    <tbody>
        <tr class="firstRow">
            <td></td>
            <td>
                // 要素の定義と返却
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                return &lt;div style={{margin: &#39;8px 16px&#39;}}&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;div&gt;&lt;button onClick={buttonHandler}&gt;選択されている顧客を表示する&lt;/button&gt;&lt;/div&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                {records.map((record) =&gt; {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                return &lt;div style={{margin: &#39;4px 8px&#39;}} key={record.$id.value}&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;label&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;input type=&quot;checkbox&quot; onChange={checkboxHandler(record.$id.value)} checked={selectedIds.includes(record.$id.value)}/&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;span style={{paddingLeft: &#39;4px&#39;}}&gt;{record.会社名.value}&lt;/span&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;/label&gt;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;/div&gt;;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                })}
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                &lt;/div&gt;;
            </td>
        </tr>
    </tbody>
</table>
<p>
    <br/>
</p>
<p>
    ボタンを押したときのハンドラや、チェックボックスをおしたときのハンドラは、それぞれ10〜17行目、20〜34行目のように宣言します。
</p>
<table>
    <tbody>
        <tr class="firstRow">
            <td></td>
            <td>
                const buttonHandler = () =&gt; {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                if (selectedIds.length === 0) {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                alert(&#39;何も選択されていません。&#39;);
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                return;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                }
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                // なにか選択されていれば、会社名を表示する。
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                alert(`${selectedIds.map((id) =&gt; records.find((r) =&gt; r.$id.value === id)?.会社名.value).join(&#39;\n&#39;)}`);
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                };
            </td>
        </tr>
    </tbody>
</table>
<p>
    <code><table>
        <tbody>
            <tr class="firstRow">
                <td></td>
                <td>
                    const checkboxHandler = (recordId: string) =&gt; (e:React.ChangeEvent&lt;HTMLInputElement&gt;) =&gt; {
                </td>
            </tr>
            <tr>
                <td></td>
                <td>
                    if (e.target.checked) {
                </td>
            </tr>
            <tr>
                <td></td>
                <td>
                    // チェックされた場合、チェックしたIDを含めて新しい配列を返却
                </td>
            </tr>
            <tr>
                <td></td>
                <td>
                    setSelectedIds((current) =&gt; [...current, recordId]);
                </td>
            </tr>
            <tr>
                <td></td>
                <td>
                    } else {
                </td>
            </tr>
            <tr>
                <td></td>
                <td>
                    // チェックを外された場合、チェックしたIDを消す
                </td>
            </tr>
            <tr>
                <td></td>
                <td>
                    setSelectedIds((current) =&gt; {
                </td>
            </tr>
            <tr>
                <td></td>
                <td>
                    // すでに選ばれているか念の為確認
                </td>
            </tr>
            <tr>
                <td></td>
                <td>
                    const targetIndex = current.indexOf(recordId);
                </td>
            </tr>
            <tr>
                <td></td>
                <td>
                    if (targetIndex === -1) return current;
                </td>
            </tr>
            <tr>
                <td></td>
                <td>
                    // 該当のindexを切り取って新しい配列を返却
                </td>
            </tr>
            <tr>
                <td></td>
                <td>
                    return [...current.slice(0, targetIndex), ...current.slice(targetIndex + 1)];
                </td>
            </tr>
            <tr>
                <td></td>
                <td>
                    });
                </td>
            </tr>
            <tr>
                <td></td>
                <td>
                    }
                </td>
            </tr>
            <tr>
                <td></td>
                <td>
                    };
                </td>
            </tr>
        </tbody>
    </table></code>
</p>
<p>
    <br/>
</p>
<p>
    また、7行目にチェックボックスでチェックしたIDを保管するようのState（状態）を定義しています。useStateを使うことで状態を保持することができます。
</p>
<table>
    <tbody>
        <tr class="firstRow">
            <td></td>
            <td>
                const [selectedIds, setSelectedIds] = useState&lt;string[]&gt;([]);
            </td>
        </tr>
    </tbody>
</table>
<p>
    <br/>
</p>
<p>
    この内、selectedIdsは今保持しているIDがはいっており、setSelectedIdsでIDのセットができます。
</p>
<p>
    このように、要素の定義と、そのハンドラの定義、状態をセットで書くことができ、一つのコンポーネントとして宣言できます。jQueryなどでは状態をclassなどで表現したりしますが、<br/>ReactではUIと切り分けて状態を保持できるのも大きな利点です。
</p>
<p>
    2. コンポーネントの表示
</p>
<p>
    <br/>
</p>
<table>
    <tbody>
        <tr class="firstRow">
            <td></td>
            <td>
                kintone.events.on(&#39;app.record.index.show&#39;, async (event) =&gt; {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                const records = event.records as KintoneTypes.SavedCustomer[];
            </td>
        </tr>
        <tr>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td>
                const targetEl = document.querySelector(&#39;#target&#39;);
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                if (targetEl == null) return;
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                // Componentを描画
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                ReactDOM.render(&lt;ChecklistComponent records={records} /&gt;, targetEl);
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                });
            </td>
        </tr>
    </tbody>
</table>
<p>
    <br/>
</p>
<p>
    1で定義したコンポーネントは、57行目にあるようにReactDOM.render()で表示することが可能です。
</p>
<p>
    <br/>
</p>
<table>
    <tbody>
        <tr class="firstRow">
            <td></td>
            <td>
                ReactDOM.render(&lt;ChecklistComponent records={records} /&gt;, targetEl);
            </td>
        </tr>
    </tbody>
</table>
<p>
    <br/>
</p>
<p>
    今回は一覧表示イベントで表示したいため、一覧表示イベントハンドラ内でそれを定義しています。
</p>
<p>
    コンポーネントにはeventオブジェクトに入っているレコードの一覧を渡しています。
</p>
<p>
    今回のように、汎用的なコンポーネントをいくつか定義しておき、kintoneのイベントハンドラはそれを組み立てるだけの最低限で書くことも可能です。
</p>
<h2>
    おわりに
</h2>
<p>
    JavaScriptカスタマイズは、今回のようにReactを活用したり、Vueなどの他フレームワークや、プレーンなJavaScriptも利用できるなど、様々なカスタマイズ方法があります。
</p>
<p>
    自分のプロジェクトにあったカスタマイズ方法は何かを見定めて技術選定をすることで、JavaScriptカスタマイズの運用がスムーズになります。<br/>特にある程度カスタマイズし続ける可能性が見込まれそうな場合、ぜひ今回のようにReactなどの大きな規模にも耐えられるフレームワーク・ライブラリを利用してみるのもいいかと思います。
</p>
<p>
    シリーズの記事一覧は<a href="https://developer.cybozu.io/hc/ja/articles/900005565903">こちら</a>。
</p>
<p>
    このTipsは、2021年9月版 kintone で確認したものになります。
</p>
<audio controls="controls" style="display: none;"></audio>