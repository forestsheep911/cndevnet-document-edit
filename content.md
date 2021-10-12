<p>
    本次将于2021年11月14日进行定期维护，在此向大家介绍维护时与 kintone API 相关的更新信息。<br/>如更新通知的内容有需要添加或更改，届时将在本文章后面追加更改或新增的内容。<br/>另外，还将依次更改受API更新影响的 API 文档。
</p>
<h2>
    kintone
</h2>
<h3>
    本月的 kintone API
</h3>
<p>
    在11月的版本中，追加了是否许可不属于空间的应用的创建，以及只有空间管理者能创建空间内应用的设置。<br/>伴随着上述功能，相应地增加了测试环境中应用创建的 API。
</p>
<h3>
    kintone REST API
</h3>
<h4>
    功能改善
</h4>
<p>
    在11月的版本中，追加了是否许可不属于空间的应用的创建，以及只有空间管理者能创建空间内应用的设置。伴随着上述功能，对应了以下内容
</p>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>在 kintone 的系统管理中，如果选择了“不允许创建不属于空间的应用”这个选项，再创建不属于空间的应用时，就会得到报错而不能创建应用。</strong>
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p>
                对象 API
            </p>
        </li>
    </ul>
</ul>
<p>
    &nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#4fc3f6;">●</span> <a href="https://cybozudev.kf5.com/hc/kb/article/1300355/#step1">在测试环境中创建应用</a> /k/v1/preview/app.json
</p>
<p>
    <strong>在空间管理中，如果选择了“只有管理员能创建应用”这个选项，管理者以外的用户再创建属于空间的应用时，就会得到报错而不能创建应用。</strong>
</p>
<ul class=" list-paddingleft-2" style="list-style-type: square;">
    <li>
        <p>
            对象 API
        </p>
    </li>
</ul>
<p>
    &nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#4fc3f6;">●</span> <a href="https://cybozudev.kf5.com/hc/kb/article/1300355/#step1">在测试环境中创建应用</a> /k/v1/preview/app.json
</p>
<h2>
    .cn 共通
</h2>
<h3>
    User API
</h3>
<h4>
    新增功能
</h4>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>增加了以 JSON 形式来删除组的 API</strong>
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p>
                对象 API
            </p>
        </li>
    </ul>
</ul>
<p>
    &nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#4fc3f6;">●</span> /v1/groups.json [DELETE]
</p>
<p>
    备注
</p>
<p>
    &nbsp;&nbsp;&nbsp;&nbsp;<span style="color:#4fc3f6;">●</span> <a href="https://cybozudev.kf5.com/hc/kb/article/1323594">导入组API</a>&nbsp;的 JSON 版（只是删除处理）。
</p>
<h3>
    其他
</h3>
<h4>
    新增功能
</h4>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <strong>在 .cn 共通管理里可以变更 Referrer-Policy 的设置了。</strong><br/><strong>如果有在外部整合中使用了 Referrer 来自定义开发的情况，请确认其设置。</strong>
        </p>
    </li>
</ul>
<p>
    <br/>
</p>
