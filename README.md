plastik-lazy-route-selector
============

`plastik-lazy-route-selector` lazy-loads pages based on routes selected using
the [`more-routing`](https://github.com/PolymerLabs/more-routing) element.

Demos and documentation are available on the
[component page](http://www.plastikit.org/1.x/#!/components/plastik-lazy-route-selector).

Pull requests are always welcome. If you encounter any bugs, please feel free to
[submit an issue](https://github.com/Plastikit/plastik-lazy-route-selector/issues/new/).

## Installation

```sh
bower install Plastikit/plastik-lazy-route-selector --save
```

## Basic usage

> _See [component page](http://www.plastikit.org/1.x/#!/components/plastik-lazy-route-selector)
> for more details._

`plastik-lazy-route-selector` can load both custom elements and templates.

By default, `plastik-lazy-route-selector` will attempt to load a custom element
that has the same name as the import's filename. For example, if the lazy loader sees
`/pages/some-page.html`, it will assume that the custom element name is `some-page`.

This behaviour can be overridden by setting an `element` attribute on the children of
the page selector nested in `plastik-lazy-route-selector`. Whatever name is given
in the `element` attribute will determine the name of the custom element that
`plastik-lazy-route-selector` tries to instantiate.

If a template is desired to be loaded instead of a custom element, add a `template`
attribute to the page placeholders. If there are multiple templates in the file provided
in the `import` attribute, then the `template` attribute can be set to the ID of the desired
template.

## Integrating into an application

The following is a simple example of how `plastik-lazy-route-selector` can be
used in an application.

### Example

```html
<more-route-config driver="path"></more-route-config>

<more-route name="home" path="/">
  <more-route name="users" path="/users">
    <more-route name="user" path="/:userId"></more-route>
  </more-route>
  <more-route name="help" path="/help"></more-route>
</more-route>

<paper-drawer-panel>

 <paper-header-panel drawer>

   <paper-toolbar>
     <div>My App</div>
   </paper-toolbar>

   <paper-menu attr-for-selected="route" selected="{{route}}">
     <paper-item route="home">Home</paper-item>
     <paper-item route="users">Users</paper-item>
     <paper-item route="help">Help</paper-item>
   </paper-menu>

 </paper-header-panel>

 <plastik-lazy-route-selector main selected="{{route}}">
   <iron-pages attr-for-selected="route">
     <div route="home" import="/pages/myapp-home.html"></div>
     <div route="users" element="myapp-users-page" import="/pages/users.html"></div>
     <div route="help" import="/pages/myapp-help.html"></div>
   </iron-pages>
 </plastik-lazy-route-selector>

</paper-drawer-panel>
```

## Using with neon-animated-pages

`plastik-lazy-route-selector` will automatically detect if the selector element provided to
it inherits from `NeonAnimationRunnerBehavior`. If it does, it will wait for the
`neon-animation-finish` event before it removes the lazy-loaded content from the page. No manual
configuration is necessary.


### Example

```html
<plastik-lazy-route-selector main selected="{{route}}">
 <neon-animated-pages attr-for-selected="route"
   entry-animation="fade-in-animation" exit-animation="fade-out-animation">
   <neon-animatable route="home" import="/pages/myapp-home.html"></neon-animatable>
   <neon-animatable route="users" import="/pages/myapp-users.html"></neon-animatable>
   <neon-animatable route="help" import="/pages/myapp-help.html"></neon-animatable>
 </neon-animated-pages>
</plastik-lazy-route-selector>
```
