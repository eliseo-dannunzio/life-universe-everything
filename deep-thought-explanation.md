#Explanation of the code

`setTimeout("alert(((_=_=>(_<<-~-~[])|-~[])(_(-~[])))<<-~[])",($=$=>$<<-~-~-~[]|-~[])((_=_=>_<<-~[]|-~[])(_(_(_($($($(-~[]))))))))^-~[])`

**So what's going on in this code?**

Two parts, we've got a "setTimeout" call for an alert of 42...

*But...* I hear you ask... *How is all that gobbledy-gook working?*

Let's first concentrate on part 1 of the code within the alert. We're ultimately trying to push an `alert` of the value `42`. I wanted a little creativity in how I coded this value, I wanted to build it up using bitwise operations where possible. The plan was to do the following:

`((((1<<2)|1)<<2)|1)<<1` which equates to `42`... Scary, but JavaScript works in mysterious ways...

How does `((((1<<2)|1)<<2)|1)<<1` work out 42?

Let's dig a little...

1) `1<<2` pushes 1 two bits to the left and fills the right with zero as it does so; which means instead of `1` in binary, we get `100` which equates to 4...

2) Next, we're applying a bitwise `or` to the value of `1`:

    4: 100
    1: 001
    ------
    5: 101

The resulting `OR` gives us `5`

3) Next we repeat steps 1 and 2 once again... First step results in `10100` which gives us `16 + 4 = 20`. Applying a bitwise `or` results in the `20` getting a +1, which makes it `21` (`10101`).

4) We then do another left-handed shift of bits, but this time only by one bit... making `101010`, which is equivalent to `42`.

*So now that we have the `42` established, how did the fancy code work out that way?*

`-~[]` is a non-alphanumeric means by which we can express the value of `1` in JavaScript. The explanation is as follows:

1) `[]` is an empty array, which when coerced with a bit-wise complement operator, the tilde (`~`), treats that empty array as a falsy value, and thus is equivalent to `~0` which equates to `-1`;

2) The act of negating it at the front, then converts the `-1` to `1`

3) Additional `-~` result in multiple additions of `1`, so `-~-~[]` is equivalent to `2`.

So, given that, we now have `((((1<<2)|1)<<2)|1)<<1` now being equivalent to `((((-~[]<<-~-~[])|-~[])<<-~-~[])|-~[])<<-~[]` which is pretty lengthy... I wanted to punch it up a bit... I noticed that the original code had a bit of a pattern, and so you technically could do:

  function _shift(i){
    return (i<<2)|1;
  }
  console.log(_shift(_shift(1))<<1);
  
From this, you had your console displaying `42`.

So I decided to play on a little ES6 fat arrow notation. Also reduced variables to `$` and `_` variables, to develop a rather non-alphanumeric answer:

  (_=_=>((_<<-~-~[])|-~[]))(_(-~[]))<<-~[]
  
So the first encapsulation `(_=_=>((_<<-~-~[])|-~[]))` is the definition of the `_` function, but because we're encapsulating it, we're then using it to apply it to another instance of the function... essentially doing `_(_(1))<<1`.


  
