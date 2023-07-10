# Python-reversed-arguments
#It is a python code for reverse arguments
def reversed_args(f):
    def g(*args):
        return f(*args[::-1])
    return g

int_func_map = {
    'pow': pow,
    'cmp': lambda a, b: 0 if a == b else [1,-1][a < b],
}

string_func_map = {
    'join_with': lambda separator, *args: separator.join(args),
    'capitalize_first_and_join': lambda first, *args: ''.join([first.upper()] + list(args)),
}

queries = int(input())

output = []  # Store the output in a list

for _ in range(queries):
    line = input().split()
    func_name, args = line[0], line[1:]
    if func_name in int_func_map:
        args = list(map(int, args))
        result = reversed_args(int_func_map[func_name])(*args)
        output.append(str(result))  # Append the result as a string to the output list
    else:
        result = reversed_args(string_func_map[func_name])(*args)
        output.append(result)  # Append the result to the output list

# Print the output with the desired format
for item in output:
    print(item)

