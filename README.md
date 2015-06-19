plastik-lazy-loader
============

`plastik-lazy-loader` lazy-loads pages based on routes selected using
the [`more-routing`](https://github.com/PolymerLabs/more-routing) element.

Demos and documentation are available on the
[component page](https://www.plastikit.org/1.x/components/plastik-lazy-loader/).

Pull requests are always welcome. If you encounter any bugs, please feel free to
[submit an issue](https://github.com/Plastikit/plastik-lazy-loader/issues/new/).

## Installation

```sh
bower install Plastikit/plastik-lazy-loader --save
```

## Basic usage

> _See [component page](https://www.plastikit.org/1.x/components/plastik-lazy-loader/)
> for more details._

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

 <plastik-lazy-loader main selected="{{route}}">
   <iron-pages attr-for-selected="route">
     <div route="home" import="/pages/myapp-home.html"></div>
     <div route="users" element="myapp-users-page" import="/pages/users.html"></div>
     <div route="help" import="/pages/myapp-help.html"></div>
   </iron-pages>
 </plastik-lazy-loader>

</paper-drawer-panel>
```

## Using with neon-animated-pages

`plastik-lazy-loader` will automatically detect if the selector element provided to
it inherits from `NeonAnimationRunnerBehavior`. If it does, it will wait for the
`neon-animation-finish` event before it removes the lazy-loaded content from the page. No manual
configuration is necessary.


### Example

```html
<plastik-lazy-loader main selected="{{route}}">
 <neon-animated-pages attr-for-selected="route"
   entry-animation="fade-in-animation" exit-animation="fade-out-animation">
   <neon-animatable route="home" import="/pages/myapp-home.html"></neon-animatable>
   <neon-animatable route="users" import="/pages/myapp-users.html"></neon-animatable>
   <neon-animatable route="help" import="/pages/myapp-help.html"></neon-animatable>
 </neon-animated-pages>
</plastik-lazy-loader>
```
