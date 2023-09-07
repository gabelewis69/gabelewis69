ssh to linux
ssh student@10.50.23.212 -X
-x is to have access to the linux apps, and password is password
Windoes is 10.50.33.144
To enter python it's python3
python --version

REPL

Read
Evaluate
Print
Loop 

clear is ctrl+L

You need to have () or a command will not work in Python

vim .vimrc

syntax enable
set tabstop=4
set shiftwidth=4
set expandtab
set number
filetype indent on
set autoindent

python3 is a way to test small portions of code, and DATATYPE is important
bool
int
float
str						'abc' * 5 = abcabcabcabcabc
tuple			A tuple is like a list and cannot be changed making it immutable making it more efficient
list			A list is mutable

id is a thing, it shows the id of the variable

if a bool is (), (None), (''), (0), ([]), (False). Then it is false, anything else being true.

str(c) makes c (which is 42 right now) into a string, returning a '42'. 
float(c) returns a 42.0

a = [1,2,3,4,5] is a list, changing the brackets to () creates a tuple
a.append(8) is how you append something to the end of a list or tuple, while del a[0] would delete the first of the list
another way to pull up indexes is by doing A[-1] which would bring up the last of the list while a[-2] will go to the one before, basically reading backwards
basic mathematical operations in the student guide

instead of b = b + 1 you can use b += 1
print('a: {} b:{}' .format(a, b))

string manipulation
using *variable*.split() you can split a string up by putting a delimiter in the () the default is space
you can treat a string as a list but it acts as a tuble, you can however turn another variable into a list of the string
l = list(s)
.join can combine different strings, ''.join(l)
we had made s into hello, after making l a list of s we then changed l[0] into j making it jello. Whatever is inside the '' of the .join is the delimiters

ACTIVITIES
cd
git clone https://git.cybbh.space/programming/python/public.git
SCRIPT
______________________________________________________________________________________________________________________________________________________________________
FIZZBUZZ
  1 #!/usr/bin/env python3
  2 
  3 a = 'Hello'
  4 print(a)  
    1 #!/usr/bin/env python3
  2 n = int(input('Enter a number: '))
  3 if n % 3 == 0 and n % 5 == 0:
  4     print ('fizzbuzz')
  5 elif n % 5 == 0:
  6     print ('buzz')
  7 elif n % 3 == 0:
  8     print ('fizz')
  9 else:
 10     print(n)
______________________________________________________________________________________________________________________________________________________________________

while statements, such as while Mr Mitchell was in Afghanistan he had created a Tiki Bar
while True: is an infinite loop

______________________________________________________________________________________________________________________________________________________________________

Guessing game
  1 #!/usr/bin/env python3
  2 
  3 def guess_number(n):
  4     while True:
  5         x = int(input ('Enter a number between 1 and 100: '))
  6         
  7         if x < n:
  8             print("too low")
  9             continue
 10         elif x > n:
 11             print("too high")
 12             continue
 13         if x == n:
 14             print ("WIN")
 15             break
 16     
 17 guess_number(23)
______________________________________________________________________________________________________________________________________________________________________

for range (start, stop, step)
if prime is a list then you can use [1:2:3] as a way to traverse the index with the same start stop step
slicing
For loops

when working with binary use format(a,'0>8b')

def invert(l):
    for n in range(0, len(l)):
        l[n] = str(255 - int(l[n]))
    Or
    counts = 0
    for num in l:
    l[counts] = str(255-int(num))
    counts += 1
    Or
    for count,numb in enumerate(l):
      l[count] = str(255-int(num))
  def inverted(l):
      result = []
      for n in range(0, len(l)):
      result.append(str(255 - int(l[n])))
      print(result)
      return result

      
