###Forms

status.value要有初始值，否则在input上用会报错。

textarea，select增加了value属性。

```
this.setState({
  [name]: value
});
```
等于ES5中的
```
var partialState = {};
partialState[name] = value;
this.setState(partialState);
```
	

React 中 composition、props可以让你方便、灵活地定制组件，不需要使用继承。


single responsibility principle


React提供了特殊的属性ref，用来绑定任意组件，ref携带一个回调函数，函数会在组件装载或卸载时立即执行。


列表循环输出，肥肠好用
```
 return (
    <ul>
      {todos.map((message) => <Item key={message} message={message} />)}
    </ul>
  );
```


0在JSX中会被当成true
```
<div>
  {props.messages.length > 0 &&
    <MessageList messages={props.messages} />
  }
</div>
```



 <input type="checkbox"> and <input type="radio"> support defaultChecked, and <select> supports defaultValue.


尽量先不要用Context api



When you want to aggregate data from multiple children or to have two child components communicate with each other, move the state upwards so that it lives in the parent component. The parent can then pass the state back down to the children via props, so that the child components are always in sync with each other and with the parent.

