def move_zeros(lst):
    zeroes = []
    non_zeroes = []
    for element in lst:
        if element == 0:
            zeroes.append(element)
        else:
            non_zeroes.append(element)
    return non_zeroes + zeroes

---

def identity(a): return a

def zero(f=identity): return f(0)
def one(f=identity): return f(1)
def two(f=identity): return f(2)
def three(f=identity): return f(3)
def four(f=identity): return f(4)
def five(f=identity): return f(5)
def six(f=identity): return f(6)
def seven(f=identity): return f(7)
def eight(f=identity): return f(8)
def nine(f=identity): return f(9)

def plus(b): return lambda a: a + b
def minus(b): return lambda a: a - b
def times(b): return lambda a: a * b
def divided_by(b): return lambda a: a // b
