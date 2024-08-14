## Setting Up Your Mixins

```scss
@mixin for-phone-only {
  @media (max-width: 599px) { @content; }
}
@mixin for-tablet-portrait-up {
  @media (min-width: 600px) { @content; }
}
@mixin for-tablet-landscape-up {
  @media (min-width: 900px) { @content; }
}
@mixin for-desktop-up {
  @media (min-width: 1200px) { @content; }
}
@mixin for-big-desktop-up {
  @media (min-width: 1800px) { @content; }
}
```

## Using a Mixin

```scss
.header-title {  
   font-size: 2rem;  

   @include for-phone-only {    
      font-size: 1rem; 
   }
}
```

## Another Way to Setup Our Mixins

If you want to take it a step further, you could use conditionals to setup your mixins.

```scss
@mixin for-size($size) {
  @if $size == phone-only {
    @media (max-width: 599px) { @content; }
  } @else if $size == tablet-portrait-up {
    @media (min-width: 600px) { @content; }
  } @else if $size == tablet-landscape-up {
    @media (min-width: 900px) { @content; }
  } @else if $size == desktop-up {
    @media (min-width: 1200px) { @content; }
  } @else if $size == big-desktop-up {
    @media (min-width: 1800px) { @content; }
  }
}
```

Then, to use our mixins in this manner, we’d select it like so:

```scss
.header-title {  
   font-size: 2rem;  

   @include for-size(phone-only) {    
      font-size: 1rem; 
   }
}
```