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
  num_read = fp.read()
  num_split = num_read.split()
  num_words = len(num_split)

  
Assign to the variable num_lines the number of lines in the file school_prompt.txt.

with open('school_prompt.txt', 'r') as fp:
    strings = fp.readlines()
    num_lines = len(strings)
OR
with open('school_prompt.txt', 'r') as fp:
    num_lines = len(fp.readlines())

Assign the first 30 characters of school_prompt.txt as a string to the variable beginning_chars.
with open('school_prompt.txt', 'r') as fp:
    beginning_chars = fp.read(30)

Using the file school_prompt.txt, assign the third word of every line to a list called three.
with open('school_prompt.txt', 'r') as fp:
    three = [line.split()[2] for line in fp]


Create a list called emotions that contains the first word of every line in emotion_words.txt.
with open('emotion_words.txt', 'r') as fp:
    emotions = [line.split()[0] for line in fp]
OR
three = []
with open('emotion_words.txt', 'r') as fp:
    for i in fp.readlines():
      three.append(i.split()[2])

Create a list called emotions that contains the first word of every line in emotion_words.txt.
with open('emotion_words.txt', 'r') as fp:
    emotions = [line.split()[0] for line in fp]
OR 
emotions = []
with open('emotion_words.txt', 'r') as fp:
    for line in fp.readlines:
      emotions.append(line.split()[0])

Assign the first 33 characters from the textfile, travel_plans.txt to the variable first_chars.
with open('travel_plans.txt', 'r') as fp:
          first_chars = fp.read(33)

Using the file school_prompt.txt, if the character ‘p’ is in a word, then add the word to a list called p_words.

p_words = []
with open('school_prompt.txt') as fp:
  lines = fp.read()
  for i in lines.split():
    if 'p' in i:
      p_words.append(i)
OR
p_words =[]
for line in fp:
  for word in line.split():
    if 'p' in word:
      p_words.append(word)
    
______________________________________________________________________________________________________________________________________________________________________


*args and **kwargs, these allow to have multiple values, such as a calculator, making it so you can add 4 different numbers together or more if you need
    


______________________________________________________________________________________________________________________________________________________________________

Practice Test

def q1(floatstr):
       '''
       TLO: 112-SCRPY002, LSA 3,4
       Given the floatstr, which is a comma separated string of
       floats, return a list with each of the floats in the 
       argument as elements in the list.
       '''
      newlist = []
      for y in floatstr.split(','):
        newlist.append(float(y))
      return newlist

      pass

      
def q2(*args):

  '''
  TLO: 112-SCRPY006, LSA 3
  TLO: 112-SCRPY007, LSA 4
  Given the variable length argument list, return the average
  of all the arguments as a float
  '''
  s = 0
  for arg in args:
    s += args
  return s/len(args)
  pass
OR 
return sum(args)/len(args)
  
def q3(lst,n):

  '''
  TLO: 112-SCRPY004, LSA 3
  Given a list (lst) and a number of items (n), return a new 
  list containing the last n entries in lst.
  '''
  return lst[-n:]

def q4(strng):
  '''
  TLO: 112-SCRPY004, LSA 1,2
  TLO: 112-SCRPY006, LSA 3
  Given an input string, return a list containing the ordinal numbers of 
  each character in the string in the order found in the input string
  '''
  newlist = []
  for i in list(strng):
    newlist.append(ord(i))
  return newlist
  pass
OR
  return [ord(x) for x in strng]

  def q5(strng):
'''
TLO: 112-SCRPY002, LSA 1,3
TLO: 112-SCRPY004, LSA 2
Given an input string, return a tuple with each element in the tuple
containing a single word from the input string in order.
'''
return tuple(strng.split())

 def q6(catalog, order):
      '''
      TLO: 112-SCRPY007, LSA 2
      Given a dictionary (catalog) whose keys are product names and values are product
      prices per unit and a list of tuples (order) of product names and quantities,
      compute and return the total value of the order.
  
      Example catalog:
      {
          'AMD Ryzen 5 5600X': 289.99,
          'Intel Core i9-9900K': 363.50,
          'AMD Ryzen 9 5900X': 569.99
      }
  
      Example order:
      [
          ('AMD Ryzen 5 5600X', 5), 
          ('Intel Core i9-9900K', 3)
      ]
  
      Example result:
      2540.45 
  
      How the above result was computed:
      (289.99 * 5) + (363.50 * 3)
      total = []
      for key in catalog:
          for item in order:
              if item[0] == key:
                  total.append(catalog[key] * item[1])
      return sum(total)

      OR

      total = 0
      for product,quantity in order:
        total += catalog[product] * quantity
      return sum(total)



def q7(filename):
     '''
     TLO: 112-SCRPY005, LSA 1
     Given a filename, open the file and return the length of the first line 
     in the file excluding the line terminator.
     '''
     with open(filename) as fp:
       x = fp.readline()
       y = len(x) - 1
       return y



 def q8(filename,lst):
     '''
     TLO: 112-SCRPY003, LSA 1
     TLO: 112-SCRPY004, LSA 1,2
     TLO: 112-SCRPY005, LSA 1
     Given a filename and a list, write each entry from the list to the file
     on separate lines until a case-insensitive entry of "stop" is found in 
     the list. If "stop" is not found in the list, write the entire list to 
     the file on separate lines.
     '''
    with open(filename, 'w') as fp:
      for item in lst:
        if item.lower() == 'stop':
          break
        fp.write(f'{item}\n')
    pass



 def q9(miltime):
     '''
     TLO: 112-SCRPY003, LSA 1
     Given the military time in the argument miltime, return a string 
     containing the greeting of the day.
     0300-1159 "Good Morning"
     1200-1559 "Good Afternoon"
     1600-2059 "Good Evening"
     2100-0259 "Good Night"
     '''
     if miltime >= 301 and miltime < 1200:
       return "Good Morning"
     elif miltime >= 1200 and miltime < 1600:
       return "Good Afternoon"
     elif >= 1600 and miltime < 2100:
       return "Good Evening"
     else:
       return "Good Night"

 def q10(numlist):
     '''
     TLO: 112-SCRPY003, LSA 1
     TLO: 112-SCRPY004, LSA 1
     Given the argument numlist as a list of numbers, return True if all 
     numbers in the list are NOT negative. If any numbers in the list are
     negative, return False.
     '''
     for i in numlist:
       if i < 0:
         return False
       return True

       
      





    
______________________________________________________________________________________________________________________________________________________________________




______________________________________________________________________________________________________________________________________________________________________

Practice Exam 2

def q1(sentence):
       '''
       Given a string of multiple words separated by single spaces,
       return a new string with the sentence reversed. The words
       themselves should remain as they are. For example, given
       'it is accepted as a masterpiece on strategy', the returned
       string should be 'strategy on masterpiece a as accepted is it'.
      '''
      sentenceG = sentence.split()
      sentenceT = sentenceG[::-1]
      sentenceF = ' '.join(sentenceT)
      return sentenceF
      pass
OR
      return ' '.join(reversed(sentence.split()))

def q2(n):
      '''
      Given a positive integer, return its string representation with
      commas seperating groups of 3 digits. For example, given 65535
      the returned string should be '65,535'.
      '''
      res = ('{:,}'.format(n))
      return res
      pass

def q3(lst0, lst1):
      '''
      Given two lists of integers, return a sorted list that contains
      all integers from both lists in descending order. For example,
      given [3,4,9] and [8,1,5] the returned list should be [9,8,5,4,3,1].
      The returned list may contain duplicates.
      '''
      lst = lst0 + lst1
      lst.sort(reverse=True)
      return lst
      pass
      
def q4(s1,s2,s3):
      '''
      Given 3 scores in the range [0-100] inclusive, return 'GO' if
      the average score is greater than 50. Otherwise return 'NOGO'.
      '''
      avg = (s1 + s2 + s3) / 3
      if avg >= 51:
          return('GO')
      else:
          return('NOGO')
      pass
  
def q5(integer, limit):
      '''
      Given an integer and limit, return a list of even multiples of the
      integer up to and including the limit. For example, if integer==3 and
      limit==30, the returned list should be [0,6,12,18,24,30]. Note, 0 is
      a multiple of any integer except 0 itself.
      '''
      return [n for n in range(0, limit+1) if n % integer == 0 and n % 2 == 0]

      OR

      multiples = []
      for i in range(0, limit+1):
          if i % integer == 0  and i % 2 == 0:
              multiples.append(i)
      return multiples

def q6(f0, f1):
      '''
      Given two filenames, return a list whose elements consist of line numbers
      for which the two files differ. The first line is considered line 0.
      '''
      diffs = []
      linenum = 0
      with open(f0) as fp0: 
         with open(f1) as fp1:
              lines0 = fp0.readlines()
              for i in fp1.readlines():
                  if i != lines0[linenum]:
                      diffs.append(linenum)
                  linenum += 1
      return diffs

      
      
      pass

 def q7(lst):
      '''
      Return the first duplicate value in the given list.
      For example, if given [5,7,9,1,3,7,9,5], the returned value should
      be 7.
      '''
      b=[]
      for i in range(len(lst)):
          if lst[i] in b:
              return(lst[i])
          elif lst[i] not in b and i == (len(lst)-1):
              return(-1)
          else:
              b.append(lst[i])
      pass

OR
      b = []
      for i in lst:
          if i in seen:
              return i
          else:
              seen.append

 def q8(strng):
      '''
      Given a sentence as a string with words being separated by a single space,
      return the length of the shortest word.
      '''
      shortest = min(strng.split(), key=len)
      return len(shortest)
      pass

 def q9(strng):
     '''
     Given an alphanumeric string, return the character whose ascii value
     is that of the integer represenation of all of the digits in the string
     concatenated in the order in which they appear. For example, given
     'hell9oworld7', the returned character should be 'a' which has
     the ascii value of 97.
     '''
     res = ''.join(filter(lambda i: i.isdigit(), strng))
     resT = chr(int(res))
     return resT
 
     pass

 def q10(arr):
     '''
     Given a list of positive integers sorted in ascending order, return
     the first non-consecutive value. If all values are consecutive, return
     None. For example, given [1,2,3,4,6,7], the returned value should be 6. 
     '''
     i = 1
     for x in arr:
         if i < len(arr) and arr[i] - arr[i-1] != 1:
             return arr[i]
         i += 1
     return None
 
     pass
OR

    for i in range(len(arr)):
        if (arr[i+1] - arr[i] != 1:
            return arr[i+1]
    return None


 
______________________________________________________________________________________________________________________________________________________________________

Test notes
format just a way to literally format a string to represent how we want it to look
'Hello. My name is {}.'.format('SSgt')
adding an f in front makes it so you can add format shorthand
given variables you can use it in format
i.e a = 'LCpl' and b = 'Lewis'
f'Hello, my name is {a} {b}.'
'Hello,  my name is LCpl Lewis.'
Remember the range command
Creates a range object but doesn't display it, to display it change it into a list
Split Join Split
ip = 192.168.0.10
octet = ip.split('.')
octet0 = octect[0]
octt0 = 192
READ THE FUCKING QUESTION
READ THE HANDBOOK AND OR NOTES NOT JUST THE BLOCKS OF CODE YOU GOOBER
