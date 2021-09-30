<h2>
    Index
</h2>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <a href="#section1">前言</a>
        </p>
    </li>
    <li>
        <p>
            <a href="#section2">环境准备</a>
        </p>
    </li>
    <li>
        <p>
            <a href="#section3">自定义概况</a>
        </p>
    </li>
    <li>
        <p>
            <a href="#section4">方式 1：使用 REST API 浏览数据</a>
        </p>
    </li>
    <li>
        <p>
            <a href="#section5">方式 2：仅引用标准功能</a>
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
 &nbsp; &nbsp;但关联记录列表的功能又无法设置。有这方面困扰的人还是很多的吧。
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
        <p class="list-paddingleft-2">
            添加应用商店中的“差旅费结算申请”和“出差申请”。
        </p>
    </li>
    <li>
        <p>
            编辑器
        </p>
        <p class="list-paddingleft-2">
            有关准备编辑器的内容可以参照 <a href="https://cybozudev.kf5.com/hc/kb/article/215327/#step3">此处</a>。
        </p>
    </li>
</ul>
<h2>
    自定义概况
</h2>
<p>
    通过此自定义，我们希望从“出差申请” 应用查看 “差旅费结算申请” 应用中的 “旅费” 表格中的数据。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>方式 1：&nbsp;使用 REST API&nbsp;</strong>
        </p>
    </li>
    <li>
        <p>
            <strong>方式 2：仅使用标准功能&nbsp; &nbsp;&nbsp;</strong>
        </p>
        <p>
            这次介绍以上两种方式。
        </p>
    </li>
</ul>
<h2>
    方式 1：&nbsp;使用 REST API&nbsp;
</h2>
<p>
    在引用表格中的数据时，根据业务情况，需要执行许多参照操作，例如下列场景。
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
    在本文中，将向您展示如何通过 JavaScript 自定义来实现上述两种方式的自动引用。
</p>
<h3>
    从其他应用获取表格数据
</h3>
<h4>
    机制
</h4>
<p>
    具体来说，它的机制是&nbsp;<strong>“从其他应用获取表格数据，并将其显示在详细信息屏幕的空白字段中”</strong> 。
</p>
<p>
    在此示例中，当显示“出差申请”应用的记录详细信息画面时，
</p>
<p>
    从“差旅费结算申请”应用获取“旅费”表格中的数据，并在空白栏字段中显示内容。 应用之间的关系图如下所示：
</p>
<p>
    <img src="https://files.kf5.com/attachments/download/23361/12386073/0016155771f98ce17ec2037c06ed0c6/" alt="0016155771f98ce17ec2037c06ed0c6"/>
</p>
<h4>
    <strong>已完成的画面</strong>
</h4>
<p>
    <img src="https://files.kf5.com/attachments/download/23361/12386221/00161557b52e01e324fe82add579749/" alt="00161557b52e01e324fe82add579749"/>
</p>
<h4>
    <strong>应用步骤</strong>
</h4>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>“出差申请”应用：<br/></strong>
        </p>
    </li>
</ul>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            添加字段代码为“出差申请编号”的记录编号字段。
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
                            用于标识“出差费用结算申请”记录的数字。<br/>请参阅同一“出差申请编号”中的“差旅费用结算申请”记录中的表数据，并将其反映在“出差申请”记录中。
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
                        用于显示检索到的“出差费用结算申请”的表格数据。
                    </td>
                </tr>
            </tbody>
        </table>
    </li>
    <li>
        <p>
            将示例程序保存到 JavaScript 文件，然后从设置画面读取文件。 *有关如何导入文件的信息，请参阅<a href="https://jp.cybozu.help/k/zh/user/app_settings/js_customize.html">通过 JavaScript 或 CSS 自定义应用</a>。
        </p>
    </li>
</ol>
<p>
    在空白栏字段中显示数据时，标准函数无法计算显示的数据的总值。如果希望计算总金额（包括空白栏字段中显示的数据），则需要使用从“差旅费结算申请“应用获取的数据来计算总金额。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>“差旅费结算申请”应用程序：</strong>
        </p>
    </li>
</ul>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            添加字段代码为“出差申请号”的数值字段（必填字段）。<br/>
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
                            用于标识“出差申请”记录的编号。<br/>相同的“出差申请号”中的“出差申请”记录反映“差旅费结算申请”的表数据。
                        </p>
                        <p>
                            在此处输入要链接的“出差申请”应用程序的记录编号。<br/>
                        </p>
                        <p>
                            * 请匹配“出差申请”应用中的“出差申请号”和字段代码。<br/>• 字段设置 ：“设为必填项” 和 “值为唯一” 。<br/>
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
    在“出差申请”应用的记录详情中，从“差旅费结算申请”应用获取“旅费”表格中的数据，并将其显示在“出差申请”应用的空白栏字段中。
</p>
<pre class="brush:js;toolbar:false">/*
 * 从其他应用程序引用表数据的示例程序
 * Copyright (c) 2020 Cybozu
 *
 * Licensed under the MIT License
 * https://opensource.org/licenses/mit-license.php
*/
(function() {
  &quot;use strict&quot;;
  kintone.events.on(&quot;app.record.detail.show&quot;, function(event) {
    // 请替换为&quot;差旅费结算申请&quot;的应用 ID
    var APP_ID = 123;
    // 获取作为「出差申请号」使用的「记录编号」
    var applicationNumber = kintone.app.record.getId();
    // 字段代码保存为变量
    var businessTripExpenses = &quot;旅费&quot;;
    var date = &quot;旅费日期&quot;;
    var transportation = &quot;交通工具&quot;;
    var summary = &quot;旅费摘要&quot;;
    var amount = &quot;旅费金额&quot;;
    var receipt = &quot;旅费发票&quot;;
    // 显示制作「差旅费结算申请应用」的情报的表格
    var tableHtml = &quot;&lt;thead&gt;&lt;tr&gt;&quot; +
        &quot;&lt;th&gt;&quot; + date + &quot;&lt;/th&gt;&quot; +
        &quot;&lt;th&gt;&quot; + transportation + &quot;&lt;/th&gt;&quot; +
        &quot;&lt;th&gt;&quot; + summary + &quot;&lt;/th&gt;&quot; +
        &quot;&lt;th&gt;&quot; + amount + &quot;&lt;/th&gt;&quot; +
        &quot;&lt;th&gt;&quot; + receipt + &quot;&lt;/th&gt;&quot; +
        &quot;&lt;/tr&gt;&quot; +
        &quot;&lt;/thead&gt;&quot; +
        &quot;&lt;/tbody&gt;&quot;;
    // 显示制作空字段的表格
    var tableEl = document.createElement(&quot;table&quot;);
    tableEl.id = &quot;table&quot;;
    tableEl.border = &quot;1&quot;;
    tableEl.style.textAlign = &quot;center&quot;;
    tableEl.style.padding = &quot;10px&quot;;
    tableEl.insertAdjacentHTML(&quot;afterbegin&quot;, tableHtml);
    kintone.app.record.getSpaceElement(&quot;tableSpace&quot;).appendChild(tableEl);
    // 从「差旅费结算申请应用」中获取相同的「出差申请号」
    var params = {
      &quot;app&quot;: APP_ID,
      &quot;query&quot;: &quot;出差申请号 = &quot; + applicationNumber
    };
    return kintone.api(kintone.api.url(&quot;/k/v1/records&quot;, true), &quot;GET&quot;, params).then(function(resp) {
      var travelExpenseAppRecords = resp.records;
      // 相同的「出差申请号」记录在「差旅费结算申请应用」中不存在的时候，显示错误
      if (travelExpenseAppRecords.length === 0) {
        window.alert(&quot;在「差旅费结算申请应用」中没有找到相同的「出差申请号」，不能显示「旅费」表格。&quot;);
        return event;
      }
      // 把获取到的「差旅费结算申请应用」的表格数据存储起来
      var tableRows = travelExpenseAppRecords[0][businessTripExpenses].value;
      var tableRef = document.getElementById(&quot;table&quot;);
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
      // 显示错误
      window.alert(&quot;发生错误，错误信息：&quot; + error.message);
      return event;
    });
  });
})();</pre>
<p>
    <br/>
</p>
<h4>
    &nbsp;<strong>动作确认</strong>
</h4>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            在“差旅费结算申请”应用中创建新记录并保存。<br/>在“旅费”表格中添加演示数据。
        </p>
    </li>
    <li>
        <p>
            在“出差申请”应用中创建新记录并保存。<br/>检查保存的记录详细信息屏幕的 tableSpace 空间字段，<br/>确认是否显示类似于“已完成的画面”中的表格。
        </p>
    </li>
</ol>
<h3>
    将表格数据导出到其他应用
</h3>
<h4>
    机制
</h4>
<p>
    具体而言<strong>，“保存记录时，在要引用表数据的应用中注册表格”</strong>。
</p>
<p>
    在此示例中，当您保存“旅行费用结算申请”应用的记录时，<br/>会将“旅费”表中的数据存储在“出差申请”应用中。 应用之间的关系图如下所示。
</p>
<p>
    <img src="https://developer.cybozu.io/hc/article_attachments/900002748226/2-2-outline-drawing.png" alt="2-2-outline-drawing.png" width="600" style="border-width:1px;border-style:solid;border-color:rgb(221,221,221);max-width:800px;vertical-align:middle;height:auto;"/>
</p>
<h4>
    已完成的图像
</h4>
<p>
    <img src="https://developer.cybozu.io/hc/article_attachments/900002792723/2-2-rendering_images.png" alt="2-2-rendering_images.png" style="border-width:1px;border-style:solid;border-color:rgb(221,221,221);max-width:800px;vertical-align:middle;height:auto;"/>
</p>
<h4>
    应用步骤
</h4>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>“出差申请”应用：</strong>
        </p>
    </li>
</ul>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            添加字段代码为“出差申请号”的记录编号字段。
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
                            用于标识“旅行费用结算申请”记录的数字。<br/>从同一“出差申请编号”的“差旅费用结算申请”记录中更新的表数据反映在“出差申请”记录中。
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
                        添加与“旅行费用结算申请”中的“差旅费”表相同的表。
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
            <strong>“差旅费结算申请”应用：</strong>
        </p>
    </li>
</ul>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            添加字段代码为“出差申请编号”的记录编号字段。<br/>
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
                            用于标识“出差申请”记录的编号。<br/>相同的“出差申请号”中的“出差申请”记录反映“差旅费结算申请”的表数据。
                        </p>
                        <p>
                            在此处输入要链接的“出差申请”应用的记录编号。<br/>
                        </p>
                        <p>
                            * 请匹配“出差申请”应用中的“出差申请号”和字段代码。<br/>• 字段设置 ：“设为必填项” 和 “值为唯一” 。
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
    在“旅行费用结算申请”应用程序的记录添加和编辑屏幕保存成功后的事件中，<br/>“旅行费用结算申请”应用的“旅费”表中的数据也会导出到“出差申请”应用程序的“旅费”表中。
</p>
<pre class="brush:js;toolbar:false">/*
 * 把表格数据保存到另一个应用的示例程序
 * Copyright (c) 2020 Cybozu
 *
 * Licensed under the MIT License
 * https://opensource.org/licenses/mit-license.php
*/
(function() {
  &quot;use strict&quot;;

  // 请替换成「出差申请应用」的应用ID
  var APP_ID = 123;

  // 把字段代码赋值给变量
  var businessTripExpenses = &quot;旅费&quot;;
  var applicationNumber = &quot;出差申请号&quot;;

  kintone.events.on([&quot;app.record.edit.submit&quot;, &quot;app.record.create.submit&quot;], function(event) {
    // 获取「差旅费结算申请应用」的子表格对象
    var travelExpenseAppRecord = event.record;
    var tableRows = travelExpenseAppRecord[businessTripExpenses].value;
    
    // 「差旅费结算申请应用」的子表格对象赋给数组
    var subtable = tableRows.map(function(row) {
      return {value: row.value};
    });

    // 从出差申请应用中获取相同的「出差申请号」的记录
    var paramForGet = {
      &quot;app&quot;: APP_ID,
      &quot;id&quot;: travelExpenseAppRecord[applicationNumber].value
    };
    return kintone.api(kintone.api.url(&quot;/k/v1/record&quot;, true), &quot;GET&quot;, paramForGet).then(function(resp) {

      var businessTripAppRecord = resp.record;

      // 「出差申请应用」中相同的「出差申请号」记录不存在时，显示错误
      if (!businessTripAppRecord) {
        window.alert(&quot;「出差申请应用」中相同的「出差申请号」记录不存在、不能更新差旅费结算申请&quot;);
        return event;
      }
      // 获取的出差申请数据に差旅费结算申请を更新
      var paramForPut = {
        &quot;app&quot;: APP_ID,
        &quot;id&quot;: travelExpenseAppRecord[applicationNumber].value,
        &quot;record&quot;: {
          // 差旅费结算申请(子表格)
          &quot;旅费&quot;: {
            &quot;value&quot;: subtable
          }
        }
      };

      // 在「出差申请应用」中反映出记录追加后的数据
      return kintone.api(kintone.api.url(&quot;/k/v1/record&quot;, true), &quot;PUT&quot;, paramForPut);

    }).then(function(resp2) {
      // 处理成功时的信息
      window.alert(&quot;出差申请应用に差旅费结算申请を反映しました!&quot;);
      return event;

    }).catch(function(error) {
      // 处理失败时的错误信息
      window.alert(&quot;向出差申请应用的反映失败了\n&quot; + error.message);
      return event;
    });
  });
})();</pre>
<h4>
    <strong>动作确认</strong>
</h4>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            在“出差申请”应用中创建新记录并保存。
        </p>
    </li>
    <li>
        <p>
            在“申请差旅费”应用中创建新记录并保存。<br/> 在“旅费”表中填入演示数据。
        </p>
    </li>
    <li>
        <p>
            保存“出差费用结算申请”应用的记录添加/编辑屏幕时，<br/>如果出现“出差申请应用反映差旅费用结算申请数据”消息，<br/>请在 1 中创建的“出差申请”记录的“差旅费”表中查看数据是否反映。
        </p>
    </li>
</ol>
<h2>
    方式 2：仅使用标准功能
</h2>
<p>
    我们已经介绍了如何使用 JavaScript 进行自定义，接下来将向您展示如何使用标准功能来实现这一切，这会显得容易一些。
</p>
<p>
    这个方法包含一些按钮操作，虽然稍微欠缺一些便利，但可以零编码。如果有兴趣的话请试试看。
</p>
<h3>
    机制
</h3>
<p>
    <strong>在别的应用中保存表数据，然后再那个应用中使用关联记录来引用数据。</strong>
</p>
<p>
    对于此示例中使用的应用
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>创建“差旅详情”应用</strong>
        </p>
    </li>
    <li>
        <p>
            <strong>将相当于“旅行费用结算申请”应用程序的表数据的内容保存到“差旅详情”应用</strong>
        </p>
    </li>
    <li>
        <p>
            <strong>使用相关记录从“旅行费用结算申请”和“出差申请”应用查看保存的“差旅费用详细信息”应用中的数据</strong>
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
    &nbsp;在新的“差旅详情”应用中注册数据是使用“申请差旅费用”应用中的操作<br/>按钮将一行表数据存储在一条记录中。
</p>
<h3>
    <strong>已完成的图像</strong>
</h3>
<p>
    <img src="https://developer.cybozu.io/hc/article_attachments/900002722403/1-rendering-image.png" alt="1-rendering-image.png" style="border-width:1px;border-style:solid;border-color:rgb(221,221,221);max-width:800px;vertical-align:middle;height:auto;"/>
</p>
<h3>
    <strong>应用步骤</strong>
</h3>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>“差旅详情”应用：</strong>
        </p>
    </li>
</ul>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            1. 创建新“差旅详情”应用。
        </p>
        <p>
            · 添加字段以保存与“旅行费用结算申请”应用程序的表数据等效的内容，如“日期”、“手段”、“差旅说明”、“金额”和“收据”。
        </p>
        <p>
            · 添加字段名称为“差旅申请编号”的字符串（一行）字段。
        </p>
        <p>
            · 有关要添加的字段的详细信息，请参阅下文。
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
                        输入旅行费用的“手段”信息。
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
            <strong>“申请差旅费报到”应用程序：</strong>
        </p>
    </li>
</ul>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            1. 删除“差旅费”表。
        </p>
    </li>
    <li>
        <p>
            2. 设置操作功能。<br/><br/>在操作设置的“关联字段”中，<br/>将“否”字段与“差旅详情”应用中的“出差申请编号”相关联。<br/><br/>※有关如何设置操作的信息，<a href="https://jp.cybozu.help/k/ja/user/app_settings/appaction/set_appaction.html">请参阅此处</a>。
        </p>
    </li>
    <li>
        <p>
            3. 添加相关记录列表字段，并将其设置为查看“差旅详情”应用中的数据。<br/><br/>有关要添加的字段的详细信息，请参阅下文。<br/>
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
                    <td>
                        · 浏览应用：差旅详情<br/>· 要显示的记录条件：此应用程序的字段“否”和要引用的应用字段“出差申请编号”<br/>· 要显示的字段：要在“申请差旅费用结算”应用中显示的字段<br/>· 有关如何设置相关记录的详细信息<a href="https://jp.cybozu.help/k/ja/user/app_settings/form/related_records/set_relatedrecords.html">，</a>请参阅此处。
                    </td>
                </tr>
            </tbody>
        </table>
    </li>
</ol>
<p>
    表格，想要让关联记录功能作为表格的替代品在“出差费用结算申请”应用中显示“旅费”的话，标准功能中的表格数据合计计算的功能就会失效了。
 &nbsp; &nbsp;想要计算含有关联记录里的金额数据的合计值的话，<a href="https://cybozudev.kf5.com/hc/kb/article/1032767/">请参照这篇文章。</a>
 &nbsp; &nbsp;想要试一试“表格数据参照”部分的效果的同学，“出差费用结算申请”的“旅费”
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>“出差申请”应用程序：</strong>
        </p>
    </li>
</ul>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            创建字段代码为“出差申请编号”的字符串（一行）字段。<br/><br/>（用作关联记录和操作关联的键）
        </p>
    </li>
    <li>
        <p>
            添加相关记录列表字段，并将其设置为查看“差旅详情”应用中的数据。<br/><br/>- 有关要添加的字段的详细信息，请参阅下文。<br/>
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
            浏览应用：差旅详情
        </p>
    </li>
    <li>
        <p>
            要显示的记录条件：此应用程序的字段“差旅申请编号”和“旅行费用申请编号”。
        </p>
    </li>
    <li>
        <p>
            要显示的字段：要在“申请差旅费用结算”应用中显示的字段
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
    还有许多其他有用的信息，如<a href="https://developer.cybozu.io/hc/ja/sections/360002613691">关联记录的自定义</a><br/>和<a href="https://developer.cybozu.io/hc/ja/sections/360002613651">数据活用的方法</a>请务必确认一下♪
</p>
<p>
    <br/>
</p>