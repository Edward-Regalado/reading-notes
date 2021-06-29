## List Comprehensions
- List compreshension always returns a result list.
- new_list = []
for i in old list:
    if filter(i):
        new_list.append(expressions(i))
new_list = [expression(i) for i in old_list if filter(i)]
- The list comprehension start with a [], square brackets.
- new_list: The new list (result)
- expression(i): Expression is based on the variable used for each element in the old list.
- for i in old_list: The word for followed by the variable name to use, followed by the work in the old list.
- if filter(i): Apply a filter with an if-statement.

## Create a simple list
- This is how you create a simple list: x = [i for i in range(10)]
print x [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
- squares = [] 
for x in range(10)
    squares.append(x**2)
    print squares
    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
- Or you can use list compreshensions to get the same result: squares = [x**2 for x in range(10)]

## Multiplying parts of a list
- list = [3, 4, 5]
multipled = [item*3 for item in list]
print multiplied [9, 12, 15]
- Note how the item*3 multiplied each piece by 3
- 