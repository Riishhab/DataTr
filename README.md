from itertools import combinations

# Comparing a list of strings to find the number of common words.

# function to extract words from a string
def get_words(string):
  return set(string.lower().split())

def compare_strings(string_list): # list of strings as input 
    
    if len(string_list) < 2:
        raise ValueError("Provide a list with at least two strings to compare.")

    # combinations of string pairs
    pairs = combinations(enumerate(string_list, start=1), 2)

    # Comparing each pair
    result_lines = []
    for (i, str1), (j, str2) in pairs:
        words1 = get_words(str1)
        words2 = get_words(str2)
        count = len(words1.intersection(words2))
        result_lines.append(f"String {i} vs String {j} : {count}")

    return "\n".join(result_lines)

# main
strings = [
    "The quick brown fox jumps over the lazy dog",
    "The dog barked at the quick brown fox",
    "A lazy cat sleeps all day"
]

result = compare_strings(strings)
print(result)


str1 = "Hello St1 itrs tech"
str2 = "Hello St2 app dynamics tech"
str3 = "Hello St3 geneos by itrs tech"

print(str1)
print(str2)
print(str3)

str_list = [str1, str2, str3]

pairs = combinations(enumerate(str_list, start=1), 2)

print(list(pairs))

print(get_words(str1))

print(compare_strings(str_list))