---
layout: post
title: 'Solutions to Elements of Programming Interviews, Chapter 5'
date: 2023-02-26 10:12:34 -0400
categories: jekyll update
---

Here are my solutions to the aforementioned book and chapter.

{% highlight python %}
# 5.1
# 5.1
def test_1():
    assert (dutch([0, 1, 2, 0, 2, 1, 1], 1) == [0, 0, 1, 1, 1, 2, 2])


def dutch(arr, i):
    pivot = arr[i]
    a = 0
    b = len(arr) - 1
    current = 0
    while current <= b:
        print(arr)
        if arr[current] < pivot:
            if current == a:
                a += 1
                current += 1
            else:
                arr[a], arr[current] = arr[current], arr[a]
                a += 1
        elif arr[current] > pivot:
            if current == b:
                b -= 1
                current += 1
            arr[b], arr[current] = arr[current], arr[b]
            b -= 1
        else:
            current += 1
    return arr


# 5.2
def test_f():
    assert (increment_integer([1, 2, 9]) == [1, 3, 0])
    assert (increment_integer([1]) == [2])
    assert (increment_integer([9, 9]) == [1, 0, 0])


def increment_integer(lst):
    i = len(lst) - 1
    nine = False
    while i >= 0:
        if lst[i] == 9:
            lst[i] = 0
            i -= 1
            nine = True
        else:
            break
    if i == -1 and nine:
        lst = [0] + lst
        i += 1
    lst[i] += 1
    return lst


#  5.2 Variant

def test_g():
    assert (add_binary('11', '10') == '101')
    assert (add_binary('111', '10') == '1001')


def add_binary(s, t):
    i = len(s) - 1
    j = len(t) - 1
    carry = 0
    new = []
    while i >= 0 or j >= 0 or carry:
        x = 0

        if i >= 0 and s[i] == '1':
            x += 1
        if j >= 0 and t[j] == '1':
            x += 1
        x += carry
        new = [str(x % 2)] + new
        carry = x // 2
        i -= 1
        j -= 1

    return "".join(new)


# 5.3
def test_h():
    assert (multiply_better([1, 2], [1, 2]) == [1, 4, 4])
    assert (multiply_better([1, 9, 3, 7, 0, 7, 7, 2, 1], [-7, 6, 1, 8, 3, 8, 2, 5, 7, 2, 8, 7]) == [-1, 4, 7, 5, 7, 3,
                                                                                                    9, 5, 2, 5, 8, 9, 6,
                                                                                                    7, 6, 4, 1, 2, 9, 2,
                                                                                                    7])


def multiply(x, y):
    neg = 1
    if x[0] < 0 and y[0] < 0:
        x[0] *= -1
        y[0] *= -1
    elif x[0] < 0:
        x[0] *= -1
        neg = -1
    elif y[0] < 0:
        y[0] *= -1
        neg = -1

    r = []

    def add_to_ret(ret, z):
        print(ret, z)
        i = len(z) - 1
        j = len(ret) - 1
        carry = 0
        while i >= 0 or carry > 0:
            if j < 0:
                j += 1
                ret = [0] + ret

            sm = (z[i] if i >= 0 else 0) + ret[j] + carry
            if sm >= 10:
                carry = 1
                sm -= 10
            else:
                carry = 0
            ret[j] = sm

            i -= 1
            j -= 1
        return ret

    a = len(x) - 1
    a_tens = 0
    while a >= 0:
        b = len(y) - 1
        b_tens = 0
        while b >= 0:
            mult = x[a] * y[b]
            mult_list = [0 for _ in range(a_tens + b_tens)]
            while mult > 0:
                mult_list = [mult % 10] + mult_list
                mult //= 10
            r = add_to_ret(r, mult_list)
            b_tens += 1
            b -= 1
        a_tens += 1
        a -= 1

    r[0] *= neg
    return r


def multiply_better(num1, num2):
    sign = -1 if (num1[0] < 0) ^ (num2[0] < 0) else 1
    num1[0], num2[0] = abs(num1[0]), abs(num2[0])
    result = [0] * (len(num1) + len(num2))

    for i in reversed(range(len(num1))):
        for j in reversed(range(len(num2))):
            print(i, j)
            result[i + j + 1] += num1[i] * num2[j]
            result[i + j] += result[i + j + 1] // 10
            result[i + j + 1] %= 10
    # Remove the leading zeroes,
    result = result[next((i for i, x in enumerate(result)
                          if x != 0), len(result)):] or [0]
    return [sign * result[0]] + result[1:]


# 5.4
def test_i():
    assert (advance_better([3, 3, 1, 0, 2, 0, 1]) == True)
    assert (advance_better([3, 2, 0, 0, 2, 0, 1]) == False)


def advance(array):
    possible = [0 for _ in range(len(array))]
    possible[0] = 1
    for i, a in enumerate(array):
        if possible[i] == 1:
            for j in range(i + 1, i + a + 1):
                if j == len(array):
                    break
                possible[j] = 1
    return possible[-1] == 1


def advance_better(array):
    farthest = 0
    for i in range(len(array)):
        if i > farthest:
            break
        farthest = max(farthest, i + array[i])

    return farthest >= len(array) - 1


# 5.4 Variant

def test_j():
    assert (min_steps_to_advance([3, 3, 0, 2, 1, 0]) == 2)


def min_steps_to_advance(array):
    min_steps = [999999 for _ in array]
    min_steps[0] = 0
    for i, a in enumerate(array[:-1]):
        for j in range(i + 1, i + a + 1):
            if j == len(array):
                break
            min_steps[j] = min(min_steps[j], min_steps[i] + 1)
    return min_steps[-1]


# 5.5

def test_k():
    assert (delete_duplicates([2, 3, 5, 5, 7, 11, 11, 11, 13]) == [2, 3, 5, 7, 11, 13, 0, 0, 0])


def delete_duplicates(array):
    next_open = 1
    last = array[0]
    for i, a in enumerate(array[1:]):
        if a != last:
            array[next_open] = a
            last = a
            next_open += 1
    for i in range(next_open, len(array)):
        array[i] = 0
    return array


# 5.5 Variant

def test_l():
    array = [5, 3, 1, 2, 3, 2, 5, 6]
    assert (remove_key(array, 3) == 2)
    assert (array == [5, 6, 1, 2, 5, 2, 5, 6])

    array = [5, 3, 1, 2, 3, 2, 5, 3]
    assert (remove_key(array, 3) == 3)
    assert (array == [5, 5, 1, 2, 2, 2, 5, 3])

    array = [5, 3, 1, 2, 3, 2, 5, 6]
    assert (remove_key_better(array, 3) == 2)
    assert (array == [5, 1, 2, 2, 5, 6, 5, 6])

    array = [5, 3, 1, 2, 3, 2, 5, 3]
    assert (remove_key_better(array, 3) == 3)
    assert (array == [5, 1, 2, 2, 5, 2, 5, 3])


def remove_key(array, key):
    i = 0
    j = len(array) - 1
    while i <= j:
        if array[i] == key:
            array[i] = array[j]
            j -= 1
        else:
            i += 1

    return (len(array) - j) - 1


def remove_key_better(array, key):  # Actually correct implementation that shifts
    open_index = 0
    i = 0
    for i in range(len(array)):
        if array[i] != key:
            array[open_index] = array[i]
            open_index += 1
        i += 1
    return len(array) - open_index


# 5.5 Variant 2

def test_weird():
    assert (weird([1, 2, 3, 3, 3, 4, 4, 5, 5, 5, 5, 6], 3) == [1, 2, 3, 3, 4, 4, 5, 5, 5, 5, 6, 6])
    assert (weird([1, 1, 1, 1, 2, 2, 2, 3, 3], 4) == [1, 1, 2, 2, 2, 3, 3, 3, 3])


def weird(array, m):
    if m == 1 or m == 2:
        return array
    last = array[0]
    occ = 1
    last_open = 1
    print(list(enumerate(array[1:])))
    for i, a in enumerate(array):
        if i == 0: continue
        print(array, a, last, i, last_open, len(array))
        if a == last:
            occ += 1
        else:
            if occ == m:
                last_open -= (m - 2)
            occ = 1
            last = a
        array[last_open] = a
        last_open += 1
    print(array)
    return array


# 5.6
def test_stock():
    assert (stock([310, 315, 275, 295, 260, 270, 290, 230, 255, 250]) == 30)
    assert (stock([300, 350, 250, 260, 330]) == 80)


def stock(array):
    mn = array[0]
    best = 0
    for a in array[1:]:
        if a < mn:
            mn = a
        elif a - mn > best:
            best = a - mn
    return best


# 5.6 Variant 1
def test_longest_subarray():
    assert (longest_subarray([5, 5, 3, 3, 3, 1, 3, 1, 4, 4]) == 3)


def longest_subarray(array):
    occ = 1
    current = array[0]
    longest = 1
    for a in array[1:]:
        if a != current:
            longest = max(occ, longest)
            current = a
            occ = 1
        else:
            occ += 1
    longest = max(occ, longest)
    return longest


# 5.7
def test_stock_twice():
    assert (stock_twice([310, 315, 275, 295, 260, 270, 290, 230, 255, 250]) == 55)
    assert (stock_twice([12, 11, 13, 9, 12, 8, 14, 13, 15]) == 10)


def stock_twice(array):
    mn = array[0]
    sell_by = [0 for _ in array]
    for i, a in list(enumerate(array))[1:]:
        sell_by[i] = max(sell_by[i - 1], a - mn)
        mn = min(mn, a)

    mx = array[-1]
    ret = float('-inf')
    for i, a in reversed(list(enumerate(array))):
        ret = max(ret, mx - a + (sell_by[i - 1] if i != 0 else 0))
        mx = max(mx, a)
    return ret


# 5.7 Variant 1
def test_stock_twice_variant():
    assert (stock_twice_variant([310, 315, 275, 295, 260, 270, 290, 230, 255, 250]) == 55)
    assert (stock_twice_variant([12, 11, 13, 9, 12, 8, 14, 13, 15]) == 10)


def stock_twice_variant(array):
    min_price_so_far = array[0]
    max_profit_after_first_sell = float('-inf')
    max_profit_after_buyback = float('-inf')
    max_profit = float('-inf')

    for a in array[1:]:
        max_profit = max(max_profit, max_profit_after_buyback + a)
        max_profit_after_buyback = max(max_profit_after_buyback, max_profit_after_first_sell - a)
        max_profit_after_first_sell = max(max_profit_after_first_sell, a - min_price_so_far)
        min_price_so_far = min(min_price_so_far, a)
    return max_profit


# 5.8
def test_alternating():
    array = [3, 1, 5, 6, 2, 6, 3, 6, 2, 3]
    ret = alternating(array)
    print(ret)
    for i in range(len(ret))[::2]:
        assert (ret[i] <= ret[i + 1])
    for i in range(len(ret))[1::2]:
        assert (ret[i] >= ret[i - 1])


def alternating(array):
    mod = 1
    for i in range(len(array))[1:]:
        if mod == 1:
            if array[i] < array[i - 1]:
                array[i - 1], array[i] = array[i], array[i - 1]
        else:
            if array[i] > array[i - 1]:
                array[i - 1], array[i] = array[i], array[i - 1]
        mod = 1 - mod
    return array


{% endhighlight %}
