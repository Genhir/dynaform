# Dynaform

Dynaform is JQuery plugin that allows you to build and edit web forms in your browser.

## Installation

Make sure JQuery along with the following Javascript files have been loaded in your html header:

* dynaform.jquery.js
* example_type.dynaform.jquery.js etc...

Current types include:

* textbox.dynaform.jquery.js
* textarea.dynaform.jquery.js
* tickbox.dynaform.jquery.js
* email.dynaform.jquery.js

## How to use

Once the above installation is complete Dynaform is really easy to use - simply add a "dynaform" class attribute to any form input element e.g:

> &lt;input name="form_schema" type="hidden" class="dynaform" /&gt;

## API

### The "Dynaform" object

The Dynaform API is exposed through the "Dynamform" object, which has two methods:

* addType(DynaformType type)
* type(String name)

#### Dynamform.addType(DynaformType type)

This method allows you to define your own types. For more information on creating custom types please see the "Creating Custom Types" section (below).

#### Dynamform.type(String name)

The method allows you get any type that has already been added by name e.g.:

> var textbox_type =  Dynamform.type("textbox");

You could now (if you wanted to) modify this type with a custom preview:

``` 
textbox_type.htmlPreview = function(){ 
  return "My custom preview!!!";
};
```

### Creating Custom Types

Creating custom types is a three step process:

1. Create an instance of the DynamformType class.
2. Customise the DynamformType instance by overriding special methods.
3. Add the DynamformType instance to the Dynamaform object.

A minimal custom type created as by doing the following:

```
(function(){
  
  //create instance
  var foo_type = new DynamformType();
  
  //customise
  foo_type.name = function(){ 
    return "foo";
  };
  
  foo_type.htmlPreview = function(){ 
    return "This is what foo will look like.";
  };
  
  //add type to Dynamform object
  
  Dynamform.addType(foo_type);
  
})();
```

Here is a more advanced example where we'll create a custom editor:

```
(function(){
  
  //create instance
  var bar_type = new DynamformType();
  
  //customise
  bar_type.name = function(){ 
    return "bar";
  };
  
  bar_type.htmlPreview = function(){ 
    return "This is what bar will look like.";
  };
  
  //lets define the initial model for this input
  bar_type.model = function(){ 
    return {label: "", favourite_color: "red"};
  };
  
  bar_type.edit = function(state){
    state.label = prompt("Please enter label:", state.label);
    state.favourite_color = prompt("What is your favourite color:", state.favourite_color);
    state.save();
  };
  
  //add type to Dynamform object
  
  Dynamform.addType(foo_type);
  
})();
```

Of course in the above above we could have used an Ajax dialog.
