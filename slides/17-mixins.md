#Mixins, Sugar

```
function enforceDependencies(klass, options, deps){
  deps = _.filter(deps, function(depName){
    if( !options[depName] ){
      throw new Error('Missing required dependency: '+ depName);
    }

    return !!klass[depName];
  });
  _.extend(klass, _.pick(options, deps));
}
```
```
Backbone.View.extend({
  initialize: function(options){
    enforceDependencies(this, options, ['model', 'app']);
  }
});
```
