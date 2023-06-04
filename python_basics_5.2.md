# Yandex handbook "Python Basics" answers

5.2. Волшебные методы, переопределение методов. Наследование

A. Классная точка 3.0
```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def move(self, shift_x, shift_y):
        self.x += shift_x
        self.y += shift_y

    def length(self, p):
        return round(((self.x - p.x)**2 + (self.y - p.y)**2)**0.5, 2)


class PatchedPoint(Point):
    def __init__(self, *args):
        if not args:
            self.x, self.y = 0, 0
        elif len(args) == 1:
            self.x, self.y = args[0]
        else:
            self.x, self.y = args  
```
B. Классная точка 4.0
```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def move(self, shift_x, shift_y):
        self.x += shift_x
        self.y += shift_y

    def length(self, p):
        return round(((self.x - p.x)**2 + (self.y - p.y)**2)**0.5, 2)


class PatchedPoint(Point):

    def __init__(self, *args):
        if not args:
            self.x, self.y = 0, 0
        elif len(args) == 1:
            self.x, self.y = args[0]
        else:
            self.x, self.y = args

    def __str__(self):
        return f"({self.x}, {self.y})"

    def __repr__(self):
        return f"PatchedPoint({self.x}, {self.y})"
```
C. Классная точка 5.0
```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y

    def move(self, shift_x, shift_y):
        self.x += shift_x
        self.y += shift_y

    def length(self, p):
        return round(((self.x - p.x)**2 + (self.y - p.y)**2)**0.5, 2)


class PatchedPoint(Point):
    def __init__(self, *args):
        if not args:
            self.x, self.y = 0, 0
        elif len(args) == 1:
            self.x, self.y = args[0]
        else:
            self.x, self.y = args

    def __str__(self):
        return f"({self.x}, {self.y})"

    def __repr__(self):
        return f"PatchedPoint({self.x}, {self.y})"

    def __add__(self, other):
        return PatchedPoint(self.x + other[0], self.y + other[1])

    def __iadd__(self, other):
        self.move(other[0], other[1])
        return self
```
D. Дроби v0.1
```python
class Fraction:

    def __simp(self, coords):
        a, b = coords[0], coords[1]
        while b:
            a, b = b, a % b
        return coords[0] // a, coords[1] // a

    def __init__(self, *args):
        if isinstance(args[0], str):
            self.n, self.d = self.__simp(tuple(map(int, args[0].split('/'))))
        else:
            self.n, self.d = self.__simp(args)

    def numerator(self, number=0):
        if number:
            self.n, self.d = self.__simp((number, self.d))
        return self.n

    def denominator(self, number=0):
        if number:
            self.n, self.d = self.__simp((self.n, number))
        return self.d

    def __str__(self):
        return f"{self.n}/{self.d}"

    def __repr__(self):
        return f"Fraction({self.n}, {self.d})"
```
E. Дроби v0.2
```python
class Fraction:

    def __simp(self, coords):
        a, b = coords[0], coords[1]
        while b:
            a, b = b, a % b
        return coords[0] // a, coords[1] // a

    def __init__(self, *args):
        if isinstance(args[0], str):
            self.n, self.d = self.__simp(tuple(map(int, args[0].split('/'))))
        else:
            self.n, self.d = self.__simp(args)

    def numerator(self, number=0):
        if number:
            if self.n > 0:
                self.n, self.d = self.__simp((abs(number), self.d))
                self.n = -self.n if number < 0 else self.n
            elif self.n < 0:
                self.n, self.d = self.__simp((abs(number), self.d))
                self.n = -self.n if number > 0 else self.n
        return abs(self.n)

    def denominator(self, number=0):
        if number:
            if self.n > 0:
                self.n, self.d = self.__simp((self.n, abs(number)))
                self.n = -self.n if number < 0 else self.n
            elif self.n < 0:
                self.n, self.d = self.__simp((abs(self.n), abs(number)))
                self.n = -self.n if number > 0 else self.n
        return self.d

    def __neg__(self):
        return Fraction(-self.n, self.d)

    def __str__(self):
        return f"{self.n}/{self.d}"

    def __repr__(self):
        return f"Fraction('{self.n}/{self.d}')"
```
F. Дроби v0.3
```python
class Fraction:

    def __simp(self, coords):
        a, b = coords[0], coords[1]
        while b:
            a, b = b, a % b
        return coords[0] // a, coords[1] // a

    def __init__(self, *args):
        if isinstance(args[0], str):
            self.n, self.d = self.__simp(tuple(map(int, args[0].split('/'))))
        else:
            self.n, self.d = self.__simp(args)

    def numerator(self, number=0):
        if number:
            if self.n > 0:
                self.n, self.d = self.__simp((abs(number), self.d))
                self.n = -self.n if number < 0 else self.n
            elif self.n < 0:
                self.n, self.d = self.__simp((abs(number), self.d))
                self.n = -self.n if number > 0 else self.n
        return abs(self.n)

    def denominator(self, number=0):
        if number:
            if self.n > 0:
                self.n, self.d = self.__simp((self.n, abs(number)))
                self.n = -self.n if number < 0 else self.n
            elif self.n < 0:
                self.n, self.d = self.__simp((abs(self.n), abs(number)))
                self.n = -self.n if number > 0 else self.n
        return self.d

    def __neg__(self):
        return Fraction(-self.n, self.d)

    def __add__(self, other):
        return Fraction(self.n * other.d + other.n * self.d, self.d * other.d)

    def __iadd__(self, other):
        self.n, self.d = self.__simp((self.n * other.d + other.n * self.d, self.d * other.d))
        return self

    def __sub__(self, other):
        return Fraction(self.n * other.d - other.n * self.d, self.d * other.d)

    def __isub__(self, other):
        self.n, self.d = self.__simp((self.n * other.d - other.n * self.d, self.d * other.d))
        return self

    def __str__(self):
        return f"{self.n}/{self.d}"

    def __repr__(self):
        return f"Fraction('{self.n}/{self.d}')"
```
G. Дроби v0.4
```python
class Fraction:

    def __simp(self, coords):
        a, b = coords[0], coords[1]
        while b:
            a, b = b, a % b
        return coords[0] // a, coords[1] // a

    def __init__(self, *args):
        if isinstance(args[0], str):
            self.n, self.d = self.__simp(tuple(map(int, args[0].split('/'))))
        else:
            self.n, self.d = self.__simp(args)

    def numerator(self, number=0):
        if number:
            if self.n > 0:
                self.n, self.d = self.__simp((abs(number), self.d))
                self.n = -self.n if number < 0 else self.n
            elif self.n < 0:
                self.n, self.d = self.__simp((abs(number), self.d))
                self.n = -self.n if number > 0 else self.n
        return abs(self.n)

    def denominator(self, number=0):
        if number:
            if self.n > 0:
                self.n, self.d = self.__simp((self.n, abs(number)))
                self.n = -self.n if number < 0 else self.n
            elif self.n < 0:
                self.n, self.d = self.__simp((abs(self.n), abs(number)))
                self.n = -self.n if number > 0 else self.n
        return self.d

    def __neg__(self):
        return Fraction(-self.n, self.d)

    def __add__(self, other):
        return Fraction(self.n * other.d + other.n * self.d, self.d * other.d)

    def __iadd__(self, other):
        self.n, self.d = self.__simp((self.n * other.d + other.n * self.d, self.d * other.d))
        return self

    def __sub__(self, other):
        return Fraction(self.n * other.d - other.n * self.d, self.d * other.d)

    def __isub__(self, other):
        self.n, self.d = self.__simp((self.n * other.d - other.n * self.d, self.d * other.d))
        return self

    def __mul__(self, other):
        return Fraction(self.n * other.n, self.d * other.d)

    def __imul__(self, other):
        self.n, self.d = self.__simp((self.n * other.n, self.d * other.d))
        return self

    def __truediv__(self, other):
        return Fraction(self.n * other.d, self.d * other.n)

    def __itruediv__(self, other):
        self.n, self.d = self.__simp((self.n * other.d, self.d * other.n))
        return self

    def reverse(self):
        self.n, self.d = self.__simp((self.d, self.n))
        return self

    def __str__(self):
        return f"{self.n}/{self.d}"

    def __repr__(self):
        return f"Fraction('{self.n}/{self.d}')"
```
H. Дроби v0.5
```python
class Fraction:

    def __simp(self, coords):
        a, b = coords[0], coords[1]
        while b:
            a, b = b, a % b
        return coords[0] // a, coords[1] // a

    def __init__(self, *args):
        if isinstance(args[0], str):
            self.n, self.d = self.__simp(tuple(map(int, args[0].split('/'))))
        else:
            self.n, self.d = self.__simp(args)

    def numerator(self, number=0):
        if number:
            if self.n > 0:
                self.n, self.d = self.__simp((abs(number), self.d))
                self.n = -self.n if number < 0 else self.n
            elif self.n < 0:
                self.n, self.d = self.__simp((abs(number), self.d))
                self.n = -self.n if number > 0 else self.n
        return abs(self.n)

    def denominator(self, number=0):
        if number:
            if self.n > 0:
                self.n, self.d = self.__simp((self.n, abs(number)))
                self.n = -self.n if number < 0 else self.n
            elif self.n < 0:
                self.n, self.d = self.__simp((abs(self.n), abs(number)))
                self.n = -self.n if number > 0 else self.n
        return self.d

    def __neg__(self):
        return Fraction(-self.n, self.d)

    def __add__(self, other):
        return Fraction(self.n * other.d + other.n * self.d, self.d * other.d)

    def __iadd__(self, other):
        self.n, self.d = self.__simp((self.n * other.d + other.n * self.d, self.d * other.d))
        return self

    def __sub__(self, other):
        return Fraction(self.n * other.d - other.n * self.d, self.d * other.d)

    def __isub__(self, other):
        self.n, self.d = self.__simp((self.n * other.d - other.n * self.d, self.d * other.d))
        return self

    def __mul__(self, other):
        return Fraction(self.n * other.n, self.d * other.d)

    def __imul__(self, other):
        self.n, self.d = self.__simp((self.n * other.n, self.d * other.d))
        return self

    def __truediv__(self, other):
        return Fraction(self.n * other.d, self.d * other.n)

    def __itruediv__(self, other):
        self.n, self.d = self.__simp((self.n * other.d, self.d * other.n))
        return self

    def reverse(self):
        self.n, self.d = self.__simp((self.d, self.n))
        return self

    def __gt__(self, other):
        return self.n / self.d > other.n / other.d

    def __ge__(self, other):
        return self.n / self.d >= other.n / other.d

    def __lt__(self, other):
        return self.n / self.d < other.n / other.d

    def __le__(self, other):
        return self.n / self.d <= other.n / other.d

    def __eq__(self, other):
        return self.n / self.d == other.n / other.d

    def __ne__(self, other):
        return self.n / self.d != other.n / other.d

    def __str__(self):
        return f"{self.n}/{self.d}"

    def __repr__(self):
        return f"Fraction('{self.n}/{self.d}')"
```
I. Дроби v0.6
```python
class Fraction:

    def __simp(self, coords):
        if len(coords) == 1:
            coords += (1,)
        a, b = coords[0], coords[1]
        while b:
            a, b = b, a % b
        return coords[0] // a, coords[1] // a

    def __init__(self, *args):
        if isinstance(args[0], str):
            self.n, self.d = self.__simp(tuple(map(int, args[0].split('/'))))
        else:
            self.n, self.d = self.__simp(args)

    def numerator(self, number=0):
        if number:
            if self.n > 0:
                self.n, self.d = self.__simp((abs(number), self.d))
                self.n = -self.n if number < 0 else self.n
            elif self.n < 0:
                self.n, self.d = self.__simp((abs(number), self.d))
                self.n = -self.n if number > 0 else self.n
        return abs(self.n)

    def denominator(self, number=0):
        if number:
            if self.n > 0:
                self.n, self.d = self.__simp((self.n, abs(number)))
                self.n = -self.n if number < 0 else self.n
            elif self.n < 0:
                self.n, self.d = self.__simp((abs(self.n), abs(number)))
                self.n = -self.n if number > 0 else self.n
        return self.d

    def __neg__(self):
        return Fraction(-self.n, self.d)

    def __add__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return Fraction(self.n * other.d + other.n * self.d, self.d * other.d)

    def __iadd__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        self.n, self.d = self.__simp((self.n * other.d + other.n * self.d, self.d * other.d))
        return self

    def __sub__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return Fraction(self.n * other.d - other.n * self.d, self.d * other.d)

    def __isub__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        self.n, self.d = self.__simp((self.n * other.d - other.n * self.d, self.d * other.d))
        return self

    def __mul__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return Fraction(self.n * other.n, self.d * other.d)

    def __imul__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        self.n, self.d = self.__simp((self.n * other.n, self.d * other.d))
        return self

    def __truediv__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return Fraction(self.n * other.d, self.d * other.n)

    def __itruediv__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        self.n, self.d = self.__simp((self.n * other.d, self.d * other.n))
        return self

    def reverse(self):
        self.n, self.d = self.__simp((self.d, self.n))
        return self

    def __gt__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return self.n / self.d > other.n / other.d

    def __ge__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return self.n / self.d >= other.n / other.d

    def __lt__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return self.n / self.d < other.n / other.d

    def __le__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return self.n / self.d <= other.n / other.d

    def __eq__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return self.n / self.d == other.n / other.d

    def __ne__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return self.n / self.d != other.n / other.d

    def __str__(self):
        return f"{self.n}/{self.d}"

    def __repr__(self):
        return f"Fraction('{self.n}/{self.d}')"
```
J. Дроби v0.7
```python
class Fraction:

    def __simp(self, coords):
        if len(coords) == 1:
            coords += (1,)
        a, b = coords[0], coords[1]
        while b:
            a, b = b, a % b
        return coords[0] // a, coords[1] // a

    def __init__(self, *args):
        if isinstance(args[0], str):
            self.n, self.d = self.__simp(tuple(map(int, args[0].split('/'))))
        else:
            self.n, self.d = self.__simp(args)

    def numerator(self, number=0):
        if number:
            if self.n > 0:
                self.n, self.d = self.__simp((abs(number), self.d))
                self.n = -self.n if number < 0 else self.n
            elif self.n < 0:
                self.n, self.d = self.__simp((abs(number), self.d))
                self.n = -self.n if number > 0 else self.n
        return abs(self.n)

    def denominator(self, number=0):
        if number:
            if self.n > 0:
                self.n, self.d = self.__simp((self.n, abs(number)))
                self.n = -self.n if number < 0 else self.n
            elif self.n < 0:
                self.n, self.d = self.__simp((abs(self.n), abs(number)))
                self.n = -self.n if number > 0 else self.n
        return self.d

    def __neg__(self):
        return Fraction(-self.n, self.d)

    def __add__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return Fraction(self.n * other.d + other.n * self.d, self.d * other.d)

    def __radd__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return Fraction(self.n * other.d + other.n * self.d, self.d * other.d)

    def __iadd__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        self.n, self.d = self.__simp((self.n * other.d + other.n * self.d, self.d * other.d))
        return self

    def __sub__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return Fraction(self.n * other.d - other.n * self.d, self.d * other.d)

    def __rsub__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return Fraction(other.n * self.d - self.n * other.d, self.d * other.d)

    def __isub__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        self.n, self.d = self.__simp((self.n * other.d - other.n * self.d, self.d * other.d))
        return self

    def __mul__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return Fraction(self.n * other.n, self.d * other.d)

    def __rmul__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return Fraction(self.n * other.n, self.d * other.d)

    def __imul__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        self.n, self.d = self.__simp((self.n * other.n, self.d * other.d))
        return self

    def __truediv__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return Fraction(self.n * other.d, self.d * other.n)

    def __rtruediv__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return Fraction(self.d * other.n, self.n * other.d)

    def __itruediv__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        self.n, self.d = self.__simp((self.n * other.d, self.d * other.n))
        return self

    def reverse(self):
        self.n, self.d = self.__simp((self.d, self.n))
        return self

    def __gt__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return self.n / self.d > other.n / other.d

    def __ge__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return self.n / self.d >= other.n / other.d

    def __lt__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return self.n / self.d < other.n / other.d

    def __le__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return self.n / self.d <= other.n / other.d

    def __eq__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return self.n / self.d == other.n / other.d

    def __ne__(self, other):
        other = other if isinstance(other, Fraction) else Fraction(other)
        return self.n / self.d != other.n / other.d

    def __str__(self):
        return f"{self.n}/{self.d}"

    def __repr__(self):
        return f"Fraction('{self.n}/{self.d}')"
```
