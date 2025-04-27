---
description: An Extension to the Work of the Great Indian Mathematician Srinivasa Ramanujan Sir!!
category: Inventions
math: True
---

## Definition

`Any Number which can be expressed as a sum of multiple numbers (called contributors) raised to some power, in multiple ways is called as a Navam's Number!`

To understand the concept better, consider the Ramanujan's Number as an example:

$$1729 = (1)^3 + (12)^3 = (9)^3 + (10)^3$$

The Significance of the Number 1729 is that it is the smallest number which can be expressed as a sum of 2 cubes in 2 different ways. Hence, 1729 (Ramanujan's Number) is also a Navam's Number. In other words, Ramanujan's Numbers are a subset of Navam's Numbers.

## Atrributes of Navam's Number

### Contributors
* The numbers which are required to be raised to their powers and added to get a Navam's Number are called as the Contributors of that Navam's Number.
* For example, numbers 1, 9, 10, 12 are called the Contributors of the Ramanujan's Number.
* Remember, the Contributor must be a Natural Number!

### Exponent
* The Power of the Contributors is called as the Exponent.
* For example, number 3 is the exponent for the Ramanujan's Number.
* Remember, the Exponent must be a Whole Number!

### Term Count
* The minimum number of Contributors required to form a Navam's Number is known as the Term Count.
* For example, numbers 1 and 12 are enough to form Ramanujan's Number.
* So, the Number of Terms in Ramanujan's Number is 2.
* Remember, the Term Count must be a Natural Number!

### Parity
* The number of ways in which a Navam's Number can be expressed is called as the Parity of that Navam's Number.
* For example, 1729 can be expressed in 2 ways.
* So, the Parity of the Ramanujan's Number is 2.
* Remember, the Parity must be greater than 1!

## Python Code

Here is the python code to generate Navam's Numbers over a specific range. Make sure you install `pandas` library before you run it.

The first column in the output contains the Navam's Numbers.

```python
from itertools import combinations
import pandas as pd

def check_minmax(minimum: int, maximum: int) -> tuple:
    """Checks the validity of the range of the Contributors"""

    if minimum >= maximum:
        print('Maximum Number should be Greater than Minimum Number!')
        minimum = int(input('Enter the Valid Minimum Number: '))
        maximum = int(input('Enter the Valid Maximum Number: '))
        return check_minmax(minimum, maximum)
    return minimum, maximum

def check_expo(exponent: int) -> int:
    """Checks if the specified Exponent is valid"""

    if exponent < 0:
        print('Exponent must be a Whole Number!')
        exponent = int(input('Enter the Valid Exponent: '))
        return check_expo(exponent)
    return exponent

def check_term(term_count: int) -> int:
    """Checks if the specified Term Count is valid"""

    if term_count < 1:
        print('Number of Terms must be a Natural Number!')
        term_count = int(input('Enter the Valid Number of Terms: '))
        return check_term(term_count)
    return term_count

def check_parity(parity: int) -> int:
    """Checks if the specified Parity is valid"""

    if parity < 2:
        print('Parity must be Greater than 1!')
        parity = int(input('Enter the Valid Parity: '))
        return check_parity(parity)
    return parity

def main():
    """Prints Navam's Numbers with provided attributes"""

    mini = int(input('Enter the Minimum Number: '))
    maxi = int(input('Enter the Maximum Number: '))
    mini, maxi = check_minmax(mini, maxi)
    expo = int(input('Enter the Exponent: '))
    expo = check_expo(expo)
    term = int(input('Enter the Term Count: '))
    term = check_term(term)
    pari = int(input('Enter the Parity: '))
    pari = check_parity(pari)

    # Creating all the Possible Combinations with the numbers in the range of Contributors
    numbers_list = []
    contributors_list = []
    for contributors in combinations(range(mini, maxi + 1), term):
        contributors_list.append(contributors)
        number = 0
        for contributor in contributors:
            number += contributor ** expo
        numbers_list.append(number)

    # Extracting the Navam's Numbers from the Possible Combinations
    navams_numbers_list = []
    navams_numbers_contributors_list = []
    for index, number in enumerate(numbers_list):
        if numbers_list.count(number) >= pari:
            navams_numbers_list.append(number)
            navams_numbers_contributors_list.append(contributors_list[index])

    # Filtering out the non-duplicate Navam's Numbers along with their Contributors
    if navams_numbers_list:
        navams_numbers = {}
        for index, navams_number in enumerate(navams_numbers_list):
            if navams_number not in navams_numbers:
                navams_numbers[navams_number] = [navams_numbers_contributors_list[index]]
            elif len(navams_numbers[navams_number]) != pari:
                navams_numbers[navams_number].append(navams_numbers_contributors_list[index])
        df = pd.DataFrame(navams_numbers)
        print("\nThe Navam's Numbers are:")
        print(df.T.sort_index().to_string(header=False))
    else:
        print('There are no Navam\'s Numbers in the given Range of Contributors!')
```