# vuejs. :tanabata_tree:
:statue_of_liberty:vuejs.org

- js framework that offers a progressive approach to solving front-end problems.
- a sensible alternative to angularjs and react
- like react uses a virtual dom to manage html
- like angular it has data-binding
- code and templates are completely unobstrusive
- no need to setup a toolchain that composes assets or transpiles modern versions of 
  javascript (angular) 
- when need to build more robust/advanced UIs and SPAs, it has plugins for routing,
  state management and a powerful CLI that works with module bundlers like webpack.

  ### changing delimiters. :checkered_flag:

  ex.
``` 
      new Vue({
         delimiters: ['${','}']
      })

      //delimiters changed to ES6 template string style
```

> Pages are process top to bottom, so whatever's being mounted needs to come first.
