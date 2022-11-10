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
            <a href="#step2">前期准备</a>
        </p>
    </li>
    <li>
        <p>
            <a href="#step3">代码范例</a>
        </p>
    </li>
    <li>
        <p>
            <a href="#step4">代码解说</a>
        </p>
    </li>
</ul>
<p>
    <span style="font-size:24px;font-weight:700;">前言</span>
</p>
<h3>
    Notion简介
</h3>
<p>
    近几年，有一款叫Notion的产品异常火爆，它是集笔记、任务管理、Wiki、数据管理为一体的产品，他主打两个理念「模块化」和「All-in-one」，Notion最有魅力的还是引进了Database和双向链的理念
</p>
<p>
    Notion也算是一个渐进式的工具产品，渐进式你可以理解为，可以简单的当笔记工具用，也可以当个人或小团队的工作知识库和任务管理工具用。
</p>
<h3>
    Notion与kintone
</h3>
<p>
    在实际使用Notion的过程中，我发现它的Database数据形式有着重要地位，它和Notion其他一些特色功能融合后，充分放大了其扩展性，自由性，和灵活性。Notion的Database属于关系型数据库的范畴，我不禁想到，关系型数据库的形式也是kintone App的核心内容，所以那他们之间一定是可以互通的。
</p>
<p>
    今天我们就来探讨一下如何进行Notion和kintone之间的数据转换。
</p>
<h2>
    探讨范围
</h2>
<p>
    本着抛砖引玉的理念，本文想要做的更多是启发开发思路，而非那种可以拿来即用成熟产品。所以探讨和演示的范围不会面面俱到。
</p>
<h3>
    数据对接
</h3>
<p>
    说到数据对接，本应该是双向的，但本文只讨论Notion向kintone的单向转换。因为反向转换的话，完全可以反推出来，有需求的读者可以自行推演。
</p>
<h3>
    字段类型
</h3>
<p>
    Notion和kintone的二维结构表格中的字段，都有自己类型的设计，有相似的，也有不同的。本文中所演示的，只是一部分字段的转换，而且字段的对应关系也非严格匹配。读者可根据实际需求，或增加更多转换字段，或更改的字段类型对应关系。
</p>
<p>
    譬如，Notion中的字段类型“Text”，其实技术上可以叫“RichText”（带丰富格式的文本），但我转换到kintone时，用的只是普通的“单行文本框”。
</p>
<h2>
    前期准备
</h2>
<h3>
    Notion方面的准备
</h3>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            在Notion中建立一个database，建立几个想要对接字段 。这里我建立了一个书店的表格。
        </p>
    </li>
    <li>
        <p>
            <img src="https://files.kf5.com/attachments/download/23361/14160799/001636475758ce7dd24bce186d67b9b/" alt="001636475758ce7dd24bce186d67b9b"/><br/>
        </p>
    </li>
    <li>
        <p>
            要使用Notion的API，则先要创建一个integration。integration字面翻译叫做“融入”，这是Notion自己的叫法，我们可以简单理解为平时经常说的API Token。创建方式见<a href="https://www.notion.so/help/create-integrations-with-the-notion-api">官方文档</a>。创建成功后你会得到一个Secrets字符串。&nbsp;
        </p>
    </li>
    <li>
        <p>
            <img src="https://files.kf5.com/attachments/download/23361/14160802/00163647575b84f88c644095bd9a9e2/" alt="00163647575b84f88c644095bd9a9e2"/><br/>
        </p>
    </li>
    <li>
        <p>
            有了integration之后，还要把它连接到刚才的database中，使得在调用API时，获得此database的访问权限。在最右上角的三个点图标中，找到Add connections，输入刚才的integration名，确认后连接成功。&nbsp;
        </p>
    </li>
    <li>
        <p>
            <img src="https://files.kf5.com/attachments/download/23361/14160800/00163647575931d9df2e0ff47445c3a/" alt="00163647575931d9df2e0ff47445c3a"/><br/>
        </p>
    </li>
</ul>
<h3>
    kintone方面的准备
</h3>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            建立一个kintone App，用来接受Notion的database数据，所以字段类型必须选择合适的。 书名、ISBN、作者、可以选择单行文本框，定价选择数值，标签可以选择复选框或是多选。
        </p>
    </li>
    <li>
        <p>
            <img src="https://files.kf5.com/attachments/download/23361/14160803/00163647575c9ade0f4df9263757316/" alt="00163647575c9ade0f4df9263757316"/><br/>
        </p>
    </li>
    <li>
        <p>
            给每个字段设置好字段代码，以备在程序中使用。我以json object的形式给出，属性名是字段名，属性值是字段代码，将来程序里能直接用得上。
        </p>
    </li>
</ul>
<pre class="brush:js;toolbar:false"> {
    书名: &#39;book_name&#39;,
    ISBN: &#39;isbn&#39;,
    作者: &#39;author&#39;,
    定价: &#39;price&#39;,
    标签: &#39;label&#39;,
  }</pre>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            创建token，以便将来程序中访问此App。&nbsp;
        </p>
    </li>
    <li>
        <p>
            <img src="https://files.kf5.com/attachments/download/23361/14160801/00163647575a49544f86f1188ef8358/" alt="00163647575a49544f86f1188ef8358"/><br/>
        </p>
        <h3>
            程序编写运行环境方面
        </h3>
    </li>
    <li>
        <p>
            本文中所演示的代码，都是在nodejs的npm模式下编写调试的，我们也强烈建议您也在这种模式下来编写程序。而且我们将分别使用Notion和kintone的SDK，这种模式下引用库也会相对方便一些。下面是package.json文件的一部分相关设置，供您参考。
        </p>
    </li>
</ul>
<pre class="brush:js;toolbar:false">{
    &quot;name&quot;: &quot;notion2kintone&quot;,
    &quot;version&quot;: &quot;1.0.0&quot;,
    &quot;type&quot;: &quot;module&quot;,
    &quot;dependencies&quot;: {
      &quot;@kintone/rest-api-client&quot;: &quot;^3.1.11&quot;,
      &quot;@notionhq/client&quot;: &quot;^2.1.1&quot;
    }
  }</pre>
<h2>
    代码范例
</h2>
<pre class="brush:js;toolbar:false">import { Client } from &#39;@notionhq/client&#39;
import { KintoneRestAPIClient } from &#39;@kintone/rest-api-client&#39;
// 用Notion的sdk创建一个客户端
const notion = new Client({ auth: &#39;secret_CNqoK82a5MQaBosS6jMEahHbQhX2806zNljRgShGuK&#39; })
// 获取Notion数据
const iterateDB = async () =&gt; {
  // 获取Notion的database
  const dbArray = await notion.databases.query({ database_id: &#39;b269007a9a44488d9ff7fe0c646179c9&#39; })
  // 获取database的属性
  const propertitsSet = await Promise.all(
    // database的每条记录是一个page，我们需要用它来获取每个属性
    dbArray.results.map(async (pageRecord) =&gt; {
      // 获取database的每一条记录
      const record = await Promise.all(
        // 遍历每条记录的每个属性名
        Object.keys(pageRecord.properties).map(async (propertyName) =&gt; {
          // 调用Notion的API，给出page id和属性id，拿到每条记录的每个属性值
          const propertyData = await notion.pages.properties.retrieve({
            page_id: pageRecord.id,
            property_id: pageRecord.properties[propertyName].id,
          })
          // 每条记录的Title，其实是在list下的，Text也是
          if (propertyData.object === &#39;list&#39; &amp;&amp; propertyData.results.length &gt; 0) {
            if (propertyData.results[0].type === &#39;title&#39;) {
              return { [propertyName]: propertyData.results[0].title.plain_text }
            } else if (propertyData.results[0].type === &#39;rich_text&#39;) {
              return {
                [propertyName]: propertyData.results[0].rich_text.plain_text,
              }
            }
            // multi_select不会出现再list下，直接判断type就可以拿到
          } else if (propertyData.type === &#39;multi_select&#39;) {
            return {
              [propertyName]: propertyData.multi_select.map((p) =&gt; {
                return p.name
              }),
            }
            // number同multi_select
          } else if (propertyData.type === &#39;number&#39;) {
            return {
              [propertyName]: propertyData.number,
            }
          }
        }),
      )
      // 由于得到的record是数组，而在kintone中需要用对象来放置数据，所以这里先行做一个转换
      return { ...record }
    }),
  )
  return { records: propertitsSet }
}
const notionDBRecords = await iterateDB()
// Notion属性名和kintone App中字段代码的对应关系
const fieldCodeMap = {
  书名: &#39;book_name&#39;,
  ISBN: &#39;isbn&#39;,
  作者: &#39;author&#39;,
  定价: &#39;price&#39;,
  标签: &#39;label&#39;,
}
// 上传kintone的对象是有一定的格式要求，所以需要把数据加工一下
for (const record of notionDBRecords.records) {
  for (const [key, value] of Object.entries(record)) {
    if (value) {
      record[fieldCodeMap[Object.keys(value)[0]]] = { value: Object.values(value)[0] }
    }
    delete record[key]
  }
}
notionDBRecords.app = 999
// 调用kintone sdk把数据添加到kintone
const client = new KintoneRestAPIClient({
  baseUrl: &#39;https://yourdomain.cybozu.cn&#39;,
  auth: {
    apiToken: &#39;WKuCUxqW8gRYrgs57w5UVAU9GUKYPaTU210MJ0bx&#39;,
  },
})
const kintoneResponse = await client.record.addRecords(notionDBRecords)
// 观察response来判断是否成功
console.log(kintoneResponse)</pre>
<h2>
    代码解说
</h2>
<p>
    整个代码的最粗的逻辑目标，就是从Notion中取出数据，存放到kintone中，这点是显而易见的。但实际观察代码，在获取Notion数据时，有很多遍历嵌套的结构，不免有些让人难以理解。所以在这里有必要做些说明。
</p>
<h3>
    Notion获取database数据问题
</h3>
<p>
    造成遍历嵌套复杂的原因，是由于Notion API的规定所造成的。Notion在2022年6月28日之前的API版本中，支持用page id一次性获取所有属性。虽然很方便，但是由于性能等方面的原因，Notion开发团队在2022年6月28日之后的API版本中规定，获取page的属性，必须先获取属性名，再用page id和属性名去获取属性值。再加上page id需要给出database id后遍历得到，看上去结构就会更加繁琐。
</p>
<p>
    具体信息可参考Notion的<a href="https://developers.notion.com/changelog/releasing-notion-version-2022-06-28">Release note</a>，文中有“why page properties are so complex”这样的词句，可见开发团队本身就意识到了其复杂性会带来困扰。
</p>
<p>
    虽然及其不推荐，但是还是有另一个办法。Notion在发送API时可以指定版本，我们可以发送类似2022-05-18这种之前的版本来规避这种复杂性。
</p>
<h3>
    Notion Page属性数据结构不统一问题
</h3>
<p>
    另一个造成程序复杂的原因是Page属性的object组织结构并不统一，有几个属性（范例中的title和rich_text)并不放在外层，而是嵌套在list中。这就需要分情况判断了。具体信息可参考<a href="https://developers.notion.com/reference/property-item-object">属性对象</a>，在处理数据时，这些情报非常重要。
</p>
<h3>
    范例中的“为了方便”
</h3>
<p>
    范例中的代码，有些地方是为了书写方便或是测试数据本身没有复杂结构等原因，没有很详细的把逻辑全面覆盖。
</p>
<p>
    譬如26行等多出有<span style="color:rgb(84,141,212);">results[0]</span><span style="font-size:16px;">的出现。</span>
</p>
<pre>if (propertyData.results[0].type === &#39;title&#39;) {</pre>
<p>
    其实<span style="color:rgb(84,141,212);">results</span>的数组长度可不一定是1，因为像title这种数据类型可能是由多个富文本块所拼接构成。而每个富文本块还有他自己的一套格式数据。如果读者在实际编写中有需要解析这种数据的，请酌情把数据继续一层层解析下去，范例中就不赘述了。
</p>
<h3>
    机密情报
</h3>
<p>
    范例中的所有关键性隐私信息（secrets，token，appid等）均为假数据，读者测试时请使用自己的真实情报替换之。
</p>
<h2>
    参考链接
</h2>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            <a href="https://cybozudev.kf5.com/hc/kb/article/1307437/" target="_blank" rel="noreferrer noopener">还没有kintone环境的读者可以免费申请</a>
        </p>
    </li>
    <li>
        <p>
            <a href="https://developers.notion.com/" target="_blank" rel="noreferrer noopener">Notion API</a>
        </p>
    </li>
</ul>
<p class="operaCheck">
    此Tips在2022年10月版的 kintone 中确认过。
</p>
<p>
    <br/>
</p>