# nyquist-cheatsheet

## Table of Contents
- [pluck-chord.sal](#pluck)
- [sample.sal](#samp)
- [functional.sal](#functional)

## <a name="pluck"></a>pluck-chord.sal
```LISP
function pluck-chord(pitch, interval, n)
  begin
    with s = pluck(pitch)
    loop
      for i from 1 below n
      set s += pluck(pitch + interval * i)
    end
    return s
  end
```
```LISP
play pluck-chord(c3, 5, 2)
play pluck-chord d3, 7, 4) ~ 3
play pluck-chord(c2, 10, 7) ~ 8
```

## <a name="samp"></a>sample.sal
```LISP
define function my-sum(x, y: 1, z: 2)
  return x + y + z
```
```LISP
define function kwdemo(p, scale: 1, vibrato: nil)
  begin
    with s = pluck(p) * scale
    if vibrato then
      set s = s * (1 + lfo(6) * 0.1)
    return s
  end
```
```LISP
define function test-range(a-note)
  begin
    if a-note < 0 then
      return quote(too-low)
    else
      if a-note > 127 then
        return quote(too-high)
      else
        return quote(in-range)
  end
```
```LISP
define function make-list()
  begin
    loop
      with numlist
      for i from 0 to 10 by 2
      set numlist @= i    ; push at front of list
      finally set result = reverse(numlist)
    end
    return result
  end
```
```LISP
define function ten-numbers()
  begin
    loop
      repeat 10
      print random(100)
    end
  end
```
```LISP
set *h* = 15322

define function op-example()
  begin
    with a, b = 0, c = 1, d = {}, e = {}, f = -1, g = 0
    display "op-example", b
    set a = 1, b += 1, c *= 2, d &= 1, f <= 1, g >= 1, *h* -= 1
    display "op-example", b
    set a = 2, b += 1, c *= 2, d &= 2, e @= 2, f <= 2, g >= 2, *h* -= 1
    display "op-example", b
    set a = 3, b += 1, c *= 2, d &= 3, e @= 3, f <= 3, g >= 3, *h* -= 1
    display "op-example", b
    set a = 4, b += 1, c *= 2, d &= 4, e @= 4, f <= 4, g >= 4, *h* -= 1
    display "op-example", b
    set a = 5, b += 1, c *= 2, d &= 5, e @= 5, f <= 5, g >= 5, *h* -= 1
    display "results", a, b, c, d, e, f, g, *h*
  end

define function op-example2()
  begin
    loop
      with a, b = 0, c = 1, d = {}, e = {}, f = -1, g = 0
      for i from 1 to 5
      set a = i, b += 1, c *= 2, d &= i, e @= i, f <= i, g >= i, *h* -= 1
      finally display "results", a, b, c, d, e, f, g, *h*
    end
  end
```

## <a name="functional"></a>functional.sal
```LISP
function harmonics(hz, n)
  return simrep(i, n,
                hzosc(hz * (i + 1)) * rrandom())
```
```LISP
function mysound()
  return harmonics(440.0, 10) *
         env(0.05, 0.2, 0.5, 1, 0.5, 0.2)

play mysound()
```
