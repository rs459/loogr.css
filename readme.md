# LoopOfGridObject

----------

Oocss is great but :

- You have to add one or many class on html node's, without any semantic role.

- You have to override your non-semantic class inside each mediaqueries. (.clearfix, .float)
	
...


LoopOfGridObject :

pro :

- Take full advantage of new feature inside SASS 3.2.x with placeholder capability.
- Your html or yout template stay clear. (you can reuse it, project after project).
- Your add role class or identity class on your html (no non-semantic class like .bordered .float .clearfix).
- You can mix it with Oocss approach.

...

cons : 

- Your selector will be appear, in many place inside your stylesheet.
- Not really for small project.

...

------------

#### You create your own mediaqueries.

```scss
//#style.scss
	@media screen and (max-width: 480px) {

	}
```

#### You add a namespace for each mediaqueries.

```scss
//#style.scss
	@media screen and (max-width: 480px) {
		$namespace : "under480";  
	}

	@media screen and (min-width: 481px) and (max-width: 768px) {
		$namespace : "min480-max768";
	}
```

#### You insert all object inside these mediaqueries and one outside mediaqueries with "all" as argument.

```scss
//#style.scss

	@include loopOfGridObject(all);

	// Your css here 
	....

	@media screen and (max-width: 480px) {
		$namespace : "under480";

		@include loopOfGridObject($namespace);
	}

	@media screen and (min-width: 481px) and (max-width: 768px) {
		$namespace : "min480-max768";

		@include loopOfGridObject($namespace);
	}
```

#### Style your website and use @extend with placeholder each of them have a namespace.

```scss
//#style.scss

	/* Your css here */

	.selector {
		color : white; // You should create this inside the loopOfGridObject mixin.
		@extend %no-pd--all;
		@extend %no-mg-left--under480;
		@extend %no-mg-right--min480-max768;
	}
	.selector-two {
		@extend %no-pd--all;
		@extend %no-mg-left--min480-max768;
		@extend %no-mg-right--under480;
	}

	...

	@media screen and (max-width: 480px) {
		$namespace : "under480";

		@include loopOfGridObject($namespace);
	}
```

#### Output.

```css
//#style.css
	.selector,.selector-two {
		padding : 0;
	}
    
	/* Your css here */

	.selector {
		color : white;
	}

	@media screen and (max-width: 480px) {
		.selector,.selector-two {
			margin-left : 0;
		}
	}

	@media screen and (min-width: 481px) and (max-width: 768px) {
		.selector,.selector-two {
			margin-right : 0;
		}
	}
```

#### You can contact me on Twitter : [@rs459](http://twitter.com/rs459)
