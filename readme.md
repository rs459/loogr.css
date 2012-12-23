# Loogr.css

(Loop of object and grid reusable for CSS).
----------
Loogr :

With preprocessor it's hard to have a good maintenability for responsive||adaptative web design. One mixin respond to was created by Mason Wendell aka @codingdesigner.

But if you read this (article), you will find there is still an issue with the final result. To circumvent this problem, loogr use a mixin which takes as argument a namespace, then it generates a large number of placeholder with the name of the namespace at the end %myObject--namespace. It works as a series of reusable object that you pass to your CSS selectors via the mechanism of @extends.

pro :

- Take full advantage of new feature inside SASS 3.2.x with placeholder capability.
- Everything will be inside the same @media rules.
- Your html or your template (i love jade) stay clear. (you can reuse it, project after project).
- Your add role class or identity class on your html (no non-semantic class like .bordered .float .clearfix).
- You can mix it with Oocss approach.
- You don't loose the possibility to use the respond-to mixins.
- ...

cons :

- Your selector will be appear, in many place inside your stylesheet. (but for big project that's could be acceptable).
- ...

TODO : write a better documentation with example.

## Example :

#### You create your own mediaqueries.

```scss
//#style.scss
    @media screen and (max-width: 480px) {

    }
```
#### You add a namespace for each mediaqueries.

```
//#style.scss
    @media screen and (max-width: 480px) {
        $namespace : "under480";  
    }

    @media screen and (min-width: 481px) and (max-width: 768px) {
        $namespace : "min480-max768";
    }
```

#### You insert all object inside these mediaqueries and one outside mediaqueries with "all" as argument.

```
//#style.scss

    @include loogr(all);

    // Your css here 
    ....

    @media screen and (max-width: 480px) {
        $namespace : "under480";

        @include loogr($namespace);
    }

    @media screen and (min-width: 481px) and (max-width: 768px) {
        $namespace : "min480-max768";

        @include loogr($namespace);
    }
```

#### Style your website and use @extend with placeholder each of them have a namespace.

```
//#style.scss

    /* Your css here */

    .selector {
        color : white; // You should create this inside the loogr mixin.
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

        @include loogr($namespace);
    }
```

#### Output.

```
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
##### You can contact me on Twitter : @rs459