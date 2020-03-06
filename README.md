# @system is a mobile first mixin with super powers
Heavily inspired by [TailwindCSS](https://github.com/tailwindcss/tailwindcss) and [styled-system](https://github.com/styled-system/styled-system)

### Requirements:

The only requirement is a $breakpoint list or map  

Example:
```
$breakpoints: 0, 768px, 1024px, 1280px;
```
or
```
$breakpoints: (
  sm: 0,
  md: 768px,
  lg: 1024px,
  xl: 1280px
);
```

### Usage
Simply map your css properties using the mixin @system  

Esample:
```
.block {
  @include system((
    font-family: '"lucida grande", Arial, sans-serif',
    font-size: (1rem, 2rem, 3rem),
    font-weight: 700,
    color: (white, black),
    display: (block, flex),
    bg: (black, white),
    mx: (10px, null, 20px),
    p: 10px
  ));
}
```
Result:
```
.block {
    font-family: "lucida grande", Arial, sans-serif;
    font-size: 1rem;
    font-weight: 700;
    color: white;
    display: block;
    background: black;
    margin-left: 10px;
    margin-right: 10px;
    padding: 10px;
}
@media (min-width: 768px) {
    .block {
        font-size: 2rem;
        color: black;
        display: flex;
        background: white;
    }
}
@media (min-width: 1024px) {
    .block {
        font-size: 3rem;
        margin-left: 20px;
        margin-right: 20px;
    }
}
```

### How it works
As property, you can use a default CSS property or an [alias](#aliases).  
As value, you can use: a string, a color, a number, null or a list.

What happen when you use a list?
```
font-size: (1rem, 2rem, 3rem)
```
Remember your $breakpoints!
```
$breakpoints: 0, 768px, 1024px, 1280px;
```
That means that every value in a list will be assigned to his corresponding breakpoint,  
so in this case
```
//default: 
font-size: 1rem;

@media (min-width: 768px) {
    font-size: 2rem;
}

@media (min-width: 1024px) {
    font-size: 3rem;
}
```
What if you use a null?  
in @system, null means that value will be skipped in his corresponding breakpoint.  
If you have something like
```
font-size: (1rem, null, 3rem)
```
The result will be:
```
//default: 
font-size: 1rem;

@media (min-width: 1024px) {
    font-size: 3rem;
}
```
That's it!


#Aliases
An alias is an abbreviation for one or more CSS properties.
Here's a list of the available aliases
```
inset: (top, right, bottom, left),

bg: background,

m: margin,
mt: margin-top,
mr: margin-right,
mb: margin-bottom,
ml: margin-left,
mx: (margin-left, margin-right),
my: (margin-top, margin-bottom),

p: padding,
pt: padding-top,
pr: padding-right,
pb: padding-bottom,
pl: padding-left,
px: (padding-left, padding-right),
py: (padding-top, padding-bottom),

w: width,
min-w: min-width,
max-w: max-width,

h: height,
min-h: min-height,
max-h: max-height,
```

Example:
```
inset: 0,
mx: (10px, null, 20px)
```
will produce:
```
top: 0;
right: 0;
bottom: 0;
left: 0;
margin-left: 10px;
margin-right: 10px;


@media (min-width: 1024px) {
    margin-left: 20px;
    margin-right: 20px;
}
```