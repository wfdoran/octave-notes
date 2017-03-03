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

### Polynomials

Multiply polynomials with `conv`.  Devide polynomials with `deconv`.

```
a = [1,1,1,1];
b = roots(a)
c = deconv(a,[1,b(1)])
c = deconv(c,[1,b(2)])
c = deconv(c,[1,b(3)])
```

## Programming/Loop Constructs

## Functions

## Images

