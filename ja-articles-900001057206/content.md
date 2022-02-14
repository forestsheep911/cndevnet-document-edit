<h1>
    Index
</h1>
<ul class="anchor-link list-paddingleft-2">
    <li>
        <p>
            <a href="#step1">前言</a>
        </p>
    </li>
    <li>
        <p>
            <a href="#step2">应用的准备</a>
        </p>
    </li>
    <li>
        <p>
            <a href="#step3">编写查询语句的方法</a>
        </p>
    </li>
    <li>
        <p>
            <a href="#step4">查询语句中变量的赋值</a>
        </p>
    </li>
    <li>
        <p>
            <a href="#step5">最后</a>
        </p>
    </li>
</ul>
<h2>
    前言
</h2>
<p>
    <span style="font-size:16px;">本文是介绍编写查询语句的基础知识。<br/></span><span style="font-size:16px;">您可以使用查询语句来获取按特定条件筛选的特定记录。<br/></span><span style="font-size:16px;">为了更好地理解如何编写查询语句，这里结合应用来说明。<br/></span><span style="font-size:16px;">当然，也可以不使用应用只参考如何编写查询语句，</span><span style="font-size:16px;">希望本文对您的开发有所帮助。</span>
</p>
<h2>
    应用的准备
</h2>
<p>
    从kintone应用商店添加“来询管理”。（参考：<a href="https://help.cybozu.cn/k/zh/user/create_app/add_app_store.html" target="_blank" rel="noreferrer noopener">从 kintone 商城中添加应用</a>）
</p>
<p>
    添加此应用后，<br/>1.首先在“更改应用的设置”中更改字段代码，如下所示：<br/>
</p>
<table>
    <tbody>
        <tr class="firstRow">
            <th>
                字段名称
            </th>
            <th>
                字段代码
            </th>
        </tr>
        <tr>
            <td>
                对应时间
            </td>
            <td>
                ResponseDate
            </td>
        </tr>
        <tr>
            <td>
                对应内容
            </td>
            <td>
                Correspondence
            </td>
        </tr>
    </tbody>
</table>
<p>
    2.其次任意添加几条记录。其中一条记录如下所示：
</p>
<table>
    <tbody>
        <tr class="firstRow">
            <th>
                字段名称
            </th>
            <th>
                值
            </th>
        </tr>
        <tr>
            <td>
                顾客名
            </td>
            <td>
                才望子有限公司
            </td>
        </tr>
        <tr>
            <td>
                期限
            </td>
            <td>
                2018-02-01
            </td>
        </tr>
    </tbody>
</table>
<h2>
    编写查询语句的方法
</h2>
<h3>
    关于表达式的格式
</h3>
<p>
    查询语句主要由下列的形式构成：
</p>
<pre class="brush:bash;toolbar:false;">&lt;字段代码&gt; &lt;运算符&gt; &lt;值 或 函数&gt;</pre>
<p>
    若希望了解有关查询语句规范的详细信息，以及每个字段可用的运算符和函数，请查阅<a href="https://cybozudev.kf5.com/hc/kb/article/201594#step3">这里</a>。<br/>现在，让我们实际获取记录。<a href="#step4">本文末尾</a>提供了在 JavaScript 中指定查询语句以获取记录的范例。
</p>
<h3>
    指定单行文本框的值
</h3>
<p>
    让我们通过指定以下条件来实际获取记录。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>“顾客名”字段的值是“xx有限公司”</strong>（完全一致）<br/>指定完全匹配的字符串时，请使用“=”运算符，如下所示：
        </p>
        <pre>Customer = &quot;才望子有限公司&quot;</pre>
    </li>
</ul>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>在“顾客名”字段的值中包含“有限公司”</strong>（部分一致）<br/>指定部分匹配的字符串时，请使用“like”运算符，如下所示：
        </p>
        <pre>Customer like &quot;有限公司&quot;</pre>
    </li>
</ul>
<h3>
    指定下拉菜单的值
</h3>
<p>
    让我们通过指定以下条件来实际获取记录。<br/>指定下拉菜单的值时，如下所示请使用“in”和“not in”运算符。<br/>使用“in”和“not in”运算符时，值必须用 () 括起来。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>“对应状况”字段的值包含“对应中”和“未对应”</strong><br/>
        </p>
        <pre>Status in (&quot;对应中&quot;,&quot;未对应&quot;)</pre>
    </li>
</ul>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>“对应状况”字段的值不包含“完了”</strong>
        </p>
        <pre>Status not in (&quot;完了&quot;)</pre>
    </li>
</ul>
<p>
    此外，以下字段可以使用“in”、“not in”运算符获取记录，类似于下拉菜单。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            复选框
        </p>
    </li>
    <li>
        <p>
            单选框
        </p>
    </li>
    <li>
        <p>
            多选
        </p>
    </li>
</ul>
<h3>
    指定日期字段的值
</h3>
<p>
    让我们通过指定以下条件来实际获取记录。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>“期限”字段的值是“2018-02-01”</strong>
        </p>
        <pre>LimitDay = &quot;2018-02-01&quot;</pre>
    </li>
</ul>
<p>
    日期字段除了可以指定某一个值也可以指定某一个范围。<br/>让我们通过指定以下条件来实际获取记录。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>“期限”字段的值从“<strong>2018-02-01</strong>”到“<strong>2018-03-01</strong>”</strong>
        </p>
        <pre> LimitDay &gt;= &quot;2018-02-01&quot; and LimitDay &lt;= &quot;2018-03-01&quot;</pre>
    </li>
</ul>
<p>
    因此，当指定多个条件时，使用“and”运算符来连接表达式。
</p>
<h3>
    获取表格内字段的值
</h3>
<p>
    “=”、“!=”运算符不能用于获取表格内字段的值。<br/>作为替代，必须使用“in”、“not in”运算符。
</p>
<p>
    让我们用以下条件实际来获取下字段吧。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>“对应时间”字段的值是“<strong>2018-01-05 14:00</strong>”</strong>
        </p>
        <pre>ResponseDate in (&quot;2018-01-05T05:00:00Z&quot;)</pre>
    </li>
</ul>
<p>
    就如“指定日期字段的值”中所述，通常日期字段或日期与时间字段使用“=”、“!=”运算符。但是请注意，表格中不能使用。
</p>
<p>
    以上，我们介绍了指定单个字段的查询语句。接下来介绍如何指定多个字段的方法。
</p>
<h3>
    指定多个字段和条件
</h3>
<p>
    正如“指定日期字段的值”末尾指定的那样，可以使用“and”、“or”运算符指定多个条件。
</p>
<p>
    首先，让我们使用“and”运算符为查询语句中的多个字段指定条件。
</p>
<h4>
    使用“and”指定条件
</h4>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>“期限”字段的值在“今天”之前</strong>
        </p>
    </li>
    <li>
        <p>
            <strong>“对应状况”字段的值不包含“完了”</strong>
        </p>
        <pre>LimitDay &lt; TODAY() and Status not in (&quot;完了&quot;)</pre>
    </li>
</ul>
<p>
    指定“期限”字段的条件为“TODAY()”函数。“TODAY()”函数是查询语句中可用的函数之一。<br/>使用该函数，可以轻松的指定条件，比如“今天”、“上周”、“下周”，而无需指定每个日期。<br/>（其他函数请参阅<a href="https://cybozudev.kf5.com/hc/kb/article/201594#step3" target="_blank" rel="noreferrer noopener">此处</a>。）
</p>
<h4>
    使用“order by”指定条件
</h4>
<p>
    接下来，让我们在之前的条件上添加另一个条件。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>“期限”字段的值在“今天”之前</strong>
        </p>
    </li>
    <li>
        <p>
            <strong>“对应状况”字段的值不包含“完了”</strong>
        </p>
    </li>
    <li>
        <p>
            <strong>“期限”字段的值按“升序”获取</strong>
        </p>
        <pre> LimitDay &lt; TODAY() and Status not in (&quot;完了&quot;) order by LimitDay asc</pre>
    </li>
</ul>
<p>
    这样就可以使用“order by”选项对记录的输出顺序进行排序。
</p>
<h3>
    表达式分组
</h3>
<p>
    为多个字段指定多个条件时，请对表达式进行分组。<br/>可以通过括号“()”括起来对表达式进行分组。<br/>通过分组，可以指定更详细的条件。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>“来询种类”字段的值是“其他”<br/></strong><strong>或者</strong>
        </p>
    </li>
    <li>
        <p>
            <strong>“期限”字段值的范围从“<strong>2018-02-01</strong>”到“<strong>2018-03-01</strong>”</strong>
        </p>
        <pre> (QType in (&quot;其他&quot;)) or (LimitDay &gt;= &quot;2018-02-01&quot; and LimitDay &lt;= &quot;2018-03-01&quot;)</pre>
    </li>
</ul>
<h2>
    查询语句中变量的赋值
</h2>
<p>
    最后介绍一下分配变量的方法。<br/>在实际使用&nbsp;JavaScript 编写查询语句时，有些情况下查询语句中可能包含变量。<br/>例如，将从记录中获取到的值分配给查询语句。<br/>为了使用这些动态值编写查询语句，需要将字符串与变量分开。
</p>
<p>
    让我们假设以下情况：
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>打开记录时，希望获取到具有相同“期限”值的其他记录。</strong>
        </p>
    </li>
</ul>
<p>
    要实现上述条件，必须按下列顺序进行处理
</p>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            获取打开的记录的值
        </p>
    </li>
    <li>
        <p>
            将获取到的值分配给查询语句
        </p>
    </li>
</ol>
<p>
    让我们实际看看代码。
</p>
<pre class="brush:js;toolbar:false">(function() {
  &#39;use strict&#39;;

  kintone.events.on(&#39;app.record.detail.show&#39;, function(event) {
    var record = event.record;
    var limitDay = record.LimitDay.value;
    var query = &#39;LimitDay = &quot;&#39; + limitDay + &#39;&quot;&#39;;

    var body = {
      &#39;app&#39;: kintone.app.getId(),
      &#39;query&#39;: query
    };

    kintone.api(kintone.api.url(&#39;/k/v1/records&#39;, true), &#39;GET&#39;, body, function(resp) {
      // success
      console.log(resp);
    }, function(error) {
      // error
      console.log(error);
    });
    return event;
  });
})();</pre>
<h4>
    重点
</h4>
<p>
    以上代码的第7行是重点。
</p>
<pre class="brush:js;toolbar:false">    var query = &#39;LimitDay = &quot;&#39; + limitDay + &#39;&quot;&#39;;</pre>
<p>
    记录中“期限”字段的值被分配给作为获取记录的条件的查询语句。<br/>因此，为了将 JavsScript 中的变量分配给查询语句，必须将其组合为字符串。
</p>
<h2>
    最后
</h2>
<p>
    一旦掌握了编写诀窍，就可以轻松编写查询语句。<br/>这次介绍了查询语句的编写方法，其实还有一种更简单的方法可以组织查询语句。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <a href="https://developer.cybozu.io/hc/ja/articles/360033708051#step3">轻松创建批量获取记录API的查询语句（日文）</a>
        </p>
    </li>
</ul>
<p>
    可以通过组合查询语句来获取各种数据，在实际开发中经常用到。<br/>希望您能利用查询语句来更方便地自定义kintone。
</p>
<p>
    <br/>
</p>
