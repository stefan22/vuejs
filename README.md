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

#### changing delimiters. :checkered_flag:

  ex.
  
```
      new Vue({
         delimiters: ['${','}']
      })

      //delimiters changed to ES6 template string style
```

> Pages are process top to bottom, so whatever's being mounted needs to come first.



## data binding  :violin:

##### <kbd>dynamic url  :banana:</kbd>	

```
      <ul>
         <li><a v-bind:href="homeURL" target="_blank">home</a></li>
      </ul>

``` 

##### <kbd>inserting a query string :banana:</kbd>	


```
      <ul>
         <li><a v-bind:href="homeURL + '?myParam=1'" target="_blank">home</a></li>
      </ul>
      
``` 

##### <kbd>data-binding w/ vue  :banana:</kbd>	

```
      <form>
           <input type="text" name="name" v-bind:value="name">
      </form>
```

 <kbd>dom respond to changes in data   :ski:</kbd>
```
      <form>
          <input type="text" name="name" :value="name">
      </form>

      //shorthand version
      data access is through vm.name not vm.data
      
```

## 2-way data binding (UI - Model)  :doughnut:

```
ex:
   instead of using: =>  v-bind:value="name"

                     =>  v-model="name"
```



- you can add ***modifiers*** into two-way data binding that act like ***onfocus*** and
  ***onblur*** events in js (too much data binding could get annoying)

```
  ex:
         v-model:value="email"         //this worked for me as well

         v-model="email"               //this supposedly right way

         v-model.lazy="email"          //adding lazy holds on till the onblur
                                       //event happens before it updates model
```



<kbd>ex: checkboxes :doughnut:</kbd>

   ***assuming something like this:***

``` 
   <input type="checkbox" v-model="selfields" value="Cycling">
   <input type="checkbox" v-model="selfields" value="Swimming">
```
    <p>You've selected: {{selfields.join(', ')}}</p>

    ..and my instance will be an array
   
   and
   
   lets say I want ***one or more fields selected*** then:

    in my array:
 
 

```
      selfields = ['Cycling', 'Swimming'];
```










