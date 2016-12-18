#The Base Converter Algorithm

##The algorithm:

we can easily modify the divideBy2 algorithm to make it work as a converter from decimal to any base. Instead of dividing the decimal number by 2, we can pass the desired base as an argument to the method and use it in the divisions instead of the number 2:

```javascript
function baseConverter(decNumber, base) {
    var remStack = new Stack(),
        rem,
        baseString = '',
        digits = '0123456789ABCDEF'; // line 6

    while(decNumber > 0) {
        rem = Math.floor(decNumber % base);
        remStack.push(rem);
        decNumber = Math.floor(decNumber / base);
    }

    while(!remStack.isEmpty()) {
        baseString += digits[remStack.pop()]; // line 7
    }
    return baseString;
}
```

There is something that we are adding here that was not present in the divideBy2 algorithm. In the conversion from decimal to binary, the remainders are 0 or 1. In the conversion from decimal to octagonal, the remainders can be 0 - 8, but in the conversion from decimal to hexadecimal, the remainders can be 0 - 9 plus A - F. For this reason, we need to convert these values as well (line 6 and 7). We can use the previous algorithm, and output its result to the console as follows:

```javascript
console.log(baseConverter(100345, 2)); // base 2 binary
console.log(baseConverter(100345, 8)); // base 8 octagonal
console.log(baseConverter(100345, 16)); // base 16 hexadecimal
```

https://simple.wikipedia.org/wiki/Hexadecimal_numeral_system

```javascript
baseConverter(100345, 2)

100345/2 === 50,172 rem === 1
50172/2 === 25086 rem === 0
25086/2 === 12543 rem === 0
12543/2 === 6271 rem === 1
6271/2 === 3135 rem === 1
3135/2 === 1567 rem === 1
1567/2 === 783 rem === 1
783/2 === 391 rem === 1
391/2 === 195 rem === 1
195/2 === 97 rem === 1
97 /2 === 48 rem === 1
48/2 === 24 rem === 0
24/2 === 12 rem === 0
12/2 === 6 rem === 0
6/2 === 3 rem === 0
3/2 === 1 rem === 1
1/2 === 0 rem === 1

10011111111000011 -> 11000011111111001

baseConverter(100345, 8)

100345/8 === 12543 rem === 1
12543/8 === 1567 rem === 7
1567/8 === 195 rem === 7
195/8 === 24 rem === 3
24/8 === 3 rem === 0
3/8 === 0 rem === 3

177303 -> 303771

baseConverter(100345, 16)

100345/16 === 6271 rem === 9
6271/16 === 391 rem === 15 === 'F'
391/16 === 24 rem === 7
24/16 === 1 rem === 8
1/16 === 0 rem === 1

9F781 -> 187F9
```

Dividing by 1/16 (and even 1/8) is a bit tricky. Why? First of all, don't use your calculator beyond the first division by 16. You'll only confuse yourself.  This is how I approached the conversion to hexadecimal:

```javascript
baseConverter(100345, 16)

100345/16 === 6271 rem === 9

5625/10000 = n/16
n = 9

6271/16 === 391 rem === 15 === 'F'

9375/10000 = n/16
n = 15
15 === 'F'
rem === 'F'

391/16 === 24 rem === 7
4375/10000 = n/16
n = 7

24/16 === 1 rem === 8
5/10 = n/16
n = 8

1/16 === 0 rem === 1
```

To learn more about how the code for the algorithm works, please visit my repository entitled Decimal to Binary Algorithm:

https://github.com/interglobalmedia/decimal-to-binary-algorithm
