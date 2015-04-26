# view

> A powerful templating component

>**Dependencies:** `mustache`

>**Author**: [Eduardo Ottaviani](//github.com/Javiani)

---

View can be used with external templates or use the html as a template.

- `data-template` : Specifies if controller will handle templating or not and what template to use.
- `data-render` : Will automatically render the template using global Jails `data` on page load.

## Markup

```html
<div data-component="view" data-render="true" data-template="user"></div>

<script type="x-tmpl-mustache" id="tpl-user">
    {{#user}}
        My name is {{name}}
    {{/user}}
</script>
```

The `data-template` refers to tpl-`user`.

But, you can also use the original html as your template system.
**Jails** provide some html data properties:
`if`, `not`, `each`, `value`, `out`, `attr`.


```html

<div data-component="view" data-template>

    <p data-if="name">My name is {{name}}</p> or
    <p data-if="name">My name is <span data-value="name"></span></p> or

    {{#name}}<p>My name is {{name}}</p>{{/name}}

    <ul data-each="users">
        <li>
            <p data-value="name" />
            <img data-attr="src={{avatar}} alt={{name}}" />
        </li>
    </ul>

    <p data-out="{{count}} != 1? 'Many users!':'Just one user'"></p>

</div>

```

## Annotations

```html
<!-- @view({ render :Boolean, template :String }) -->
<div data-component="view" />
```

## .render
    .render( data, [template]);

`data` can be either a `Object` or a `Promise`.

View will render the html mixing the data object with a specified template. If template is not specified, html will be rendered using `data-template` value.

The following examples do the same thing:

```html
<div data-component="view" data-template />
```

```js
jails.controller('my-controller', function(){

    var view = this.x('[data-component=view]');

    this.init = function(){
        view('render', { name:'Eduardo' }, 'user');
    };
});
```

> or


```html
<div data-component="view" data-template="user" />
```

```js
jails.controller('my-controller', function(){

    var view = this.x('[data-component=view]');

    this.init = function(){
        view('render', { name:'Eduardo' });
    };
});
```

## .partial
    .partial( element, template, data );

Does the same thing as `.render()` but you can specify a html element target to render instead of the current `view`.


## .template
    .template( object, template );

If, for some reason, you need just the string result of the template, you can use this method.
Jails saves all the mustache template embeded on html on `jails.templates` property.
