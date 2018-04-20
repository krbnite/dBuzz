Some things to check out:
* http://www.learncpp.com/


------------------------------------



So you want to learn C?  Me too.  That's why I'm writing this.

I know Python is a dynamic language, and C is --- some other kind.  But I'll be using
analogies with Python throughout anyway.  

Ok...  http://www.learn-c.org/

So in Python, there is a standard library, which is conveniently present whenever Python is called. 
In C, to use its standard library, you have to specify that in each script you write.  To specify
a library is generally not much different than Python's `import library`:
```c
#include <stdio.h>
```

Now C is not object-oriented, but it can still be modular by writing various functions and calling
them in a `main()` function:
```c
#include <stdio.h>

int main() {
    #include <stdio.h>
    print_hey();
    print_oh();
return 0;
}

int print_hey() {
    printf("Hey");
return 0;
}

int print_oh() {
    printf("oh!");
return -1;
}
```

Several things to observe:
1. For some reason we had to `#include <stdio.h>` in `main()` as well as the parent environment.
2. However, `#include <stdio.h>` did not need to be included in the non-main function, `print_hey()`
3. Since these functions are meant for printing, we just return an int...the value of which seems arbitrary after trying out various values.  
4. Each command/statement needs a semi-colon (aside from `#include` statements)
5. Functions are bracketed, {}

--------------------------------------------------------------------------

## Vars and Types
The basic/atomic types are:
1. Integers
  * char
    - why is this considered an integer?
  * int
  * short
  * long
  * long long
2. Unsigned Integers
  * unsigned char
  * unsigned int
  * etc (unsigned \<Integer Type\>)
3. Floating Point Numbers
  * float
  * double
4. Structures
  * you know, dictionary thingies


http://www.learn-c.org/en/Variables_and_Types
