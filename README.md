# Octave Notes

These are my personal notes for using GNU Octave.  They are in no way
complete or comprehensive.  If you find them useful, great.  If you
don't, great.

## Random Comments

## Matrices

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

