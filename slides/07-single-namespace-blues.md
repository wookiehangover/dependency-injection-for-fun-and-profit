## Single Namespace Blues

```
window.App = {
  Models: {
    ...
  },
  Controllers: {
    ...
  },
  Views: {
    ...
  }
}
```

```
window.App = window.App || {};
window.App.Models = window.App.Models || {};

window.App.Models.PlaylistItem = Backbone.Model.extend({
  initialize: function(){
    this.someDependency = window.App.someDependency; // woof
  }
});
```

```
$(function(){
  window.App.router = new window.App.Router();
  Backbone.History.start();
});
```
