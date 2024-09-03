# jsx rules
- Return a single root element 
- If you don’t want to add an extra <div> to your markup, you can write <> and </> instead 
- This empty tag is called a `Fragment`. Fragments let you group things without leaving any trace in the browser HTML tree.

reason JSX looks like HTML, but under the hood it is transformed into plain JavaScript objects. You can’t return two objects from a function without wrapping them into an array. This explains why you also can’t return two JSX tags without wrapping them into another tag or a Fragment.

- Close all the tags (like img li ... can work without closing in html but not in jsx)
- most of the things are camel case now

# JavaScript in JSX with Curly Braces
- As text directly inside a JSX tag: \<h1>{name}'s To Do List\</h1> works, but <{tag}>Gregorio Y. Zara's To Do List</{tag}> will not.
- As attributes immediately following the = sign: src={avatar} will read the avatar variable, but src="{avatar}" will pass the string "{avatar}".
- React does not require you to use `inline styles` (CSS classes work great for most cases). But when you need an inline style, you pass an `object` to the `style attribute`

# conditional rendering
- (?:) && ?? || if(){}else{} can be used for conditional rendering
```jsx
function Item({ name, isPacked }) {
  let itemContent = name;
  if (isPacked) {
    itemContent = name + " ✅";
  }
  return (
    <li className="item">
      {itemContent}
    </li>
  );
}
```

```jsx
function Item({ name, isPacked }) {
  let itemContent = name;
  if (isPacked) {
    itemContent = (
      <del>
        {name + " ✅"}
      </del>
    );
  }
  return (
    <li className="item">
      {itemContent}
    </li>
  );
}
```

# \<Fragment> (<></>)
- does not add overhead 
- agar typescript me banate hain react wala to bas element hi return kar sakte hain nahi to typescript error show karne lgta hai but in js normal array bhi return kar sakte hain