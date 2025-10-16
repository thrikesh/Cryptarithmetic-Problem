<h1>ExpNo 8 : Solve Cryptarithmetic Problem,a CSP(Constraint Satisfaction Problem) using Python</h1> 
<h3>Name: THRIKESWAR P        </h3>
<h3>Register Number: 212222230162      </h3>
<H3>Aim:</H3>
<p>
    To solve Cryptarithmetic Problem,a CSP(Constraint Satisfaction Problem) using Python
</p>
<h3>Procedure:</h3>
Input and Output
<br>Input:
This algorithm will take three words.
<br> B A S E<br>
    B A L L<br>
           ----------<br>
           G A M E S<br>

Output:
It will show which letter holds which number from 0 – 9.
For this case it is like this.

              B A S E                         2 4 6 1
              B A L L                         2 4 5 5
             ---------                       ---------
            G A M E S                       0 4 9 1 6
Algorithm
For this problem, we will define a node, which contains a letter and its corresponding values.<br>

isValid(nodeList, count, word1, word2, word3)<br>

Input − A list of nodes, the number of elements in the node list and three words.<br>

Output − True if the sum of the value for word1 and word2 is same as word3 value.<br>

Begin<br>
   m := 1<br>
   for each letter i from right to left of word1, do<br>
      ch := word1[i]<br>
      for all elements j in the nodeList, do<br>
         if nodeList[j].letter = ch, then<br>
            break<br>
      done<br>
      val1 := val1 + (m * nodeList[j].value)<br>
      m := m * 10<br>
   done<br>

   m := 1<br>
   for each letter i from right to left of word2, do<br>
      ch := word2[i]<br>
      for all elements j in the nodeList, do<br>
         if nodeList[j].letter = ch, then<br>
            break<br>
      done<br>

      val2 := val2 + (m * nodeList[j].value)
      m := m * 10
   done<br>

   m := 1<br>
   for each letter i from right to left of word3, do<br>
      ch := word3[i]<br>
      for all elements j in the nodeList, do<br>
         if nodeList[j].letter = ch, then<br>
            break<br>
      done<br>

      val3 := val3 + (m * nodeList[j].value)
      m := m * 10
   done<br>

   if val3 = (val1 + val2), then<br>
      return true<br>
   return false<br>
End<br>
<hr>

<h2>Program:</h2>

```
from itertools import permutations

def solve_cryptarithmetic(word1, word2, result):
    letters = set(word1 + word2 + result)
    if len(letters) > 10:
        return None
    
    first_letters = set([word1[0], word2[0], result[0]])
    
    for perm in permutations(range(10), len(letters)):
        mapping = dict(zip(letters, perm))
        
        if any(mapping[first] == 0 for first in first_letters):
            continue
            
        num1 = sum(mapping[ch] * (10 ** i) for i, ch in enumerate(word1[::-1]))
        num2 = sum(mapping[ch] * (10 ** i) for i, ch in enumerate(word2[::-1]))
        num3 = sum(mapping[ch] * (10 ** i) for i, ch in enumerate(result[::-1]))
        
        if num1 + num2 == num3:
            return mapping, num1, num2, num3
    
    return None

def print_solution(word1, word2, result, mapping, num1, num2, num3):
    print(f"{word1:>10} = {num1}")
    print(f"{word2:>10} = {num2}")
    print(f"{'':>10}---")
    print(f"{result:>10} = {num3}")
    print("\nLetter to Number Mapping:")
    for letter, number in sorted(mapping.items()):
        print(f"{letter} = {number}")

if __name__ == "__main__":
    word1 = "SEND"
    word2 = "MORE"
    result = "MONEY"
    
    solution = solve_cryptarithmetic(word1, word2, result)
    
    if solution:
        mapping, num1, num2, num3 = solution
        print_solution(word1, word2, result, mapping, num1, num2, num3)
    else:
        print("No solution found")
```

<h2>Sample Input and Output:</h2>
SEND = 9567<br>
MORE = 1085<br>
<hr>
MONEY = 10652<br>
<hr>
<img width="464" height="323" alt="image" src="https://github.com/user-attachments/assets/feab4a56-ad9b-4dfb-903f-1b36a8c2641a" />

<h2>Result:</h2>
<p> Thus a Cryptarithmetic Problem was solved using Python successfully</p>
