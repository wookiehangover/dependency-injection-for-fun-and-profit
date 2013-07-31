### I promise, it's a simple pattern

```
var PlaylistView = Backbone.View.extend({
  initialize: function(options){
    if( !this.collection ){
      throw new Error('PlaylistView requires a collection property');
    }

    this.listenTo(this.collection, 'add', this.renderItem);
  },
  ...
});

$(function(){
  window.app = new PlaylistView({
    collection: new Backbone.Collection()
  });
});
```

<aside class="notes">
  <p>Pass dependencies as options to constructors</p>
  <p>throw errors when your deps not met</p>
</aside>
