# Multi grid system

This framework use : box-sing with border-box. (That's mean it don't support IE < 8)

--------
## example :

 - You want one grid of 12 for all viewport.
 - You want for the same content, but for another viewport 4 columns (or anything you want).

```html
	<div class="container">
		<section class="main-section">
		</section>
		<aside class="main-aside">
		</aside>
	</div>
```

```.container``` class provide a block already clearfixed for all viewport.

```scss
	.main-section {
		@extend %float-left--all;
		@extend %mg-right1of12--all;
		@extend %w8of12--all;

		@extend %no-mg-right--under480;
		@extend %w12of12--under480;

		@extend %no-mg-right--min480-max768;		
		@extend %w3of4--min480-max768;
	}

	.main-aside {
		@extend %float-left--all;
		@extend %w3of12--all;

		@extend %w12of12--under480;
		@extend %w1of4--min480-max768;
	}
```

output : 

```css

	...

	* { -moz-box-sizing: border-box; -webkit-box-sizing: border-box; box-sizing: border-box; }

	.main-aside {
		width: 25%; 
	}

	.main-section {
		width: 66.66667%; 
	}

	.main-section {
		margin-left: 8.33333%; 
	}

	.main-section, .main-aside {
  		float: left; 
  	}

	.container:before,
	.container:after {
		content: " ";
		display: table; 
	}

	.container:after {
		clear: both; 
	}

	.lt-ie8 .container {
	  zoom: 1; 
	}

	@media screen and (max-width: 480px) {
		
		.main-section, .main-aside {
			width: 100%; 
		}

		.main-section {
			margin-right: 0; 
		} 
	}

	@media screen and (min-width: 481px) and (max-width: 768px) {
	  
		.main-aside {
	    	width: 25%; 
	    }

		.main-section {
			width: 75%; 
		}

		.main-section {
			margin-right: 0; 
		} 
	}

```

__You don't have to worry about the large number of grid, only what you use will be in the output,
thank's to placeholder in SASS 3.2.x .__

You have any grid you want in pourcentage width :

```scss

	...

	@each $gridlength in 48, 40, 32, 24, 20, 16, 12, 10, 8, 6, 5, 4, 3 {

		...

	}

	...

```

you can limit the column count : 

```scss
	$maxColumnCount : 24;
```
Each value over this number will generate only padding and margin for it.

example : you want to have a grid of 24.

	23/24 width + 1/48 margin-left + 1/48 margin-right = 24/24 width