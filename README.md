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

If you have a string named fish and then do list(fish) it will separate the name of the fish into separate pieces in a list
Works the same with changing it into an integer, int(fish), or a float, float(fish)
If you have a list you use ''.join(fish) to get it into a string from a list

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
______________________________________________________________________________________________________________________________________________________________________
Dictionary
romanNumerals = {'I':1,'V':5,'X':10,'L':50}
romanNumerals['X']
10
romanNumerals['C'] = 100
romanNumerals['C']
100

ord takes the string and finds the ordinal value, ex. a is 97 which can be translated into binary
The opposite of ord is chr ex. chr(97) = 'a'
msgbin = format(ord(msg), '0>8b')
      
______________________________________________________________________________________________________________________________________________________________________
Stego exercise

 def steg_encode_char(char, cover):
  6     charbin = format(ord(char),'0>8b')
  7     for i in range(0,len(cover)):
  8         coverbinl = list(format(int(cover[i]),'0>8b'))
  9         coverbinl[-1] = charbin[i]
 10         cover[i] = str(int(''.join(coverbinl),base = 2))
 11         
 12     pass
 13     
 14 def steg_decode_char(stego):
 15     msgbits = []
 16     for b in stego:
 17         msgbits.append(bin(int(b))[-1])
 18     return chr(int(''.join(msgbits),2))
 19     
 20     pass
 21 
 22 if __name__ == '__main__':
 23     pass

This was taking a binary and hiding it within 8 different binaries and breaks things into lists and puts them back together.

______________________________________________________________________________________________________________________________________________________________________




fp = open("test.txt")
fp.close()
with open("test.txt") as fp:
 1 with open('test.txt', 'w') as fp: 
 2     fp.write('first line\n')
with open('test.txt', 'r') as fp:
...     fp.read()
when using fp.read() it returns the characters as strings with no escape characters, so \n is just \n
when a number is used in fp.read(5) it returns 5 bytes of the file, a character is a byte so it will return the first 5 letters\
when using fp.readline() it returns a string, when using fp.readlines() it is returned as a list of strings
with open('test.txt') as fp:
...     for line in fp:
...             print(line,end='')
with this it opens up all of the lines with the newline breaks (\n) and opens as if you are using cat on the .txt file


______________________________________________________________________________________________________________________________________________________________________

file_io assignment



The textfile, travel_plans.txt, contains the summer travel plans for someone with some commentary. Find the total number of characters in the file and save to the variable num.

with open('travel_plans.txt', 'r') as fp:
    num = len(fp.read())

We have provided a file called emotion_words.txt that contains lines of words that describe emotions. Find the total number of words in the file and assign this value to the variable num_words.

with open('emotion_words.txt', 'r') as fp:
    strings = fp.readline()
    num_words = len(strings) - 6

    
    
______________________________________________________________________________________________________________________________________________________________________
