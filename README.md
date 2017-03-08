# Octave Notes

These are my personal notes for using GNU Octave.  They are in no way
complete or comprehensive.  If you find them useful, great.  If you
don't, great.

## Random Comments

The output from commands terminated by `;` is suppressed. 

Ranges are defined by `start:step:end` and includes the `end` if a multiple of the `step` from the `start`.  If the `step` is omitted, assumed to be 1. 

Some base datatypes: `double`, `uint8`, `uint32`

## Scalar Math

```
isprime(12345554321)
factor(12345554321)
```

## Matrices

Arrays and matrices are 1-indexed.  Entries are accessed with parenthesis (e.g. `A(5)` or `B(2,5)`).

### Initialize a matrix

Init with identity, ones, or zeros.

```
x = eye(n);
x = eye(n,m);
x = ones(n);
x = ones(n,m);
x = zeros(n);
x = zeros(n,m);
```

Random matrix
```
x = rand(n);
x = rand(n,m);
x = uint32(100 * rand(5));
```

Manual init.

```
x = [1, 2, 3; 4, 5, 6];
```

Reshape a 1-d array 

```
x = [1:8,2,4];
```

### Solve a linear system.

```
A = [1,2,3; 4,5,6; 7,8,10];
b = [1;1;1];
A \ b
```

## Solving

### Polynomials Roots

Multiply polynomials with `conv`.  Devide polynomials with `deconv`.

```
a = [1,1,1,1];
b = roots(a)
c = deconv(a,[1,b(1)])
c = deconv(c,[1,b(2)])
c = deconv(c,[1,b(3)])
```

### Minimum of a 1-D Function

```
function [y] = f(x)
y = sin(100.0*x)/10.0 + (x-4) .* (x-4);
endfunction

[min_x, min_val, converge] = fminbnd(@f, -100, 100)

x = 3:.01:5;
y = f(x);
plot(x,y)
```

Note the importance of the `.*` in the definition of f.   This is not
needed for `fminbnd`, but is needed when computing `f(x)`.  Without the 
dot, octave tries to do an matrix multiplication and errors out. 

Also, can one line the function definition with 

```
f = @(x) sin(100.0*x)/10.0 + (x-4) .* (x-4);
```

## Programming/Loop Constructs

## Functions

## Images

### Load and Display an Image

Navigate to working directory in "File Browser".

```
I = imread("orig.jpg");
size(I)
imshow(I);
```

### Apply a Function to Every Pixel

First, a function quantizes to multiples of `m`.
```
function rv = quant(x, m)
    t = int32(x) ./ int32(m);
    rv = m * t;
    if (rv > 255)
        rv = 255 - mod(255,m);
    endif
    if (rv < 0) 
        rv = 0;
    endif
endfunction
```

Second, specialize to 8.  Octave has closures!
```
foo = @(y) @(x) uint8(quant(x,y));
quant8 = foo(8);
```

Finally, use `arrayfun` to apply the `quant8` to every pixel.
```         
I = imread("orig.jpg");
J = arrayfun(@quant8, I);
imshow(J);
```
I don't know what is going on behind the scenes, but the call to 
`arrayfun` is quite slow. 