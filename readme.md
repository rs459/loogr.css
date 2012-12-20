# LoopOfGridObject

- use object with placeholder

1. You create your own mediaqueries
2. You add a namespace for each mediaqueries
3. You insert all object inside these mediaqueries ```@include loopOfGridObject($namespace);```
4. Style your website and use @extend with placeholder each of them have a namespace ```.selector {@extend %no-mg-left--mynamespaceformymediaqueries;}```
