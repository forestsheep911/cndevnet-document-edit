<p class="operaCheck">
    Moment.js已进入维护状态，推荐转为使用更加新的<a href="https://momentjs.com/docs/#/-project-status/recommendations">可替代Moment.js进行日期处理的库</a>。替代库的候选之一<a href="https://github.com/moment/luxon">Luxon</a>，我们也公开了<a href="https://developer.cybozu.io/hc/ja/articles/900000985463">在kintone自定义中的导入Luxon的方法</a>（日语）
</p>
<h1>
    <span style="font-size:24px;font-weight:700;">Index</span>
</h1>
<ul class="anchor-link list-paddingleft-2">
    <li>
        <p>
            <a href="#step1">概 要</a>
        </p>
    </li>
    <li>
        <p>
            <a href="#step2">事前准备</a>
        </p>
    </li>
    <li>
        <p>
            <a href="#step3">程序范例</a>
        </p>
    </li>
</ul>
<h2>
    <a style="color:rgb(21,142,194);"></a>概 要
</h2>
<p>
    本范例介绍当故障处理应用的流程状态变为【完成】时，系统自动记录任务完成日及负责人（登录用户）的自定义方法。另外，还加入以下功能。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            添加记录时自动生成编号
        </p>
    </li>
    <li>
        <p>
            任务完成日字段和负责人字段设为不可编辑
        </p>
    </li>
    <li>
        <p>
            重复利用记录时，自动清除任务完成日和负责人字段中的数据
        </p>
    </li>
</ul>
<h3>
    完成图
</h3>
<p>
    &nbsp;<img src="https://cybozudev.kf5.com/attachments/download/1119146/00157f48976227e459076543a7f3a53/" alt="00157f48976227e459076543a7f3a53"/>
</p>
<h2>
    <a style="color:rgb(21,142,194);"></a>事前准备
</h2>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            创建【故障处理管理】应用。<br/>表单设置详情如下：
        </p>
        <table style="font-size:16px;">
            <tbody>
                <tr class="firstRow">
                    <th>
                        <p>
                            字段名称
                        </p>
                    </th>
                    <th>
                        <p>
                            字段类型
                        </p>
                    </th>
                    <th>
                        <p>
                            字段代码
                        </p>
                    </th>
                </tr>
                <tr>
                    <td>
                        <p>
                            受理编号
                        </p>
                    </td>
                    <td>
                        <p>
                            单行文本框
                        </p>
                    </td>
                    <td>
                        <p>
                            受理编号
                        </p>
                    </td>
                </tr>
                <tr>
                    <td>
                        <p>
                            类型
                        </p>
                    </td>
                    <td>
                        <p>
                            单选框
                        </p>
                    </td>
                    <td>
                        <p>
                            类型
                        </p>
                    </td>
                </tr>
                <tr>
                    <td>
                        <p>
                            任务期限
                        </p>
                    </td>
                    <td>
                        <p>
                            日期<br/>
                        </p>
                    </td>
                    <td>
                        <p>
                            任务期限
                        </p>
                    </td>
                </tr>
                <tr>
                    <td>
                        <p>
                            开始执行
                        </p>
                    </td>
                    <td>
                        <p>
                            创建时间
                        </p>
                    </td>
                    <td>
                        <p>
                            开始执行
                        </p>
                    </td>
                </tr>
                <tr>
                    <td>
                        <p>
                            任务完成时间
                        </p>
                    </td>
                    <td>
                        <p>
                            日期与时间
                        </p>
                    </td>
                    <td>
                        <p>
                            任务完成时间
                        </p>
                    </td>
                </tr>
                <tr>
                    <td>
                        <p>
                            负责人
                        </p>
                    </td>
                    <td>
                        <p>
                            选择用户
                        </p>
                    </td>
                    <td>
                        <p>
                            负责人
                        </p>
                    </td>
                </tr>
                <tr>
                    <td>
                        <p>
                            所用时间
                        </p>
                    </td>
                    <td>
                        <p>
                            计算
                        </p>
                    </td>
                    <td>
                        <p>
                            所用时间
                        </p>
                    </td>
                </tr>
            </tbody>
        </table>
        <p>
            ※其他字段任意设置。<br/>※所用时间的计算公式为：任务完成时间-开始执行<br/><img src="https://cybozudev.kf5.com/attachments/download/1119173/00157f48cd4a918661335fa46614986/" alt="00157f48cd4a918661335fa46614986"/><br/>
        </p>
    </li>
    <li>
        <p>
            流程管理的设置<br/>状态有：未处理、受理、调查中、执行中、完成、保留<br/>具体流程设置如下：<br/><img src="https://files.kf5.com/attachments/download/23361/12529867/001618b7de22094c5987b7161f03421/" alt="001618b7de22094c5987b7161f03421"/><br/>
        </p>
    </li>
</ul>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            编辑器<br/>选择符合自己使用习惯的文本编辑器。
        </p>
    </li>
</ul>
<h2>
    <a style="color:rgb(21,142,194);"></a>程序范例
</h2>
<h3>
    注意事项
</h3>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            直接使用此处提供的程序范例的情况，才望子不予以保证程序的正常运行
        </p>
    </li>
    <li>
        <p>
            才望子不提供对程序范例的技术支持
        </p>
    </li>
    <li>
        <p>
            有些地方使用XMLHttpRequest 进行同步处理。处理过程中，浏览器可能会卡住。另外，部分浏览器无法使用XMLHttpRequest ，请注意！
        </p>
    </li>
</ul>
<h3>
    PC专用的JavaScript文件
</h3>
<p>
    在应用设置页面打开【通过JavaScript / CSS自定义】，从<a href="https://cybozudev.kf5.com/hc/kb/article/206405">Cybozu CDN</a>&nbsp;中选择以下库。
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            Mement.js<br/>https://js.cybozu.com/momentjs/2.8.4/moment-with-locales.min.js (使用version 2.8.4 )
        </p>
    </li>
</ul>
<h3>
    JavaScript 范例
</h3>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            将以下代码拷贝到编辑器，文件命名为【sample.js】，文字编码设为【UTF-8】、无BOM，保存<br/>※文件名任意，但是文件的扩展名要指定为【js】
        </p>
    </li>
    <li>
        <p>
            在【通过JavaScript / CSS自定义】页面中上传保存的文件
        </p>
        <p>
            <br/>
        </p>
        <pre class="brush:js;toolbar:false">/*
 * 故障处理管理应用的程序范例
 * Copyright (c) 2014 Cybozu
 *
 * Licensed under the MIT License
 */
(function() {
    &quot;use strict&quot;;
    // 记录创建/编辑页面显示时
    var eventsCreateShow = [&#39;app.record.create.show&#39;, &#39;app.record.index.create.show&#39;,
                            &#39;app.record.edit.show&#39;, &#39;app.record.index.edit.show&#39;];
    kintone.events.on(eventsCreateShow, function(event) {
        var record = event.record;
        // 设置字段不可编辑
        record[&#39;受理编号&#39;][&#39;disabled&#39;] = true;
        record[&#39;任务完成时间&#39;][&#39;disabled&#39;] = true;
        record[&#39;负责人&#39;][&#39;disabled&#39;] = true;
        switch (event.type) {
            case &#39;app.record.create.show&#39;:
            case &#39;app.record.index.create.show&#39;:
                record[&#39;受理编号&#39;][&#39;value&#39;] = &quot;&quot;;
                // 指定从今日起2天后
                record[&#39;任务期限&#39;][&#39;value&#39;] = moment().add(&quot;days&quot;, 2).format(&quot;YYYY-MM-DD&quot;);
                record[&#39;任务完成时间&#39;][&#39;value&#39;] = null;
                record[&#39;负责人&#39;][&#39;value&#39;] = [];
                break;
            default:
                break;
        }
        return event;
    });
    // 记录添加页面保存时
    var eventsSubmit = [&#39;app.record.create.submit&#39;, &#39;app.record.edit.submit&#39;,
                        &#39;app.record.index.edit.submit&#39;];
    kintone.events.on(eventsSubmit, function(event) {
        var record = event.record;
        // 【受理编号】中自动生成【CD-YYMM-XXXX】格式的编号
        if (!record[&#39;受理编号&#39;][&#39;value&#39;]) {
            var recId = 1;
            // 获取记录编号的最大值
            var appId = kintone.app.getId();
            // 设置URL
            var appUrl = kintone.api.url(
                &#39;/k/v1/records&#39;, true) + &#39;?app=&#39; + appId + &#39;&amp;query=&#39; + encodeURI(&#39;order by 记录编号 desc limit 1&#39;
                );
            var xmlHttp;
            // 为了使用记录编号的最大值，需要同步处理
            xmlHttp = new XMLHttpRequest();
            xmlHttp.open(&quot;GET&quot;, appUrl, false);
            xmlHttp.setRequestHeader(&#39;X-Requested-With&#39;, &#39;XMLHttpRequest&#39;);
            xmlHttp.send(null);
            if (xmlHttp.status === 200) {
                if (window.JSON) {
                    var obj = JSON.parse(xmlHttp.responseText);
                    if (obj.records[0] !== null) {
                        try {
                            recId = parseInt(obj.records[0][&#39;$id&#39;][&#39;value&#39;], 10) + 1;
                        } catch(e) {
                            event.error = &#39;无法获取受理编号。&#39;;
                        }
                    }
                    //设置自动生成编号
                    var r4 = zeroformat(recId, 4);
                    var m = moment();
                    var shipmentNo = &quot;CD&quot; + m.format(&quot;YY&quot;) + m.format(&quot;MM&quot;) + &quot;-&quot; + r4;
                    record[&#39;受理编号&#39;][&#39;value&#39;] = shipmentNo;
                } else {
                    event.error = xmlHttp.statusText;
                }
            } else {
                record.error = &#39;无法获取受理编号。&#39;;
            }
        }
        return event;
    });
    // 流程管理的动作执行时
    kintone.events.on([&quot;app.record.detail.process.proceed&quot;], function(event) {
        var record = event.record;
        var nStatus = event.nextStatus.value;
        // 状态为【完成】时，自动设置任务完成日和负责人
        switch (nStatus) {
            case &quot;完成&quot;:
                var user = kintone.getLoginUser();
                record[&#39;任务完成时间&#39;][&#39;value&#39;] = moment().format(&quot;YYYY-MM-DDTHH:mmZ&quot;);
                record[&#39;负责人&#39;][&#39;value&#39;][0] = {code: user.code};
                break;
        }
        return event;
    });
    // 统一位数的函数
    function zeroformat(v, n) {
        var vl = String(v).length;
        if (n &gt; vl) {
            return (new Array((n - vl) + 1).join(0)) + v;
        } else {
            return v;
        }
    }
})();</pre>
        <p>
            <br/>
        </p>
    </li>
</ul>
<h3>
    设置的页面
</h3>
<p>
    以下是【通过JavaScript / CSS自定义】页面的设置范例。<br/><img src="https://cybozudev.kf5.com/attachments/download/1119198/00157f48f72efbff743f157a0945db0/" alt="00157f48f72efbff743f157a0945db0"/>
</p>
<h3>
    使用的API
</h3>
<ol class=" list-paddingleft-2">
    <li>
        <p>
            <a href="https://cybozudev.kf5.com/hc/kb/article/205422#step2">添加事件句柄</a>
        </p>
    </li>
    <li>
        <p>
            <a href="https://cybozudev.kf5.com/hc/kb/article/206878#step1">记录添加页面显示时的事件</a>
        </p>
    </li>
    <li>
        <p>
            <a href="https://cybozudev.kf5.com/hc/kb/article/206917#step1">记录编辑页面显示时的事件</a>
        </p>
    </li>
    <li>
        <p>
            <a href="https://cybozudev.kf5.com/hc/kb/article/206878#step2">记录添加页面在执行保存之前的事件</a>
        </p>
    </li>
    <li>
        <p>
            <a href="https://cybozudev.kf5.com/hc/kb/article/206917#step2">记录编辑页面在执行保存之前的事件</a>
        </p>
    </li>
    <li>
        <p>
            <a href="https://cybozudev.kf5.com/hc/kb/article/206857/#step2">在记录列表页面点击【保存】按钮时的事件</a>
        </p>
    </li>
    <li>
        <p>
            <a href="https://cybozudev.kf5.com/hc/kb/article/207506#step2">获取URL（无查询字符串）</a>
        </p>
    </li>
    <li>
        <p>
            <a href="https://cybozudev.kf5.com/hc/kb/article/206907#step3">流程管理的动作执行事件</a>
        </p>
    </li>
</ol>
<p>
    <br/>
</p>