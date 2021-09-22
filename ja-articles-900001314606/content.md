<h2>
    Index
</h2>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <a href="#section1">入门</a>
        </p>
    </li>
    <li>
        <p>
            <a href="#section2">环境准备</a>
        </p>
    </li>
    <li>
        <p>
            <a href="#section3">自定义图像</a>
        </p>
    </li>
    <li>
        <p>
            <a href="#section4">模式 1：使用 REST API 浏览数据</a>
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p>
                <a href="#section4-1">从其他应用检索表数据<br/></a>
            </p>
        </li>
        <li>
            <p>
                <a href="#section4-2">将表数据注册到其他应用</a>
            </p>
        </li>
    </ul>
    <li>
        <p>
            <a href="#section5">模式 2：仅引用标准功能</a>
        </p>
    </li>
    <li>
        <p>
            <a href="#section6">结束语</a>
        </p>
    </li>
</ul>
<h2>
    前言
</h2>
<p>
    如果想从另一个kintone应用引用表格的整个数据，
    但关联记录列表的功能又无法设置。有这方面困扰的人还是很多的吧。
</p>
<p>
    对于这些用户，我们总结了在应用之间引用表格数据的方法。现在，让我们看一下具体操作吧。
</p>
<h2>
    环境准备
</h2>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            kintone应用
        </p>
        <p class=" list-paddingleft-2">
        添加应用商店中的&quot;差旅费结算申请&quot;和&quot;出差申请&quot;。
        </p>
    </li>
    <li>
      <p>
        编辑器
      </p>
      <p class=" list-paddingleft-2">
        有关准备编辑器的内容可以参照 <a href="https://cybozudev.kf5.com/hc/kb/article/215327/#step3">此处</a>。
      </p>
    </li>
</ul>
<h2>
    自定义图像
</h2>
<p>
    通过此自定义，我们希望从<br/>&quot;出差申请&quot; 应用查看 &quot;差旅费结算申请&quot; 应用中的 &quot;差旅费用&quot; 表格中的数据。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>方式 1：&nbsp;使用 REST API&nbsp;</strong>
        </p>
    </li>
    <li>
        <p>
            <strong>方式 2：仅使用标准功能&nbsp; &nbsp;&nbsp;</strong>两种方式。
        </p>
    </li>
</ul>
<h2>
    方式 1：&nbsp;使用 REST API&nbsp;
</h2>
<p>
    在引用表格中的数据时，根据业务情况，需要执行许多参考操作，如下所示。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>我想从其他应用获取表格数据</strong>
        </p>
    </li>
    <li>
        <p>
            <strong>我想将表格数据存储到另一个应用中</strong>
        </p>
    </li>
</ul>
<p>
    在本文中，我想向您展示如何通过 JavaScript 自定义来实现上述两种方式的自动引用。
</p>
<h3>
    从其他应用检索表格数据
</h3>
<h4>
    <strong>工作方式</strong>
</h4>
<p>
    具体来说，它的工作原理是&nbsp;<strong>&quot;从其他应用获取表格数据，并将其显示在详细信息屏幕的空白字段中</strong>&quot; 。
</p>
<p>
    在此示例中，当显示&quot;出差申请&quot;应用的记录详细信息画面时，
</p>
<p>
    从&quot;差旅费结算申请&quot;应用获取&quot;旅费&quot;表格中的数据，并在空白栏字段中显示内容。 应用之间的关系图如下所示：
</p>
<p>
    <img src="https://developer.cybozu.io/hc/article_attachments/900002748206/2-1-outline-drawing.png" alt="2-1-outline-drawing.png" width="600" style="border-width:1px;border-style:solid;border-color:rgb(221,221,221);max-width:800px;vertical-align:middle;height:auto;"/>
</p>
<h4>
    <strong>已完成的画面</strong>
</h4>
<p>
    <img src="https://developer.cybozu.io/hc/article_attachments/900002792743/2-1-rendering_images.png" alt="2-1-rendering_images.png" style="border-width:1px;border-style:solid;border-color:rgb(221,221,221);max-width:800px;vertical-align:middle;height:auto;"/>
</p>
<h4>
    <strong>应用步骤</strong>
</h4>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>&quot;出差申请&quot;应用：<br/></strong>
        </p>
    </li>
</ul>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            添加字段代码为&quot;出差申请编号&quot;的记录编号字段。
        </p>
    </li>
    <li>
        <p>
            添加一个字段代码为 tableSpace 的空白栏字段。<br/>
        </p>
        <table>
            <tbody>
                <tr class="firstRow">
                    <th>
                        字段代码
                    </th>
                    <th>
                        字段类型
                    </th>
                    <th>
                        备注
                    </th>
                </tr>
                <tr>
                    <td>
                        出差申请号
                    </td>
                    <td>
                        记录编号
                    </td>
                    <td>
                        <p>
                            用于标识&quot;出差费用结算申请&quot;记录的数字。<br/>请参阅同一&quot;出差申请编号&quot;中的&quot;差旅费用结算申请&quot;记录中的表数据，并将其反映在&quot;出差申请&quot;记录中。
                        </p>
                    </td>
                </tr>
                <tr>
                    <td>
                        tableSpace
                    </td>
                    <td>
                        空白栏
                    </td>
                    <td>
                        用于显示检索到的&quot;出差费用结算申请&quot;的表格数据。
                    </td>
                </tr>
            </tbody>
        </table>
    </li>
    <li>
        <p>
            将示例程序保存到 JavaScript 文件，然后从设置画面读取文件。 *有关如何导入文件的信息<a href="https://jp.cybozu.help/k/ja/user/app_settings/js_customize.html">，请参阅使用 JavaScript 或 CSS 自定义</a>应用程序。<br/><br/>
        </p>
    </li>
</ol>
<p>
    在空白栏字段中显示数据时，<br/>标准函数无法计算显示的数据的总值。<br/>如果希望计算总金额（包括空白栏字段中显示的数据），<br/>则需要使用从&quot;差旅费结算申请&quot;应用获取的数据来计算总金额。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>&quot;差旅费结算申请&quot;应用程序：</strong>
        </p>
    </li>
</ul>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            添加字段代码为&quot;出差申请号&quot;的数值字段（必填字段）。<br/>
        </p>
        <table>
            <tbody>
                <tr class="firstRow">
                    <th>
                        字段代码
                    </th>
                    <th>
                        字段类型
                    </th>
                    <th>
                        备注
                    </th>
                </tr>
                <tr>
                    <td>
                        出差申请号
                    </td>
                    <td>
                        数值
                    </td>
                    <td>
                        <p>
                            用于标识&quot;出差申请&quot;记录的编号。<br/>相同的&quot;出差申请号&quot;中的&quot;出差申请&quot;记录反映&quot;差旅费结算申请&quot;的表数据。
                        </p>
                        <p>
                            在此处输入要链接的&quot;旅行申请&quot;应用程序的记录编号。<br/>
                        </p>
                        <p>
                            * 请匹配&quot;出差申请&quot;应用中的&quot;出差申请号&quot;和字段代码。<br/>• 字段设置 ：&quot;设为必填项&quot; 和 &quot;值为唯一&quot; 。<br/>
                        </p>
                    </td>
                </tr>
            </tbody>
        </table>
    </li>
</ol>
<h4>
    <strong>示例程序</strong><strong><br/></strong>
</h4>
<p>
    在&quot;出差申请&quot;应用的记录详情中，从&quot;差旅费结算申请&quot;应用获取&quot;差旅费用&quot;表格中的数据，并将其显示在&quot;出差申请&quot;应用的空白栏字段中。
</p>
<pre class="brush:js;toolbar:false">/*
 * 从其他应用程序引用表数据的示例程序
 * Copyright (c) 2020 Cybozu
 *
 * Licensed under the MIT License
 * https://opensource.org/licenses/mit-license.php
*/
(function() {
  &#39;use strict&#39;;
  kintone.events.on(&#39;app.record.detail.show&#39;, function(event) {
    // 请重写为&quot;差旅费结算申请&quot;的应用 ID
    var APP_ID = 123;
    // 获取「出差申请号」として利用する「记录编号」を取得
    var applicationNumber = kintone.app.record.getId();
    // フィールドコードを変数に格納
    var businessTripExpenses = &#39;旅費&#39;;
    var date = &#39;旅費日付&#39;;
    var transportation = &#39;手段&#39;;
    var summary = &#39;旅費摘要&#39;;
    var amount = &#39;旅費金額&#39;;
    var receipt = &#39;旅費領収書&#39;;
    // 「旅費精算申請アプリ」情報を表示する表を作成
    var tableHtml = &#39;&lt;thead&gt;&lt;tr&gt;&#39; +
        &#39;&lt;th&gt;&#39; + date + &#39;&lt;/th&gt;&#39; +
        &#39;&lt;th&gt;&#39; + transportation + &#39;&lt;/th&gt;&#39; +
        &#39;&lt;th&gt;&#39; + summary + &#39;&lt;/th&gt;&#39; +
        &#39;&lt;th&gt;&#39; + amount + &#39;&lt;/th&gt;&#39; +
        &#39;&lt;th&gt;&#39; + receipt + &#39;&lt;/th&gt;&#39; +
        &#39;&lt;/tr&gt;&#39; +
        &#39;&lt;/thead&gt;&#39; +
        &#39;&lt;/tbody&gt;&#39;;
    // スペースフィールドに作成した表を表示
    var tableEl = document.createElement(&#39;table&#39;);
    tableEl.id = &#39;table&#39;;
    tableEl.border = &#39;1&#39;;
    tableEl.style.textAlign = &#39;center&#39;;
    tableEl.style.padding = &#39;10px&#39;;
    tableEl.insertAdjacentHTML(&#39;afterbegin&#39;, tableHtml);
    kintone.app.record.getSpaceElement(&#39;tableSpace&#39;).appendChild(tableEl);
    // 「旅費精算申請アプリ」から「出張申請番号」が同じのレコードを取得
    var params = {
      &#39;app&#39;: APP_ID,
      &#39;query&#39;: &#39;出張申請番号 = &#39; + applicationNumber
    };
    return kintone.api(kintone.api.url(&#39;/k/v1/records&#39;, true), &#39;GET&#39;, params).then(function(resp) {
      var travelExpenseAppRecords = resp.records;
      // 同じ「出張申請番号」のレコードが「旅費精算申請アプリ」に存在しないときにエラーを表示
      if (travelExpenseAppRecords.length === 0) {
        window.alert(&#39;「旅費精算申請アプリ」に同じ「出張申請番号」のレコードがないため、「旅費」テーブルのデータを表示できません。&#39;);
        return event;
      }
      // 取得した「旅費精算申請アプリ」のテーブルデータを作成した表に格納
      var tableRows = travelExpenseAppRecords[0][businessTripExpenses].value;
      var tableRef = document.getElementById(&#39;table&#39;);
      tableRows.forEach(function(row) {
        var tableRow = tableRef.insertRow(-1);
        var cell1 = tableRow.insertCell(-1);
        var cell2 = tableRow.insertCell(-1);
        var cell3 = tableRow.insertCell(-1);
        var cell4 = tableRow.insertCell(-1);
        var cell5 = tableRow.insertCell(-1);
        cell1.appendChild(document.createTextNode(row.value[date].value));
        cell2.appendChild(document.createTextNode(row.value[transportation].value));
        cell3.appendChild(document.createTextNode(row.value[summary].value));
        cell4.appendChild(document.createTextNode(row.value[amount].value));
        cell5.appendChild(document.createTextNode(row.value[receipt].value));
      });
      return event;
    }).catch(function(error) {
      // エラー表示をする
      window.alert(&#39;エラーが起こりました。エラーメッセージ：&#39; + error.message);
      return event;
    });
  });
})();</pre>
<p>
    <br/>
</p>
<h4>
    &nbsp;<strong>操作确认</strong>
</h4>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            在&quot;差旅费结算申请&quot;应用中创建新记录并保存。<br/><br/>- 在&quot;差旅费&quot;表格中添加演示数据。
        </p>
    </li>
    <li>
        <p>
            在&quot;出差申请&quot;应用中创建新记录并保存。<br/>检查保存的记录详细信息屏幕的 tableSpace 空间字段<br/>是否显示类似于&quot;已完成画面&quot;的表格。
        </p>
    </li>
</ol>
<h3>
    将表格数据注册到其他应用
</h3>
<h4>
    <strong>工作方式<br/></strong>
</h4>
<p>
    具体而言<strong>，&quot;保存记录时，在要引用表数据的应用中注册表格</strong>&quot;。
</p>
<p>
    在此示例中，当您保存&quot;旅行费用结算申请&quot;应用的记录时，<br/>图像会将&quot;差旅费用&quot;表中的数据存储在&quot;旅行申请&quot;应用中。 应用之间的关系图如下所示。
</p>
<p>
    <img src="https://developer.cybozu.io/hc/article_attachments/900002748226/2-2-outline-drawing.png" alt="2-2-outline-drawing.png" width="600" style="border-width:1px;border-style:solid;border-color:rgb(221,221,221);max-width:800px;vertical-align:middle;height:auto;"/>
</p>
<h4>
    <strong>已完成的图像<br/></strong>
</h4>
<p>
    <img src="https://developer.cybozu.io/hc/article_attachments/900002792723/2-2-rendering_images.png" alt="2-2-rendering_images.png" style="border-width:1px;border-style:solid;border-color:rgb(221,221,221);max-width:800px;vertical-align:middle;height:auto;"/>
</p>
<h4>
    <strong>应用步骤</strong>
</h4>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>&quot;出差申请&quot;应用：</strong>
        </p>
    </li>
</ul>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            添加字段代码为&quot;出差申请号&quot;的记录编号字段。
        </p>
    </li>
    <li>
        <p>
            从设置中，添加用于存储检索到的数据的表。<br/>
        </p>
        <table>
            <tbody>
                <tr class="firstRow">
                    <th>
                        字段代码
                    </th>
                    <th>
                        字段类型
                    </th>
                    <th>
                        备注
                    </th>
                </tr>
                <tr>
                    <td>
                        出差申请号
                    </td>
                    <td>
                        记录编号
                    </td>
                    <td>
                        <p>
                            用于标识&quot;旅行费用结算申请&quot;记录的数字。<br/>从同一&quot;旅行申请编号&quot;的&quot;差旅费用结算申请&quot;记录中更新的表数据反映在&quot;旅行申请&quot;记录中。
                        </p>
                    </td>
                </tr>
                <tr>
                    <td>
                        旅费
                    </td>
                    <td>
                        表
                    </td>
                    <td>
                        添加与&quot;旅行费用结算申请&quot;中的&quot;差旅费&quot;表相同的表。
                    </td>
                </tr>
            </tbody>
        </table>
    </li>
</ol>
<p>
    <br/>
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>&quot;差旅费结算申请&quot;应用：</strong>
        </p>
    </li>
</ul>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            添加字段代码为&quot;旅行申请编号&quot;的记录编号字段。<br/>
        </p>
        <table>
            <tbody>
                <tr class="firstRow">
                    <th>
                        字段代码
                    </th>
                    <th>
                        字段类型
                    </th>
                    <th>
                        备注
                    </th>
                </tr>
                <tr>
                    <td>
                        出差申请号
                    </td>
                    <td>
                        数值
                    </td>
                    <td>
                        <p>
                            用于标识&quot;出差申请&quot;记录的编号。<br/>相同的&quot;出差申请号&quot;中的&quot;出差申请&quot;记录反映&quot;差旅费结算申请&quot;的表数据。
                        </p>
                        <p>
                            在此处输入要链接的&quot;出差申请&quot;应用的记录编号。<br/>
                        </p>
                        <p>
                            * 请匹配&quot;出差申请&quot;应用中的&quot;出差申请号&quot;和字段代码。<br/>• 字段设置 ：&quot;设为必填项&quot; 和 &quot;值为唯一&quot; 。
                        </p>
                    </td>
                </tr>
            </tbody>
        </table>
    </li>
    <li>
        <p>
            将示例程序保存到 JavaScript 文件，然后从设置屏幕读取文件。 *有关如何导入文件的信息<a href="https://jp.cybozu.help/k/ja/user/app_settings/js_customize.html">，请参阅使用 JavaScript 或 CSS 自定义</a>应用程序。<br/><br/>
        </p>
    </li>
</ol>
<h4>
    <strong>示例程序<br/></strong>
</h4>
<p>
    在&quot;旅行费用结算申请&quot;应用程序的记录添加和编辑屏幕保存成功后的事件中，&quot;<br/>旅行费用结算申请&quot;应用的&quot;差旅费&quot;表中的数据也会注册到&quot;旅行申请&quot;应用程序的&quot;差旅费&quot;表中。
</p>
<pre class="brush:js;toolbar:false">/*
 * テーブルのデータを別アプリから参照するサンプルプログラム
 * Copyright (c) 2020 Cybozu
 *
 * Licensed under the MIT License
 * https://opensource.org/licenses/mit-license.php
*/
(function() {
  &#39;use strict&#39;;
  kintone.events.on(&#39;app.record.detail.show&#39;, function(event) {
    // 「旅費精算申請アプリ」のアプリのIDに書き換えてください
    var APP_ID = 123;
    // 「出張申請番号」として利用する「レコード番号」を取得
    var applicationNumber = kintone.app.record.getId();
    // フィールドコードを変数に格納
    var businessTripExpenses = &#39;旅費&#39;;
    var date = &#39;旅費日付&#39;;
    var transportation = &#39;手段&#39;;
    var summary = &#39;旅費摘要&#39;;
    var amount = &#39;旅費金額&#39;;
    var receipt = &#39;旅費領収書&#39;;
    // 「旅費精算申請アプリ」情報を表示する表を作成
    var tableHtml = &#39;&lt;thead&gt;&lt;tr&gt;&#39; +
        &#39;&lt;th&gt;&#39; + date + &#39;&lt;/th&gt;&#39; +
        &#39;&lt;th&gt;&#39; + transportation + &#39;&lt;/th&gt;&#39; +
        &#39;&lt;th&gt;&#39; + summary + &#39;&lt;/th&gt;&#39; +
        &#39;&lt;th&gt;&#39; + amount + &#39;&lt;/th&gt;&#39; +
        &#39;&lt;th&gt;&#39; + receipt + &#39;&lt;/th&gt;&#39; +
        &#39;&lt;/tr&gt;&#39; +
        &#39;&lt;/thead&gt;&#39; +
        &#39;&lt;/tbody&gt;&#39;;
    // スペースフィールドに作成した表を表示
    var tableEl = document.createElement(&#39;table&#39;);
    tableEl.id = &#39;table&#39;;
    tableEl.border = &#39;1&#39;;
    tableEl.style.textAlign = &#39;center&#39;;
    tableEl.style.padding = &#39;10px&#39;;
    tableEl.insertAdjacentHTML(&#39;afterbegin&#39;, tableHtml);
    kintone.app.record.getSpaceElement(&#39;tableSpace&#39;).appendChild(tableEl);
    // 「旅費精算申請アプリ」から「出張申請番号」が同じのレコードを取得
    var params = {
      &#39;app&#39;: APP_ID,
      &#39;query&#39;: &#39;出張申請番号 = &#39; + applicationNumber
    };
    return kintone.api(kintone.api.url(&#39;/k/v1/records&#39;, true), &#39;GET&#39;, params).then(function(resp) {
      var travelExpenseAppRecords = resp.records;
      // 同じ「出張申請番号」のレコードが「旅費精算申請アプリ」に存在しないときにエラーを表示
      if (travelExpenseAppRecords.length === 0) {
        window.alert(&#39;「旅費精算申請アプリ」に同じ「出張申請番号」のレコードがないため、「旅費」テーブルのデータを表示できません。&#39;);
        return event;
      }
      // 取得した「旅費精算申請アプリ」のテーブルデータを作成した表に格納
      var tableRows = travelExpenseAppRecords[0][businessTripExpenses].value;
      var tableRef = document.getElementById(&#39;table&#39;);
      tableRows.forEach(function(row) {
        var tableRow = tableRef.insertRow(-1);
        var cell1 = tableRow.insertCell(-1);
        var cell2 = tableRow.insertCell(-1);
        var cell3 = tableRow.insertCell(-1);
        var cell4 = tableRow.insertCell(-1);
        var cell5 = tableRow.insertCell(-1);
        cell1.appendChild(document.createTextNode(row.value[date].value));
        cell2.appendChild(document.createTextNode(row.value[transportation].value));
        cell3.appendChild(document.createTextNode(row.value[summary].value));
        cell4.appendChild(document.createTextNode(row.value[amount].value));
        cell5.appendChild(document.createTextNode(row.value[receipt].value));
      });
      return event;
    }).catch(function(error) {
      // エラー表示をする
      window.alert(&#39;エラーが起こりました。エラーメッセージ：&#39; + error.message);
      return event;
    });
  });
})();</pre>
<h4>
    <strong>操作确认</strong>
</h4>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            在&quot;出差申请&quot;应用中创建新记录并保存。
        </p>
    </li>
    <li>
        <p>
            在&quot;申请差旅费&quot;应用中创建新记录并保存。<br/><br/>- 在&quot;差旅费&quot;表中注册演示数据。
        </p>
    </li>
    <li>
        <p>
            保存&quot;出差费用结算申请&quot;应用的记录添加/编辑屏幕时，<br/>如果出现&quot;出差申请应用反映差旅费用结算申请数据&quot;消息，<br/>请在 1 中创建的&quot;出差申请&quot;记录的&quot;差旅费&quot;表中查看数据是否反映。
        </p>
    </li>
</ol>
<h2>
    方式 2：仅引用标准功能
</h2>
<p>
    现在，我介绍了如何使用 JavaScript 进行自定义<br/>，但我想向您展示如何使用标准功能，这要容易一些。
</p>
<p>
    这是一个有点缺乏方便的方法，如按下操作按钮，<br/>但你可以不编码，所以如果你有兴趣，请试试看。
</p>
<h3>
    <strong>工作方式</strong>
</h3>
<p>
    <strong>&quot;要保存为表的数据存储在其他应用中</strong><br/>，<strong>然后使用相关记录功能从应用</strong>引用数据&quot;。
</p>
<p>
    对于此示例中使用的应用，
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>创建&quot;差旅项目&quot;应用</strong>
        </p>
    </li>
    <li>
        <p>
            <strong>将相当于&quot;旅行费用结算申请&quot;应用程序的表数据的内容保存到&quot;差旅费用明细&quot;应用</strong>
        </p>
    </li>
    <li>
        <p>
            <strong>使用相关记录从&quot;旅行费用结算申请&quot;和&quot;旅行申请&quot;应用查看保存的&quot;差旅费用详细信息&quot;应用中的数据</strong>
        </p>
    </li>
</ul>
<p>
    图像。 应用之间的关系图如下所示。
</p>
<p>
    <img src="https://developer.cybozu.io/hc/article_attachments/900002722503/1-outline-drawing.png" alt="1-outline-drawing.png" width="600" style="border-width:1px;border-style:solid;border-color:rgb(221,221,221);max-width:800px;vertical-align:middle;height:auto;"/>
</p>
<p>
    &nbsp;在新的&quot;差旅项目&quot;应用中注册数据是使用&quot;申请差旅费用&quot;应用中的操作<br/>按钮将一行表数据存储在一条记录中。
</p>
<h3>
    <strong>已完成的图像</strong>
</h3>
<p>
    <img src="https://developer.cybozu.io/hc/article_attachments/900002722403/1-rendering-image.png" alt="1-rendering-image.png" style="border-width:1px;border-style:solid;border-color:rgb(221,221,221);max-width:800px;vertical-align:middle;height:auto;font-family:&#39;-apple-system&#39;, BlinkMacSystemFont, &#39;Segoe UI&#39;, Helvetica, Arial, sans-serif;"/>
</p>
<h3>
    <strong>应用步骤</strong>
</h3>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>&quot;差旅项目&quot;应用：</strong>
        </p>
    </li>
</ul>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            创建新&quot;差旅项目&quot;应用。<br/><br/>-添加字段以保存与&quot;旅行费用结算申请&quot;<br/>应用程序的表数据等效的内容，如&quot;日期&quot;、&quot;手段&quot;、&quot;差旅说明&quot;、&quot;金额&quot;和&quot;收据&quot;。&nbsp;- 添加字段名称为&quot;差旅申请编号&quot;的字符串（一行）字段。<br/><br/><br/><br/>- 有关要添加的字段的详细信息，请参阅下文。<br/>
        </p>
        <table>
            <tbody>
                <tr class="firstRow">
                    <th>
                        字段名称
                    </th>
                    <th>
                        字段类型
                    </th>
                    <th>
                        备考
                    </th>
                </tr>
                <tr>
                    <td>
                        日期
                    </td>
                    <td>
                        日期字段
                    </td>
                    <td>
                        输入差旅费用的日期信息。
                    </td>
                </tr>
                <tr>
                    <td>
                        手段
                    </td>
                    <td>
                        下拉列表
                    </td>
                    <td>
                        输入旅行费用的&quot;手段&quot;信息。
                    </td>
                </tr>
                <tr>
                    <td>
                        旅行费用说明
                    </td>
                    <td>
                        字符串（一行）
                    </td>
                    <td>
                        输入旅行费用的说明信息。
                    </td>
                </tr>
                <tr>
                    <td>
                        金额
                    </td>
                    <td>
                        数字
                    </td>
                    <td>
                        输入差旅费用的金额信息。
                    </td>
                </tr>
                <tr>
                    <td>
                        收据
                    </td>
                    <td>
                        复选框
                    </td>
                    <td>
                        输入差旅费用的收据信息。
                    </td>
                </tr>
                <tr>
                    <td>
                        差旅费申请号
                    </td>
                    <td>
                        字符串（一行）
                    </td>
                    <td>
                        用作关联记录和操作的关键。
                    </td>
                </tr>
            </tbody>
        </table>
    </li>
</ol>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>&quot;申请差旅费报到&quot;应用程序：</strong>
        </p>
    </li>
</ul>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            删除&quot;差旅费&quot;表。
        </p>
    </li>
    <li>
        <p>
            设置操作功能。<br/><br/>- 在操作设置的&quot;关联字段&quot;中<br/>，将&quot;否&quot;字段与&quot;差旅项目&quot;应用中的&quot;旅行申请编号&quot;相关联。<br/><br/>*有关如何设置操作<a href="https://jp.cybozu.help/k/ja/user/app_settings/appaction/set_appaction.html">的信息</a>，请参阅此处。
        </p>
    </li>
    <li>
        <p>
            添加相关记录列表字段，并将其设置为查看&quot;差旅项目&quot;应用中的数据。<br/><br/>- 有关要添加的字段的详细信息，请参阅下文。<br/>
        </p>
        <table>
            <tbody>
                <tr class="firstRow">
                    <th>
                        字段名称
                    </th>
                    <th>
                        字段类型
                    </th>
                    <th>
                        备考
                    </th>
                </tr>
                <tr>
                    <td>
                        差旅费用项目
                    </td>
                    <td>
                        相关记录列表
                    </td>
                    <td></td>
                </tr>
            </tbody>
        </table>
    </li>
</ol>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            浏览应用：差旅项目
        </p>
    </li>
    <li>
        <p>
            要显示的记录条件：此应用程序的字段&quot;否&quot;和要引用的应用字段&quot;旅行申请编号&quot;
        </p>
    </li>
    <li>
        <p>
            要显示的字段：要在&quot;申请差旅费用结算&quot;应用中显示的字段
        </p>
    </li>
    <li>
        <p>
            有关如何设置相关记录的详细信息<a href="https://jp.cybozu.help/k/ja/user/app_settings/form/related_records/set_relatedrecords.html">，</a>请参阅此处。
        </p>
    </li>
</ul>
<p>
    如果相关记录功能（而不是表）在&quot;提交差旅费用&quot;应用中显示&quot;差旅<br/>&quot;数据，则表数据无法计算标准功能的总值。<br/>如果希望计算总计值（包括相关记录中的金额数据<a href="https://developer.cybozu.io/hc/ja/articles/203030394">），请参阅</a>此文章。<br/>如果首先尝试&quot;浏览表数据&quot;部分的行为，<br/>请在删除&quot;旅行费用结算申请&quot;中的&quot;旅行费用&quot;表时删除&quot;总差旅费用&quot;计算字段。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>&quot;旅行申请&quot;应用程序：</strong>
        </p>
    </li>
</ul>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            创建字段代码为&quot;旅行申请编号&quot;的字符串（一行）字段。<br/><br/>（用作关联记录和操作关联的键）
        </p>
    </li>
    <li>
        <p>
            添加相关记录列表字段，并将其设置为查看&quot;差旅项目&quot;应用中的数据。<br/><br/>- 有关要添加的字段的详细信息，请参阅下文。<br/>
        </p>
        <table>
            <tbody>
                <tr class="firstRow">
                    <th>
                        字段名称
                    </th>
                    <th>
                        字段类型
                    </th>
                    <th>
                        备考
                    </th>
                </tr>
                <tr>
                    <td>
                        差旅费申请号
                    </td>
                    <td>
                        字符串（一行）
                    </td>
                    <td>
                        用作关联记录和操作的关键。
                    </td>
                </tr>
                <tr>
                    <td>
                        差旅费用项目
                    </td>
                    <td>
                        相关记录列表
                    </td>
                    <td></td>
                </tr>
            </tbody>
        </table>
    </li>
</ol>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            浏览应用：差旅项目
        </p>
    </li>
    <li>
        <p>
            要显示的记录条件：此应用程序的字段&quot;差旅申请编号&quot;和&quot;旅行费用申请编号&quot;。
        </p>
    </li>
    <li>
        <p>
            要显示的字段：要在&quot;申请差旅费用结算&quot;应用中显示的字段
        </p>
    </li>
    <li>
        <p>
            有关如何设置相关记录的详细信息<a href="https://jp.cybozu.help/k/ja/user/app_settings/form/related_records/set_relatedrecords.html">，</a>请参阅此处。
        </p>
    </li>
</ul>
<h2>
    结束
</h2>
<p>
    在本提示中，我介绍了如何跨应用程序引用表数据（^0^）/
</p>
<p>
    还有许多其他有用的信息，<a href="https://developer.cybozu.io/hc/ja/sections/360002613691">如自定义</a><br/>数据引用中<a href="https://developer.cybozu.io/hc/ja/sections/360002613651">常用的相关</a>记录以及如何在表中执行其他操作♪
</p>
<p>
    <br/>
</p>
