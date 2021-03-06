# <kbd>VUEJS :tanabata_tree: NOTES</kbd>
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

+ <kbd>dynamic url  :banana:</kbd>	

```
      <ul>
         <li><a v-bind:href="homeURL" target="_blank">home</a></li>
      </ul>

``` 

+ <kbd>inserting a query string :banana:</kbd>	


```
      <ul>
         <li><a v-bind:href="homeURL + '?myParam=1'" target="_blank">home</a></li>
      </ul>
      
``` 

+ <kbd>data-binding w/ vue  :banana:</kbd>	

```
      <form>
           <input type="text" name="name" v-bind:value="name">
      </form>
```

+ <kbd>dom respond to changes in data   :ski:</kbd>
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

   ..and my instance will be an array  :ferris_wheel:
   
  and
   
   lets say I want ***one or more fields selected*** then:  :boom:

  in my array:
 
 

```
    selfields = ['Cycling', 'Swimming'];
```


#### :small_orange_diamond: rendering content in a loop/while toggling their display
(whether pull from database or api and rendered dynamically)

<script type="text/javascript">
  <div id="app">
      <form method="post" action="/">
        <label for="email">Email</label> <input type="email" v-model.lazy="email" id="email">
        <fieldset>
          <legend>Interests</legend>
          <div v-for="interest in interests">
              <input type="checkbox" v-model="selectedInterests" :value="interest"/>{{interest}}
          </div>
        </fieldset>
        <input type="submit" value="Subscribe">
        <!--<p>You entered {{email}}.</p>-->
        
        <p v-show="selectedInterests.length > 0"> 
            
            You selected: {{selectedInterests.join(', ')}}
        
        </p>
      </form>
  </div>
</script>

<script>
  var vm = new Vue({
     el:                      '#app',
     data: {
       email: '',
       interest:              ['Running', 'Cycling', 'Swimming'],
       selectedInterests:     []
     }
  });
</script>





#### :small_orange_diamond: If I want to hide this section til one element is selected:



```
    <p v-show="selectedInterests.length > 0"> 
            
        You selected: {{selectedInterests.join(', ')}}
        
    </p>


```

#### :small_orange_diamond: v-if directive (use when you don't expect that value to change)
it removes the element from the DOM when the expression is false

```
    <p v-if="selectedInterests.length > 0"> 
            
        You selected: {{selectedInterests.join(', ')}}
        
    </p>

    <p v-else>Please select at least one</p>

```
#### :small_orange_diamond: v-else  (can be used for whenever the v-if fails)

#### :small_orange_diamond: v-else-if  (to add an arbitrary number of cases)

```  
    <p v-else-if="selectedInterests.length ==3">Please select at least one</p>

```

#### :small_orange_diamond: this gets id on url


```
    <div v-for="(interest, index) in interests">
        <input type="checkbox" v-model="selectedInterests" :value="interest.id"/>
        {{index}}.{{interest.name}}
    </div>
        
    <p v-show="selectedInterests.length > 0"> 
            
        You selected: {{selectedInterests.join(', ')}}
        
    </p>

```

new instance:   
by adding a second looping variable, and putting them both in parentheses,
we can get access to that index   
index before that name in curly braces adds index: 0,1,2

ex:

```
  0.Running
  1.Cycling
  2.Swimming

```



```
  <script>
        var vm = new Vue({
           el:                      '#app',
           data: {
             email: '',
             interest:  [
                {
                  id: 1,
                  name: 'Running',
                },
                
                {
                  id: 2,
                  name: 'Cycling'
                },

                {
                  id: 3,
                  name: 'Swimming'
                }    


             ],        

             selectedInterests:     []
           }
        });
  </script>


```


### :small_orange_diamond: another way to display every value key pair
(for access to the index, add another parameter after key)
and add {{index+1}} before {{key}}

```
    <div v-for="(value, key) in address">
          {{key}}: {{value}}
    </div>

    selectedInterests = [],
    address: {
        street: '123 Is my house',
        city: 'London',
        postcode: NW123
    }

```

  
## basic binding notes

- v-show for toggling visibility
- v-if when not expecting boolean value to change
- v-else (if v-if exists for when condition fails)
- v-else-if to add an arbitrary number of cases
- v-else and v-else-if dont work with v-show
- single-data-binding added to most static content in page

- v-for loop syntax: -> "item in collection"
- (item,index) to a second looping index, to get access to that index.

- for event handlers: v-on:evt-name    ex: v-on:click="message"


## vue instance
- how to vue manages data pass to constructor and changes that need re-rendering

> when a vue is first initialized, the properties and the data object are added
  to the instance along with special getter and setter methods.
  - getter when invoked returns value and executes
  - setter invoked sets value and re-renders as well


```

Vue instance:

  get firstname() {
   
   /*
    *  Register this property and watch
    *  for changes to react to.
    *  Return the value
    *
    */

  }

  set firstName()

   /*
    *  Update the value.
    *  Re-render any elements that use it. (updating vue's virtual dom
    *  which can be updated much faster. Once updated, it compares the new
    *  virtual dom to the previous version and updates only changes
    */

Constructor Parameter:

{
    data: {

        firstName: ''
    }

}  

```

### computer properties
allow you to setup more sophisticated relationships between data properties

We can declare initial properties and data, and use them in expressions in our
templates, but it's not possible to refer to other data properties from
within this initial data property itself.

ex: to create a full name property out of firstname and lastname

```
    data: {
      fistname: 'Mike',
      lastname: 'Jones',
      fullname: this.firstname + ' ' + this.lastname  

      // wont work cause neither the data object nor the view instance have
      // been created yet and `this` refers to the window global object or
      // undefined in strict mode

    }
```  


```
      //assuming tempF is part of data instance

    computed: {
            console.log('using computed property');  //will show and if log
            tempC: function() {                      // is cached 
                return Math.round(5/9 * (this.tempF - 32));
            }
       }

       //then

       {{tempC}}


```

> note: crazy enough, you can just call it using:

```
      methods: {
            console.log('using method');      //when called
            tempC: function() {
                return Math.round(5/9 * (this.tempF - 32));
            }
       }

       //then

       {{tempC()}}


       // big difference is that with methods is going to get
       // recalculated everytime you call the function

       // but with computed it gets ***cached***
```


## watch

- properties we would like to watch in response to changes.
- asynchronous tasks in response to a property change

> cannot use computed to call an api, it needs to be watch cause some
> value would have to be immediately return and can't wait for api response.


## lifecycle hooks

- a view instance exposes a number of lifecycle hooks that we can use in order
  to execute custom code in response to certain events during initialization,
  updates and destruction.

- beforeCreate hook is triggered before the instance is initalized and any
  data is processed

- created hook is called after the properties are configured, but before the
  instance has been mounted to the DOM

- beforeMount hook is called when the template is compiled and ready to be
  inserted to the DOM

- Mounted hook is called when the template is inserted into the DOM as
  a replacement for the element.

- beforeUpdate hook triggered whenever data changes

- Updated hook runs after re-rendering to reflect the changes

- beforeDestroy and Destroyed events are raised whenever vm.$destroy is called


> to destroy an instance =>. vm$destroy();


## Vue components
- they provide a way to encapsulate data and behavior making them easily
  reusable

- to add a custom component to a page -> do this by adding an element to our
  template with a custom tag name that we register and define

- a component can be global - avail for any vue instance - or local
ex
    <global-component></global-component>

    // we can have vue replace this tag at runtime with any markup we choose
    // but one important rule is that the markup that replaces it must have
    // a single root element that wraps all other elements


> Register a global component by calling Vue.component and
> passing the custom tag, followed by an Options object and
> before the call to new Vue so it doesn't mount the instance

ex.
registered a component with an option object with template as property

    Vue.component('global-component', {template:'<div></div>'})


- Components are very useful for working with data, but they can't    

- the data property in a component is going to have a function assigned to it.

- components are very similar to vue instances and can use all the same life
  cycle hooks. They can also have methods

## components properties made more powerful
by allowing the parent view instance to provide initial properties to
each component instance.


## to add additional content to a component
 
ex (adding child elements between the components starting and ending tags)

    done by using slot tags
        ex:
            <slot name="top">this will be default content</slot>

        Also we can add default content to a slot by including it between the slot
        tags (in Vue.component, assuming there's no content btw tags)    

        <p slot="top">Everything on sale</p> //will only appears if 'this will..' not there



Vue 2.1 => theres a new slot called 'scoped slot'
it allows slot content to be specified as a template that can receive it own props
from the parent template.

  ex. here slot uses template tags in html (this here is a little confusing atm)

```
    <product-list-flexible :products="theProducts" the-title="Custom layout">
       <template scope="props">{{props.product.name}}</template> 
    </product-list-flexible>

    //Vue.component then uses regular <slot></slot> tags with whatever binding prop
    here be => :product="product"  (in products)

    * if you got more than one slot then you'll have to name them.
```

## using webpack module bundler
> vue-cli to configure webpack

- separating components into individual files and processing them
- some advantages to using single-file components instead of just declaring them
  in javascript along:
    - syntax highlighting - using js strings to define templates can be a bit hard to read
    - single-file components have the same color coding and auto-completion as html
    - use new javascript features es6 or es5 including modules to avoid scope issues and
      without worrying about browser compatibility
    - component specific styling for css
    - hot module replacement w/webpack - which will recompile components when we make a change
      to the code and update the page automatically without refresh


- @vue spa initial setup at last :boom:
  + it requires vue-cli installed global
  + npm runs dependencies
  + vue init puts together, and run local server env
  + and u can even do npm run build when ur done









