"Globals go against the grain of modularity" - Dave Herman

## ¡Warning!

There's more than one way to do it.


## Application View

```
var ApplicationView = Backbone.View.extend({
  initialize: function(){
    this.playlist = new PlaylistModel();

    var injector = {
      app: this,
      model: this.playlist
    };

    this.list = new ListView(injector);
    this.player = new PlayerView(injector);
    this.controls = new ControlsView(injector);
  }
});

$(function(){
  window.app = new ApplicationView();
});
```

## Views tend to have the most dependencies

## If you're depending on another class, make it explicit that you're doing so

## Dependency Injection + Events = Happy Fun Times

* creates a contract of what to expect
* keeps coupling to a minimum
* events are easy to mock in your test suite

```
var PlaylistView = Backbone.View.extend({
  initialize: function(){
    if( !this.model ){
      throw new Error('Requires a model instance');
    }

    this.listenTo(this.model, 'change', this.redner);
  };
});
```

```
describe('PlaylistView', function(){
  describe('initialize', function(){
    it('should attach an event listener', function(){
      var stub = sinon.stub(PlaylistView.prototype, 'listenTo');
      var view = new PlaylistView({
        model: new Backbone.Model
      });

      assert.ok(stub.called);
      assert.ok(stub.calledWith(view.model, 'change', view.render));
    });
  });

  describe('render', function(){
    it('should be called on model change events', function(){
      var spy = sinon.spy(PlaylistView.prototype, 'render');
      var view = new PlaylistView({
        model: new Backbone.Model
      });

      view.model.set({ foo: 'bar' });
      assert.ok(spy.called);
    });
  });
});
```
