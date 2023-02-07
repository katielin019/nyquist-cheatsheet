# nyquist-cheatsheet

```SAL
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

```SAL
play pluck-chord(c3, 5, 2)
play pluck-chord d3, 7, 4) ~ 3
play pluck-chord(c2, 10, 7) ~ 8
```
