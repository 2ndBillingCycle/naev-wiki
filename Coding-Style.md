# Introduction

The exact coding style for Naev has been asked before. First off let's mention the two golden rules of Naev coding development:

* We want contributions rather than scare off contributors. Therefore we are not really strict. However if you do a good job following our coding style you shall be praised for it.
* We want readable and well documented code. Even if you've done an awesome optimization, if we can't understand it, chances are it'll get rewritten or modified in a way that creates bugs. So please focus on readability first and then optimizations second. 

# Some Details

## Doxygen

It is FUNDAMENTAL that everything be clearly documented. To help with this it's generally a good idea to use doxygen. For example we can do:

```
/**
 * @brief Checks if a foo_t is bar.
 *
 * Longer explanation of what exactly this does and how it does it here.
 *
 * @note foo must not be NULL.
 *
 *    @param foo foo_t to check if is bar.
 *    @return 1 if foo is bar, 0 otherwise.
 */
int foo_isBar( foo_t foo )
{
   return (foo == bar);
}
```

This is a clear way to document. However, doxygen does not exclude you from documenting the code also. Especially if it's a complicated part.

## Indentation

We use 3 spaces instead of tabs. This can be achieved by putting the following in your `~/.vimrc`:

```vim
set tabstop=3           " indents
set softtabstop=3       " treat 3 spaces as a single character (when deleting)
set shiftwidth=3        " more indents
set expandtab           " use spaces instead of tabs
```

## Function Declarations

Generally we declare functions as:

```
type function( type1* param1, type param2 );
```

However if there are no parameters we do it as:

```
type function (void);
```

With brackets we do:

```
type function (void)
{
   some_code();
}
```

## Variables

We declare variables at the top of the function right after the opening bracket. Note that when declaring pointers we do differently from function declarations. For example:

```
void function( type* pointer )
{
   type *pointer, not_pointer;
}
```

The point is to increase readability as:

```
type* pointer, not_pointer;
```

Is harder to understand.

## Conditional Expressions

We use the following formatting:

```
if (something) {
   do_something();
}
```

However if it's more readable and there's only one line we can avoid brackets:

```
if (something)
   do_something();
```

If there are multiple statements it is recommended to use explicit parenthesis:

```
if ((some_value == 0) && (some_pointer != NULL))
   do_something();
```

It is recommended to compare against NULL instead of just checking the pointer. For example:

```
if (some_pointer != NULL)
```

instead of

```
if (some_pointer)
```

As it's more explicit on the type.

## Loops

We prefer to check against conditions instead of for conditions to avoid indentation. For example:

```
for (i=0;i<N;i++) {
   if (!foo_isBar(&foo[i]))
      continue;
   DEBUG( "foo is bar" );
}
```

This helps make code more readable. 