<h2>
    前言〜库的昨夜和今天〜
</h2>
<p>
    前端的世界日新月异，新技术层出不穷，令人难以追逐。但就最近一段时间而言，相对还算稳定。<br>
    就拿 JavaScript 的框架来说，经过了一时的逐鹿中原、盛衰荣辱，React 和 Vue.js 的两大主流地位基本确立了下来。<br>
    如果说轻量级 JavaScript 自定义开发不导入框架也能信手拈来的话，<br>
    一旦规模达到一定程度，借助框架的力量来提升开发效率就显得必不可少了。
</p>
<p>
    现在我们来演示导入 React 的过程，其中如果有合适的经验或窍门正好能用在您的项目中，我们将感到十分荣幸。
</p>
<h2>
    React 是什么、React 的特征
</h2>
<p>
    React 是 Facebook 和 React社区为构筑用户界面而开发的 JavaScript 库。
</p>
<p>
    现在解说一下<a href="https://ja.reactjs.org/">React 的官方网站</a>上所记载的三个特征。
</p>
<h3>
    声明式
</h3>
<p>
    &nbsp;「声明式」所说的是条件或者动作所明确表示的状态。<br>例如 jQuery 是「命令式」的，如果是 DOM 操作的话，就取得元素后对它进行命令的堆叠。<br>代码中有很多地方都对某个元素进行命令的话，各种复杂的条件交织在一起时，便成了 bug 的温床。
</p>
<p>
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
<p>
    只有很少的代码，可能怎么写区别都不大，拿 jQuery 来说，可以从任何地方追加事件的句柄。<br>还有“这个元素现在是什么颜色？”类似这种状态也要用代码管理起来的话，<br>渐渐的越来越复杂，到最后难以维系正常的动作。<br>React 则会把 DOM 和状态分开管理，状态一目了然。
</p>
<h3>
    基于组件
</h3>
<p>
    在 React 中，组件自身能管理状态，并用搭建胶囊化的组件的方式，来构筑复杂的用户界面。
</p>
<p>
    组件的逻辑是，不用 Template 而是直接可以写 JavaScript 代码，以便在程序中简单地获取各种各样的数据<br>并且可以让 DOM 不带自身的状态。
</p>
<p>
    在上述的代码范例中，“是红还是绿”，这个情报保存在 color 变量中，不需要在意 DOM 的状态。<br>。
</p>
<h3>
    一次学习，处处使用
</h3>
<p>
   React 可以和其他技术并存而不产生冲突。<br>使用 React 追加新功能时也不必更换既有代码。
</p>
<p>
    React 在自建服务器或租赁服务器上都可运作，React Native则可以使你的程序运行在手机上，所以一旦掌握了可以在各处使用。
</p>
<h2>
    React 引入时的注意点
</h2>
<p>
    React 有以下优缺点，在引入的时候，最好综合考虑各方面因素再加以判断。
</p>
<h3>
    优点
</h3>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            &nbsp;和jQuery或纯 JavaScript 相比较，最大的强项是可以写声明式。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p>
                定义好的组件，其状态如果发生改变（按上述的范例代码来举例的话，就是用 useState 来声明的变量 color ），则代码各处都会得到一遍执行。<br>这样，发生了一些什么事都会很明确。例如 jQuery或纯 JavaScript 的话，<br>对于 DOM 发起的命令的源头和内容就不能把握，复杂性逐渐增加，最后达到难以控制的程度。
            </p>
        </li>
        <li>
            <p>
                处理数量众多的元素，例如“列表的自定义视图”，或“自创的按钮”等非常高效。
            </p>
        </li>
    </ul>
    <li>
        <p>
            暗箱操作的部分较少。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p>
                和其他的框架例如 Vue.js 等比较的话、React 所规定的特殊规则较少（例如 Vue.js 中的 v-model 等语法）、比较容易明白正在执行些什么事情。<br>正如范例代码所写的那样，事件句柄的值会怎么变化都在掌握之中，有点像在写纯 JavaScript 的那种感觉，什么都可以自己掌控。
            </p>
        </li>
    </ul>
    <li>
        <p>
            React 在 JavaScript 框架中是非常有人气的，学习起来比较容易，而且公开了非常多好用的组件。<br>就像上面所说的，可以在各种场合使用。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p>
                虽然制作的方式各有不同，kintone JavaScript 自定义所制作的组件，可以原封不动地用在手机上。
            </p>
        </li>
    </ul>
    <li>
        <p>
            可以部分导入。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p>
                一部分的 JavaScript 自定义是用纯 JavaScript 编写、复杂的地方采用 React 来写，这种方案也是可行的。
            </p>
        </li>
    </ul>
    <li>
        <p>
            UI 和逻辑是分离的，适合大规模的项目。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p>
                特别是各种应用都会使用 REST API来取得数据并加工。这种逻辑部分和 UI 是分开的，显得很清晰。
            </p>
        </li>
    </ul>
</ul>
<h3>
    缺点
</h3>
<ul class=" list-paddingleft-2">
    <li>
        <p>
            因为是声明式的，记述的代码量会有增加的趋势。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p>
                然而对于一直维护的 kintone 环境来说，反而式比较适合的。
            </p>
        </li>
    </ul>
    <li>
        <p>
           要运用到记忆化等技术进行性能提升时，根据情况不同多少有点难度。
        </p>
    </li>
    <li>
        <p>
            寥寥数行代码就能解决的事情，用纯 JavaScript 就已经足够了。
        </p>
    </li>
    <ul class=" list-paddingleft-2" style="list-style-type: square;">
        <li>
            <p>
                根据实际情况，如果只是文本变色等简单逻辑，没有必要刻意导入。
            </p>
        </li>
    </ul>
</ul>
<h2>
    用 React 实现自定义视图
</h2>
<p>
    这次，我们将利用顾客列表中制作自定义视图作为范例代码。
</p>
<p>
    自定义完成后，将达到这样一个效果：
</p>
<p>
    显示公司名列表，并且可以选择。
</p>
<p>
    按下按钮后，显示现在选中的公司名。
</p>
图片插入点1
<h3>
    事前准备
</h3>
<p>
    1. 添加顾客列表应用<br>
    新增一个应用，选择默认安装好的模板“顾客列表”。<br>
    创建成功后，初始还没有数据，我们可以自行添加一些测试数据。
</p>
<p>
    1. 设置自定义视图，指定 HTML 代码。
</p>
```html
<div id="target"></div>
```

<p>
3. 为了配合后面克隆项目中的配置，我们把公司名的字段代码从“单行文本框”改为“会社名”
</p>
图片插入点2
<p>
    4. 从 Github上克隆代码。
</p>
<p>
    <a href="https://github.com/cybozudevnet/sample-kintone-webpack-for-intermediate">https://github.com/cybozudevnet/sample-kintone-webpack-for-intermediate</a>
</p>
<p>
    详情请参照<a href="https://cybozudev.kf5.com/hc/kb/article/1412604">第1篇</a>中的内容。
</p>
<p>
    &nbsp; 这次将按 React 的要求来设置。
</p>
<h3>
    范例代码
</h3>
<p>
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
    <br>
</p>
<h3>
    代码的概要说明
</h3>
<p>
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

<p>
    这里，把多选框定义为一个组件。
</p>
<p>
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

<p>
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

<p>
    另外，第7行使用了 State （状态）保存了已选中的ID，使用 useState 可以保持住状态。
</p>

```javascript
const [selectedIds, setSelectedIds] = useState<string[]>([]);
```

<p>
    这里面 selectedIds 是存放已选的ID，setSelectedIds设置这次所选ID。
</p>
<p>
    像这样，通过定义元素、定义事件的句柄等可以完整地申明一个组件。<br>相较于jQuery这种是用 class 来表示状态，React把 UI 和状态分开存放的特点是一大优势。
</p>
<p>
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

<p>
    在1中定义的组件，可以用 ReactDOM.render() 这个方法来显示
</p>

```javascript
ReactDOM.render(<ChecklistComponent records={records} />, targetEl);
```

<p>
    这次主要想显示列表事件，所以就在列表的事件内逐一定义了。
</p>
<p>
    把 event 对象内的记录列表传给了组件。
</p>
<p>
    像这次这样，申明一些通用的组件，在 kintone 的事件句柄中自由组合这些组件，就可以以一个极小的代码量来完成这些需求。
</p>
<h2>
    结束语
</h2>
<p>
    JavaScript 的自定义中，可以用本篇中所介绍的 React，也可以用 Vue 等其他的框架，也可以写纯 JavaScript。方法是多种多样的。
</p>
<p>
    根据自己项目的特点，选择合适的技术，可以使 JavaScript 的自定义工作更加柔顺。<br>特别是有持续维护可能性的项目，非常推荐您使用本篇中所介绍的像 React 那样有大项目耐受性的框架。
</p>
<p>
    该Tips在 kintone 2021年9月版中进行过确认。
</p>