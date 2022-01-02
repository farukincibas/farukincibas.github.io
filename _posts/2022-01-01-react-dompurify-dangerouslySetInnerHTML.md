---
title: "Post:  React using dangerouslySetInnerHTML with dompurify "
date: 2021-09-30T15:34:30-04:00
categories:
  - react
tags:
  - react
  - dompurify
---



When to use dangerouslySetInnerHTML?
---

if you take html data from rich text editor or it is coming from another application that html and you want to use your app like 3d secure form

Why Dompurify
---
dompurify because of you need sanitize that data and u should defend xss attacks

How to install dompurify?
---
```ruby
npm i dompurify
#=> install purify first
```

Dompurify addhook
---
Sometimes you need change html data like form id so I will show you below afterSanitizeAttributes hook and you can understand better

Example With React
---

```ruby
import DOMPurify from 'dompurify'
import './App.css';

function App() {
  const postHtml = `
  <!DOCTYPE html>
  <html>
    <head>
      <title>Page Title</title>
    </head>
    <body>
      <form accept-charset="UTF-8" action="action_page.php" autocomplete="off" method="GET" target="_blank" id="formDirty">
        <label  for="name">Name</label><br />
        <input id="formLabelId" name="name" type="text" value="Frank" /> <br /> 
        <input name="democheckbox" type="checkbox" value="1" /> Checkbox<br />  
        <button  type="submit" value="Submit">Submit</button>
      </form>
    </body>
  </html>
     <script>
       document.getElementById('formLabelId').value='Faruk';
       document.getElementById('formDirty').submit();
     </script>
`;

  function sanitizedData() {
    DOMPurify.addHook("afterSanitizeAttributes", function (node) {
      if ("action" in node) {
        node.setAttribute("id", "form-purify");
      }
    });
    console.log(DOMPurify.sanitize(postHtml));
    return {
      __html: DOMPurify.sanitize(postHtml)
    };
  }



  return (
    <>
      <div
        dangerouslySetInnerHTML={sanitizedData()}
      />
    </>
  );
}

export default App;
#=> I explained here with form data
```

console.log sanitized data result below
---

```ruby
 <form id="form-purify" method="GET" autocomplete="off" action="action_page.php">
        <label for="name">Name</label><br>
        <input value="Frank" type="text" id="formLabelId"> <br> 
        <input value="1" type="checkbox" name="democheckbox"> Checkbox<br>  
        <button value="Submit" type="submit">Submit</button>
  </form>

      #=> Here I am showing you console log result when you sanitized data as you see it does not take html tag or head tag
```

Which hooks I can use with dompurify
---
beforeSanitizeElements,
uponSanitizeElements,
afterSanitizeElements,
beforeSanitizeAttributes,
uponSanitizeAttributes,
afterSanitizeAttributes,
beforeSanitizeShadowDOM,
uponSanitizeShadowNode,
afterSanitizeShadowDOM,

Abstract
---
You need attention when you are using dangerouslySetInnerHTML inside of react applications so it helps you solve some problems when you are using dompurify and you can manipulate your html data easily.