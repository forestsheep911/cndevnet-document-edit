<h2>
    スペースのトップ画面の表示後イベント
</h2>
<p>
    スペースのトップ画面が表示された後に発生するイベントです。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            「スペースのポータルと複数にスレッドを使用する」が有効のスペースのみで発生します。
        </p>
    </li>
    <li>
        <p>
            ゲストスペースのトップ画面では発生しません。
        </p>
    </li>
    <li>
        <p>
            各ウィジェットがすべて描画されたあとに発生します。
        </p>
    </li>
    <li>
        <p>
            kintone.Promise オブジェクトを return すると、非同期処理の完了を待って次の処理を開始します。
        </p>
    </li>
</ul>
<h3>
    イベントタイプ
</h3>
<table>
    <tbody>
        <tr class="firstRow">
            <th>
                環境
            </th>
            <th>
                イベントタイプ
            </th>
            <th>
                イベントが発生するタイミング
            </th>
        </tr>
        <tr>
            <td>
                PC 用
            </td>
            <td>
                space.portal.show
            </td>
            <td>
                スペースのトップ画面が表示された時
            </td>
        </tr>
        <tr>
            <td>
                スマートフォン用
            </td>
            <td>
                mobile.space.portal.show
            </td>
            <td>
                モバイルのスペースのトップ画面が表示された時
            </td>
        </tr>
    </tbody>
</table>
<h3>
    eventオブジェクトのプロパティ
</h3>
<table>
    <tbody>
        <tr class="firstRow">
            <th>
                プロパティ名
            </th>
            <th>
                型
            </th>
            <th>
                説明
            </th>
        </tr>
        <tr>
            <td>
                spaceId
            </td>
            <td>
                文字列
            </td>
            <td>
                スペース ID
            </td>
        </tr>
    </tbody>
</table>
<h3>
    eventオブジェクトで実行できる操作
</h3>
<h4>
    非同期処理の完了を待って次の処理を行う
</h4>
<p>
    kintone.Promise オブジェクトを return することにより、非同期処理の完了を待ってから event オブジェクトで実行できる操作を実行できます。<br/>同じイベントに複数のイベントハンドラが登録されているとき、エラーなどが発生して Thenable オブジェクトが棄却された場合には、後続のイベントハンドラの処理は実行されません。<br/><br/>記述方法は&nbsp;<a href="https://developer.cybozu.io/hc/ja/articles/360023047852">kintone における Promise の書き方の基本</a>を参考にしてください。
</p>
<h3>
    サンプル
</h3>
<p>
    スペースのトップ画面が表示された時にアラートを表示します。
</p>
<p>
    <br/>
</p>
<table>
    <tbody>
        <tr class="firstRow">
            <td></td>
            <td>
                kintone.events.on(&#39;space.portal.show&#39;, function(event) {
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                window.alert(&#39;スペースのポータル画面を開きました&#39;);
            </td>
        </tr>
        <tr>
            <td></td>
            <td>
                return event;
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