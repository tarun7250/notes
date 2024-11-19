# useTranslation hook
```jsx
const { __testT } = useTestTranslation();
return <div>{__testT('Hello World')}</div>
```

# withTranslation HOC
- for class based components
```jsx
class MyComponent extends Component {
  render(){
    return <div>{this.props.__testT('Hello World')}</div>
  }
};
export withTestTranslation(MyComponent);
```

# trans component
- trans component should be used rather than `__T` on different components
```js
<TestTrans>
    Hello <strong>Arthur</strong>, you have 42 unread messages.
</TestTrans>
```


```js
__testT('Hello')
    <strong>__testT('Arthur')</strong>
__testT(', you have 42 unread messages.')
```

```js
//wrong way
{
   "Video call {{status}}" : "वीडियो कॉल में {{status}} है"
   "Started": "शुरू कर दिया"
}

//right way
{
   "Video call has started" : "वीडियो कॉल शुरू हो गई है"
   "Video call has ended" : "वीडियो कॉल समाप्त हो गई है"
}
```

# Use meaningful interpolation variable names
```js
//wrong
const greeting = __T('Hello {{label}}', { label: user.name })
//right
const greeting = __T('Hello {{name}}', { name: user.name })

//wrong
const groupLabel =__T('{{label}} Custom Property', { label }) 
//right
const groupLabel =__T('{{entityName}} Custom Property', { entityName })

```