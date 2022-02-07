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
            ※其他字段任意设置。<br/>※所用时间的计算公式为：任务完成时间-开始执行<br/><br/>
        </p>
    </li>
    <li>
        <p>
            <img src="https://files.kf5.com/attachments/download/23361/12880758/0016200d04a3028c22977e84e52bbe3/"/><br/>
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
            Luxon<br/>https://js.cybozu.com/luxon/2.1.1/luxon.min.js (使用version 2.1.1)
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
* Copyright (c) 2021 Cybozu    
*    
* Licensed under the MIT License    
*/    
(function () {    
    &#39;use strict&#39;;    
    var date = luxon.DateTime.local();    
    // 记录创建/编辑页面显示时    
    var eventsCreateShow = [&#39;app.record.create.show&#39;, &#39;app.record.edit.show&#39;, &#39;app.record.index.edit.show&#39;];    
    kintone.events.on(eventsCreateShow, function(event){    
        var record = event.record;    
        // 设置字段不可编辑
        record[&#39;任务完成时间&#39;][&#39;disabled&#39;] = true;    
        record[&#39;负责人&#39;][&#39;disabled&#39;] = true;    
        if (event.type === &#39;app.record.create.show&#39;){    
            // 指定从今日起2天后
            record[&#39;任务期限&#39;][&#39;value&#39;] = date.plus({days: 2}).toISODate();    
            record[&#39;任务完成时间&#39;][&#39;value&#39;] = null;    
            record[&#39;负责人&#39;][&#39;value&#39;] = [];    
        }    
        return event;    
    });    
    // 流程管理的动作执行时
    kintone.events.on(&#39;app.record.detail.process.proceed&#39;, function(event){    
    var record = event.record;    
    var nStatus = event.nextStatus.value;    
    // 状态为【完成】时，自动设置任务完成日和负责人
    if (nStatus === &#39;完了&#39;){    
        var user = kintone.getLoginUser();    
        record[&#39;任务完成时间&#39;][&#39;value&#39;] = date.toISO();    
        record[&#39;负责人&#39;][&#39;value&#39;][0] = {code : user.code};    
    }    
    return event;    
    });    
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
    以下是【通过JavaScript / CSS自定义】页面的设置范例。<br/><br/>
</p>
<p>
    <img src="https://files.kf5.com/attachments/download/23361/12880805/0016200d19ad5fc29003c12bcae1a02/"/>
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
            <a href="https://cybozudev.kf5.com/hc/kb/article/206857#step3">记录列表页面的行内编辑开始时的事件</a>
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