# Advent of Code
Input data and solutions (in Jupyter notebook form, with links to the original problem).


## Lessons learned

When I attempted my first [Advent of Code](https://adventofcode.com/) in 2020 it was as a way of practising my python skills and learning by solving a different style of problem to my day-to-day work. Through lots of googling and help from Stack Overflow, this helped me:
- discover new techniques
- learn more about algorithms
- discover libraries and features of python I wasn't aware of
- identify performance bottlenecks and more code- and time-efficient solutions

Some of these are documented here for posterity:

- **list/dict comprehensions**
  - `squares_list = [x**2 for x in range(10)]`
  - `squares_dict = {x:x**2 for x in range(10)}`
  - `if` condition at end of comprehension v. useful for filtering/matching other lists
- **sets** (`squares_set = {1,4,9,16}`)
  - Unordered, unindexed, no duplicates
  - Lots of set arithmetic methods, e.g. 
    - intersection: `set_a & set_b & set_c` or `set_a.intersection(set_b, set_c)`
    - union: `set_a | set_b` or `set_a.union(set_b)`)
- **`zip`ping iterators** - use `zip(a,b)` as an iterator of tuples `(a,b)` through iterators `a` and `b` in parallel
- **Packing/unpacking with `*` (positional arguments) and `**` (keyword arguments)** [[see here]](https://www.geeksforgeeks.org/python-star-or-asterisk-operator/). I've seen this often in function definitions but kind of ignored it until now. It became useful to unpack a list into multiple arguments with `*` (e.g. intersection of many sets with `set.intersection(*list_of_sets)`) or unpack a dictionary with `**` (e.g. combining two dictionaries `d1` and `d2` with `new_dict = {**d1, **d2}`)
- **DIY generators** - never bothered to make my own before, but less intimidated than I would have been before. Basically just a function that `yield`s values one at a time rather than `return`ing. For example, cell 2 of my [Day 9 solution](https://github.com/samnlindsay/advent_of_code/blob/main/Day09-EncodingError.ipynb) defines `sliding_window()` which `yield`s a chunk of the list provided and steps through the list until the end.
- **regex** (`re` library, or enhanced version `regex`)
  - Coming from `stringr` in R and latterly using SQL/PySpark, I still find the `re`/`regex` API confusing and have to look up the expected arguments and the contents of the "match object" returned, as well as differences between e.g. `match` (find all instances of a pattern) vs `search` (find the _first_ instance of a pattern)
  - A new regex trick I discovered, which isn't supported in `re` but is in `regex` is the idea of recursion in a regex, to match balanced constructs like nested brackets. The simple version (described [here](regular-expressions.info/recurse.html) before going deeper) can be applied in Part 2 of [Day 19](https://adventofcode.com/2020/day/19) to match any string in the form `ab`, `aabb`, `aaabbb` etc. with the regex pattern `a(?R)?b`. The `(?R)` tells the regex engine to start again looking for `a` until it fails and moves onto `b`. However many levels of recursion reached in the first part (`a`), the pattern isn't completed until that many `b`s are detected. (`a` and `b` can themselves be entire patterns)
- **[`parse`](https://pypi.org/project/parse/) library** - kind of like a reverse-engineered f-string, as an alternative to regex for predictable formatting. For example, `p = parse.compile("{field}: {a:d}-{b:d} or {c:d}-{d:d}")` creates a parser that looks for strings like `"age: 18-30 or 31-49"`. Then `p.parse(test_string)` produces a dict returning `{"field": "age", "a": 18, ...}` (example from [Day 16](https://github.com/samnlindsay/advent_of_code/blob/main/Day16-TicketTranslation.ipynb))
- **`collections` library**
  - [`Counter`](https://docs.python.org/3/library/collections.html#collections.Counter) - useful for counting instances of a value in a list of values, and storing as a dict - e.g. `wins = Counter(list_of_world_cup_winners)` - `wins["England"]` returns `1` while `wins["Wales"]` returns `0` (for obvious reasons), and `wins.most_common(1)` returns `('Brazil', 5)` 
  - [`defaultdict`](https://docs.python.org/3/library/collections.html#collections.defaultdict) - same as any other dict but if a new key is encountered, it is given a default value, depending on value type (e.g. `0` for `int` or `[]` for `list`)
  - [`deque`](https://docs.python.org/3/library/collections.html#collections.deque) - "double-ended queue" (which I refuse to pronounce "deck") to optimise various list operations and iteration, where indexing the list is not needed. Didn't use this when I probably could have, and then tried to use it where [I probably shouldn't have](https://github.com/samnlindsay/advent_of_code/blob/main/Day23-CrabCups.ipynb)
- Related to `deque`, thank you to @mratford for introducing me to the idea of using a dictionary as a linked list (`[a,b,c]` becomes `{a: b, b:c, c:a}`)
- Complex numbers are useful for coordinates and vector geometry (see [Day 12](https://github.com/samnlindsay/advent_of_code/blob/main/Day12-RainRisk.ipynb))
- **Classes** - I have a lot to learn! But `functools.cached_property` can be very useful to add the `@cached_property` decorator to class properties that are likely to be reused frequently (caching them rather than recalculating many times).
- `numpy` is a thing that is useful, and I should be far more aware of it than "_I bet `numpy` has a function for this..._"
- `append` vs `extend` - You can `list1.append(list2)` to add `list2` as a _single_ item to `list1`, or `list1.extend(list2)` to add _each element_ of `list1` to `list2`. 
