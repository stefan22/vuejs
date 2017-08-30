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

### data binding

#### dynamic url

```
      <ul>
         <li><a v-bind:href="homeURL" target="_blank">home</a></li>
      </ul>

      

``` 

#### inserting a query string


```
      <ul>
         <li><a v-bind:href="homeURL + '?myParam=1'" target="_blank">home</a></li>
      </ul>
      
``` 

#### data-binding w/ vue
dom respond to changes in data.
```
          <form>
            <input type="text" name="name" v-bind:value="name">
         </form>
```

```
          <form>
            <input type="text" name="name" :value="name">
         </form>

         //shorthand version
         data access is through vm.name not vm.data
```












