

### List
```py
--------------------------------------
# glist.sort()
# glist.reverse()
# sorted(glist)
# reversed(glist)
# glist.append(value)
# glist.extend(glist1)
# glist.pop(index)
# glist.remove(value)
# glist.insert(index,value)
# glist.index(value)
# glust.count(value)
# max(glist)
# min(glist)
# glist = [[0]*2]*2
# glist = [[0 for _ in range(m)] for _ in range(n)]
-------------------------------------

glist = [1,2,3,4,5]
glist = ['name','phone','address']

glist = [0,1,2,3,4,5]
glist[0]=0
glist.sort() #make glist sorted
glist.reverse() #make glist reversed
glist1 = sorted(glist) #return sorted list but not update glist
glist2 = list(reversed(glist))
max_glist = max(glist)
min_glist = min(glist)

glist.append(3)
glist.insert(0,5) #(index,value)
glist.pop() #remove and return last item
glist.pop(3) #(index)
glist.remove('raj') #(value) remove by value
del glist[3] #[index]

glist=[0,1,2,3,4,5]
glist[:] #[0,1,2,3,4,5]
glsit[:4] #[0,1,2,3]
glist[3:] #[3,4,5]
glist[1::2] #[1,3,5]
glist[::2] #[0,2,4]
glist[::-1] #[5,4,3,2,1,0]
glist[-1:1:-2]
```

### Set
```py
### Set
rset = {2,1,3,4,5,5} # {2,1,3,4,5} it avoid repetion

glist = [1,2,2,3,4]
rset = set(glist) # {1,2,3,4} 

gtuple = (3,2,3,4,1,3,5)
rset = set(gtuple) # {1,2,3,4,5}

rset.add(9)
rset.remove(9)
sorted(rset) # return sorted list

gset={1,2,3,4,5,6}
gset.pop() # return 1
gset.pop() # return 2
```

### String Formatting
```py
num=2
print(f"{num:05}") # 00002
print(f"{num:>5}") #'    2'
print(f"{num:<5}") #'2    '
print(f"{num:^5}") #'  2  '
print(f"{num:.2f}")# 2.00
print(f"{num:b}") # 10
print(f"{num:o}") # 2
print(f"{num:x}") # 2
print(f"{num:,}") # 2
print(f"{num:e}") # in exponential
```

### String Binary to int
```py
str_bin = "0101"
int_num = int(str_bin,2) #5

str_hex = "0xA"
num_hex = int(str_hex,16) #10
```

### char to int and int to char
```py
chr = 'a'
chr_num = ord(char) #97

chr = chr(98) #'b'
```

### math.ceil, math.floor
```py
math.ceil(5.5) #6
math.floor(5.5) #5
```
### LinkedList

```py
class Node:
    def __init__(self,value):
        self.value = value
        self.next = None

class LinkedList:
    def __init__(self,value):
        new_node = Node(value)
        self.head = new_node
        self.tail = new_node
        self.length = 1

    def show(self):
        temp = self.head
        while temp is not None:
            print(temp.value,end=" ")
            temp = temp.next
        
    def append(self,value):
        new_node = Node(value)
        if self.head == None:
            self.head = new_node
            self.tail = new_node
        else:
            self.tail.next = new_node
            self.tail = new_node
        
        self.length+=1
    
    def pop(self):
        if (self.length==0):
            return None
        pre = self.head
        temp = self.head

        while(temp.next):
            pre = temp
            temp = temp.next
        
        self.tail = pre
        self.tail.next = None
        self.length-=1
        
        if (self.length==0):
            pre = self.head
            self.head=None
            self.tail=None

            return pre.value
        return temp.value
    
    def prepend(self,value):
        new_node = Node(value)
        if (self.head==None):
            self.head = new_node
            self.tail = new_node
            return
        
        temp = self.head
        self.head = new_node
        new_node.next = temp
        self.length+=1

    def popFirst(self):
        if (self.head==None):
            return None
        temp = self.head
        self.head = self.head.next
        self.length-=1
        if (self.head==None):
            self.tail = None
            self.length = 0
        
        return temp.value
    
    def get(self,index):
        if index<0 or index>=self.length:
            return False
        temp = self.head

        for _ in range(index):
            temp = temp.next
        
        return temp
    
    def set(self,index,value):
        if index<0 or index>=self.length:
            return False
        temp = self.head

        for _ in range(index):
            temp = temp.next
        
        temp.value = value
        return True

    def insert(self,index,value):
        
        if index<0 or index>self.length:
            return False
        if (index==0):
            self.prepend(value)
        if (index==self.length):
            self.append(value)
        
        new_node = Node(value)
        temp = self.get(index-1)
        new_node.next = temp.next
        temp.next = new_node

    def remove(self,index):
        if (index<0 or index>=self.length):
            return False
        if (index==0):
            self.popFirst()
            self.length-=1
            return True
        if (index==self.length-1):
            self.pop()
            self.length=-1
            return True
        
        else:
            prev = self.get(index-1)
            temp = prev.next

            prev.next = temp.next
            temp.next = None

            self.length-=1

        return temp
    
    def reverse(self):
        temp = self.head
        self.head = self.tail
        self.tail = temp

        before = None
        after = temp.next

        for _ in range(self.length):
            after = temp.next
            temp.next = before
            before = temp
            temp = after
        
        return

    
my_linkedlist = LinkedList(5)
my_linkedlist.append(6)
my_linkedlist.append(7)
my_linkedlist.append(8)

my_linkedlist.reverse()
my_linkedlist.show()
```

#### DLL
```py
class Node:
    def __init__(self,value):
        self.value=value
        self.next=None
        self.prev=None

class DLL:
    def __init__(self,value):
        new_node = Node(value)
        self.head=new_node
        self.tail=new_node
        self.length=1

    def append(self,value):
        new_node = Node(value)
        if self.head is None:
            self.head = new_node
            self.tail = new_node
            self.length=1
            return True
        self.tail.next = new_node
        new_node.prev = self.tail
        self.tail = new_node
        self.length+=1
        return True
    
    def show(self):
        temp = self.head
        while temp is not None:
            print(temp.value,end=" ")
            temp=temp.next
        print()

    def pop(self):
        if (self.head is None):
            return False
        
        temp = self.tail
        
        if (self.length==1):
            self.head=None
            self.tail=None
            return temp
        
        self.tail = temp.prev
        self.tail.next = None
        temp.prev=None
        self.length-=1
        return temp
        
    def prepend(self,value):
        new_node = Node(value)
        if (self.length==0):
            self.head = new_node
            self.tail = new_node

        else:
            self.head.prev = new_node
            new_node.next = self.head
            self.head = new_node
        
        self.length+=1
        
        return self.head
    
    def popFirst(self):
        if (self.length==0):
            return False
        if (self.length==1):
            temp = self.head
            self.head = None
            self.tail = None
        else:
            temp = self.head
            self.head = temp.next
            self.head.prev = None
            temp.next = None

        self.length-=1
        return temp
    
    def get(self,index):
        if index<0 or index>self.length:
            return None
        else:
            temp = self.head
            for _ in range(index):
                temp=temp.next
            
            return temp
        
    def set_value(self,index,value):
        temp = self.get(index)
        temp.value = value

        return temp
    
    def insert(self,index,value):
        if (index<0 or index>self.length):
            return False
        
        if (index==0):
            self.prepend(value)
            self.length+=1
            return True
        if (index==self.length-1):
            self.append(value)
            self.length+=1
            return True
        
        new_node = Node(value)

        before = self.head
        after = self.head

        for _ in range(index):
            before=after
            after=after.next

        before.next = new_node
        new_node.prev = before
        after.prev = new_node
        new_node.next = after

        self.length+=1
        return True
    
    def remove(self,index):
        if (index<0 or index>self.length):
            return None
        if (index==0):
            return self.popFirst()
        if (index==self.length-1):
            return self.pop()
        
        temp = self.get(index)
        temp.prev.next = temp.next
        temp.next.prev = temp.prev
        temp.next = None
        temp.prev = None

        return temp
my_dll = DLL(20)
my_dll.append(30)
my_dll.append(40)
my_dll.append(50)

my_dll.insert(2,35)
print(my_dll.remove(2).value)

print("DLL:",end=" ")
my_dll.show()
```

#### Stack
```py
class Node:
    def __init__(self,value):
        self.value = value
        self.next = None

class Stack:
    def __init__(self,value):
        new_node = Node(value)
        self.top = new_node
        self.height=1

    def append(self,value):
        new_node = Node(value)
        if (self.top==None):
            self.top=new_node
            return True
        temp = self.top
        while temp.next is not None:
            temp=temp.next
        temp.next = new_node
        self.height+=1
        return True
    
    def push(self,value):
        new_node = Node(value)
        if (self.top is None):
            self.top=new_node
            self.height=1
            return True
        
        new_node.next = self.top
        self.top = new_node
        self.height+=1
        return True
    
    def pop(self):
        if self.height==0:
            return None
        
        temp = self.top
        self.top = temp.next
        temp.next = None
        self.height-=1

        return temp

    def show(self):
        temp = self.top
        while temp is not None:
            print(temp.value,end=" ")
            temp=temp.next
        print()
        return

my_stack = Stack(1)
my_stack.push(0)
my_stack.append(2)
my_stack.append(3)
my_stack.append(4)
print(my_stack.pop().value)

my_stack.show()
```

#### Queue
```py
class Node:
    def __init__(self,value):
        self.value=value
        self.next=None

class Queue:
    def __init__(self,value):
        new_node = Node(value)
        self.first=new_node
        self.last=new_node
        self.length=1

    def show(self):
        if (self.length==0):
            return False
        else:
            temp = self.first
            while temp is not None:
                print(temp.value,end=" ")
                temp=temp.next
            
            return
    
    def enqueue(self,value):
        if (self.length==0):
            return False
        else:
            new_node = Node(value)
            self.last.next=new_node
            self.last=new_node
            self.length+=1
    def dequeue(self):
        if(self.length==0):
            return None
        after = self.first
        before=None
        while after!=self.last:
            before=after
            after=after.next
        
        before.next=None
        self.last=before
        self.length-=1

        return after
my_queue=Queue(1)
my_queue.enqueue(2)
my_queue.enqueue(3)
# my_queue.enqueue(3)

my_queue.dequeue()
my_queue.show()
```

### HashTable
```py
class HashTable:
    def __init__(self,size=7):
        self.data_map=[None]*size

    def __hash(self,key):
        my_hash=0
        for letter in key:
            my_hash=(my_hash+ord(letter)*23)%len(self.data_map)
        return my_hash
    
    def show(self):
        for i,val in enumerate(self.data_map):
            print(i,": ",val)

    def set(self,key,value):
        index = self.__hash(key)
        if (self.data_map[index]==None):
            self.data_map[index]=[]
        self.data_map[index].append([key,value])
    
    def get(self,key):
        index=self.__hash(key)
        if (self.data_map[index] is not None):
            for i in range(len(self.data_map[index])):
                if self.data_map[index][i][0]==key:
                    return self.data_map[index][i][1]
            
            return None
    
    def keys(self):
        all_keys=[]
        for i in range(len(self.data_map)):
            if (self.data_map[i] is not None):
                for j in range(len(self.data_map[i])):
                    all_keys.append(self.data_map[i][j][0])
        
        return all_keys

my_hash=HashTable()
my_hash.set('rs',22)
my_hash.set('rsp',23)
my_hash.set('r',24)
my_hash.show()
print(my_hash.keys())
```
### Graph
```py
class Graph:
    def __init__(self):
        self.adj_list={}
    
    def add_vertex(self,vertex):
        if vertex not in self.adj_list.keys():
            self.adj_list[vertex]=[]
            return True
        return False
    
    def add_edge(self,v1,v2):
        if v1 in self.adj_list.keys() and v2 in self.adj_list.keys():
            self.adj_list[v1].append(v2)
            self.adj_list[v2].append(v1)
            return True
        return False
    
    def remove_edge(self,v1,v2):
        if v1 in self.adj_list.keys() and v2 in self.adj_list.keys():
            try:
                self.adj_list[v1].remove(v2)
                self.adj_list[v2].remove(v1)
            except ValueError:
                pass
            return True
        return False
    
    def remove_vertex(self,vertex):
        if vertex in self.adj_list:
            for other_vertex in self.adj_list[vertex]:
                self.adj_list[other_vertex].remove(vertex)
            del self.adj_list[vertex]

            return True
        return False

    
    def show_vertex(self):
        print(list(self.adj_list.keys()))
        print(self.adj_list)
    

    

my_graph=Graph()
my_graph.add_vertex('A')
my_graph.add_vertex('B')
my_graph.add_vertex('C')
my_graph.add_vertex('D')

my_graph.add_edge('A','B')
my_graph.remove_vertex('A')
my_graph.show_vertex()
```

### BST
```py
class Node:
    def __init__(self,value):
        self.value=value
        self.left=None
        self.right=None


class BST:
    def __init__(self):
        self.root=None
    
    def insert(self,value):
        new_node=Node(value)
        if self.root is None:
            self.root=new_node
            return True
        
        temp = self.root
        while True:
            if (new_node.value==temp.value):
                return False
            if (new_node.value<temp.value):
                if(temp.left is None):
                    temp.left = new_node
                    return True
                temp=temp.left
            if(new_node.value>temp.value):
                if(temp.right is None):
                    temp.right=new_node
                    return True
                temp=temp.right
                return True
    
    def contains(self,value):
        if (self.root is None):
            return False
        
        temp = self.root
        while True:
            if (value==temp.value):
                return True
            elif (value<temp.value):
                if (temp.left is None):
                    return False
                temp=temp.left
            elif (value>temp.value):
                if (temp.right is None):
                    return False
                temp=temp.right


bst = BST()
bst.insert(5)
bst.insert(4)
bst.insert(6)
bst.insert(3)

if (bst.contains(7)):
    print('it is containing')
else:
    print('it is not containing')

```

#### BFS
Breadth First Search
```py
def bfs(self):
        result=[]
        queue=[]
        currentNode = self.root
        queue.append(currentNode)

        while queue:
            currentNode=queue.pop(0)
            result.append(currentNode.value)
            if currentNode.left is not None:
                queue.append(currentNode.left)
            if currentNode.right is not None:
                queue.append(currentNode.right)

        
        return result
```

#### DFS
	##### PreOrder
```py
def pre_order(self):
        result=[]
        currentNode = self.root

        def traverse(currentNode):
            result.append(currentNode.value)
            if currentNode.left != None:
                traverse(currentNode.left)
            if currentNode.right !=None:
                traverse(currentNode.right)

        traverse(currentNode)
        return result
```

##### InOrder
```py
def in_order(self):
        result=[]
        currentNode = self.root

        def traverse(currentNode):
            if currentNode.left != None:
                traverse(currentNode.left)
            
            result.append(currentNode.value)
            if currentNode.right !=None:
                traverse(currentNode.right)

        traverse(currentNode)
        return result
```

##### PostOrder
```py
def post_order(self):
        result=[]
        currentNode = self.root

        def traverse(currentNode):
            if currentNode.left != None:
                traverse(currentNode.left)
            
            if currentNode.right !=None:
                traverse(currentNode.right)
            
            result.append(currentNode.value)


        traverse(currentNode)
        return result
```

### Sorting Algorithm
#### Bubble Sort
```py
def bubble_sort(glist):
    l=0
    r=1
    len_list = len(glist)
    
    for _ in range(len_list):
        while r<len_list:
            if glist[l]>glist[r]:
                temp = glist[l]
                glist[l]=glist[r]
                glist[r]=temp
            l+=1
            r+=1
            
        l,r=0,1 
    return glist

print(bubble_sort([4,2,6,5,1,3]))
```

#### Selection Sort
```py
def selection_sort(glist):
    for l in range(len(glist)):
        min_index = l 
        min_value = glist[l]
        r=l+1
        while r<len(glist):
            if min_value>glist[r]:
                min_index=r 
                min_value=glist[r] 
            r+=1
        if l!=min_index:
            temp = glist[l]
            glist[l]=min_value
            glist[min_index]=temp
    
    return glist
```

#### Insertion Sort
```py
def insertion_sort(glist):
    prev,current=0,1
    for current in range(1,len(glist)):
        temp=current
        prev=current-1
        while glist[temp]<glist[prev] and prev>-1:
            temp_value = glist[temp]
            glist[temp]=glist[prev]
            glist[prev]=temp_value
            
            temp=prev
            prev=prev-1
    
    return glist
```

#### Merge Sort
```py
def merge(array1, array2):
    combined = []
    i = 0
    j = 0
    while i < len(array1) and j < len(array2):
        if array1[i] < array2[j]:
            combined.append(array1[i])
            i += 1
        else:
            combined.append(array2[j])
            j += 1
              
    while i < len(array1):
        combined.append(array1[i])
        i += 1

    while j < len(array2):
        combined.append(array2[j])
        j += 1

    return combined
    
def merge_sort(glist):
    if len(glist)==1:
        return glist
    
    mid_index = len(glist)//2
    left = merge_sort(glist[:mid_index])
    right = merge_sort(glist[mid_index:])
    
    return merge(left,right)
```


#### Quick Sort
```py
def swap(my_list, index1, index2):
    temp = my_list[index1]
    my_list[index1] = my_list[index2]
    my_list[index2] = temp


def pivot(my_list, pivot_index, end_index):
    swap_index = pivot_index

    for i in range(pivot_index+1, end_index+1):
        if my_list[i] < my_list[pivot_index]:
            swap_index += 1
            swap(my_list, swap_index, i)
    swap(my_list, pivot_index, swap_index)
    return swap_index


def quick_sort_helper(my_list,left,right):
    if (left<right):
        pivot_index = pivot(my_list,left,right)
        quick_sort_helper(my_list,left,pivot_index-1)
        quick_sort_helper(my_list,pivot_index+1,right)
    
    return my_list
    
    

def quick_sort(my_list):
    quick_sort_helper(my_list, 0, len(my_list)-1)
```

### Problems

`Omega Ω - Best Case`
`Theta Θ - Average Case`
`Omicron O - Worst Case`
#### `1[0]*1` Match Count
```py
g_str = "100010100a1"
validating = False
l = 0
count=0

while l<len(g_str):
    if validating:
        if g_str[l]=="0":
            l+=1
        elif g_str[l]=="1":
            count+=1
            l+=1
        else:
            validating=False
            l+=1
    
    else:
        if g_str[l]=="1":
            validating=True
            l+=1
        
        else:
            l+=1

print(count)
```

#### 5. Longest Palindromic Sub-sequence
```py
class Solution:
    def longestPalindrome(self, s: str) -> str:
	    l,r=0,0
        res=[]
        max_len=0

		# Odd Palindromic Sequence
        for i in range(len(s)):
            l=i
            r=l

            while l>=0 and r<len(s) and s[l]==s[r]:
                if (r-l+1)>max_len:
                    max_len = r-l+1
                    res = s[l:r+1]
                l-=1
                r+=1
                
		# Even Palindromic Sequence
        for i in range(len(s)):
            l=i
            r=l+1

            while l>=0 and r<len(s) and s[l]==s[r]:
                if (r-l+1)>max_len:
                    max_len = r-l+1
                    res = s[l:r+1]
                l-=1
                r+=1
            
        return "".join(res)
```
#### 35.Search Insert Position
```py
import math
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        first = 0
        last = len(nums)
        mid = 0

        while first<last:
            mid = math.ceil((first+last)//2)
            if nums[mid]==target:
                return mid
            elif nums[mid]<target and mid!=first:
                first = mid
            elif nums[mid]>target and mid!=last:
                last = mid
            
            elif nums[mid]<target:
                return mid+1
            
            elif nums[mid]>target:
                if mid==0:
                    return mid
                return mid-1
        
        if nums[mid]<target:
            return mid+1
            
        elif nums[mid]>target:
            if mid==0:
                return mid
            return mid-1
```

#### 55. Jump Game [link](https://leetcode.com/problems/jump-game/submissions/1419982470/)
```py
class Solution:
    def canJump(self, nums: List[int]) -> bool:
        goal=len(nums)-1
        for i in range(len(nums)-1,-1,-1):
            if i+nums[i]>=goal:
                goal=i
        if goal==0:
            return True
        return False
```


#### 167. Two Sum II - Input Array Is Sorted
```py
class Solution:
    def twoSum(self, numbers: List[int], target: int) -> List[int]:
        l=0
        r=len(numbers)-1

        while l<r:
            summ=numbers[l]+numbers[r]
            if summ<target:
                l+=1
            elif summ>target:
                r-=1
            else:
                return [l+1,r+1]
```
#### 189. Rotate Array
```py
class Solution:
    def rotate(self, nums: List[int], k: int) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        k=k%len(nums)
        result=[0]*len(nums)

        for i in range(len(nums)):
            result[(i+k)%(len(nums))]=nums[i]

        nums[:]=result

```

#### 303. Range Sum Query - Immutable
#prefix_sum
```py
class NumArray:

    def __init__(self, nums: List[int]):
        self.nums = nums
        prefix_sum = []
        for i in range(len(nums)):
            if i==0:
                prefix_sum.append(nums[i])
            else:
                prefix_sum.append(nums[i]+prefix_sum[i-1])
        
        self.prefix_sums = prefix_sum
        
    def sumRange(self, left: int, right: int) -> int:
        if (left-1)<0:
            return self.prefix_sums[right]
        else:
            return self.prefix_sums[right]-self.prefix_sums[left-1]
```

#### [525. Contiguous Array](https://leetcode.com/problems/contiguous-array/description/)
#prefix_sum

```py
class Solution:
    def findMaxLength(self, nums: List[int]) -> int:
        num_dic={}
        sum=0
        max_len = 0

        for i in range(len(nums)):
            num = nums[i]
            if num==0:
                num=-1
            sum+=num

            if sum==0:
                if max_len<i:
                    max_len=i+1

            elif sum in num_dic:
                j = num_dic[sum]
                length = i-j
                if max_len<length:
                    max_len = length
            else:
                num_dic[sum]=i
            
        return max_len
```
#### 539. Minimum Time Difference

```py
class Solution:
    def findMinDifference(self, timePoints: List[str]) -> int:
        def minute_converter(gstr):
            time_list=gstr.split(':')
            hh = int(time_list[0])
            mm = int(time_list[1])
            minutes = hh*60+mm
            return minutes
        
        min_minute_diff = 1440
        timePoints.sort()

        current = 0
        prev = len(timePoints)-1
        
        while current<len(timePoints):
            current_min = minute_converter(timePoints[current])
            prev_min = minute_converter(timePoints[prev])

            diff_min = current_min - prev_min 
            if diff_min<0:
                diff_min = -diff_min

            if min_minute_diff>diff_min:
                min_minute_diff = diff_min
            
            diff_min = 1440-diff_min

            if min_minute_diff>diff_min:
                min_minute_diff = diff_min

            prev = current
            current+=1
        
        return min_minute_diff
```

#### 560. Subarray Sum Equals K 
#prefix_sum 
```py
class Solution:
    def subarraySum(self, nums: List[int], k: int) -> int:
        sums_array={0:1}
        n=len(nums)
        l=0
        summ=0
        diff=0
        result=0

        while l<n:
            summ+=nums[l]
            diff = summ-k
            if diff in sums_array:
                result+=sums_array[diff]
            if summ in sums_array:
                sums_array[summ]+=1
            else:
                sums_array[summ]=1
            
            l+=1
        
        return result

```
#### [1072. Flip Columns For Maximum Number of Equal Rows](https://leetcode.com/problems/flip-columns-for-maximum-number-of-equal-rows/)
```py
class Solution:
    def maxEqualRowsAfterFlips(self, matrix: List[List[int]]) -> int:
        def nott(n):
            if n=='0':
                return '1'
            else:
                return '0'

        hash_table={}
        max_count = 0

        for row in matrix:
            if row[0]==0:
                roww = ''.join(map(nott,map(str,row)))
            else:
                roww = ''.join(map(str,row))
            
            if roww in hash_table:
                hash_table[roww]+=1
            else:
                hash_table[roww]=1
            
            if hash_table[roww]>max_count:
                max_count = hash_table[roww]

        return max_count
```
#### [1593. Split a String Into the Max Number of Unique Substrings](https://leetcode.com/problems/split-a-string-into-the-max-number-of-unique-substrings/)
```py
class Solution:
    def maxUniqueSplit(self, s: str) -> int:
        value_set=set()

        def maxUnique(s,value_set):
            maxm=0
            for i in range(1,len(s)+1):
                temp = s[0:i]
                
                if temp not in value_set:
                    value_set.add(temp)
                    maxm=max(maxm,maxUnique(s[i:],value_set)+1)
                    value_set.remove(temp)
            
            return maxm

        result = maxUnique(s,value_set)
        return result
```
#### 2220. Minimum Bit Flips to Convert Number
```py
class Solution:
    def minBitFlips(self, start: int, goal: int) -> int:
        xor_result = bin(start^goal)
        result = xor_result.count('1')
        return result
```

#### [2257. Count Unguarded Cells in the Grid](https://leetcode.com/problems/count-unguarded-cells-in-the-grid/)
```py
class Solution:
    def countUnguarded(self, m: int, n: int, guards: List[List[int]], walls: List[List[int]]) -> int:

        grid = [[0 for _ in range(n)] for _ in range(m)]

        for guard in guards:
            i,j = guard[0],guard[1]
            grid[i][j] = 2
        
        for wall in walls:
            i,j = wall[0],wall[1]
            grid[i][j] = 3

        for guard in guards:
            ii,jj = guard[0],guard[1]
            i,j = ii,jj

            # Up Guarding
            while i>0:
                i-=1
                if grid[i][j]!=2 and grid[i][j]!=3:
                    grid[i][j]=1

                else:
                    break

            # Down Guarding
            i,j = ii,jj
            while i<m-1:
                i+=1
            
                if grid[i][j]!=2 and grid[i][j]!=3:
                    grid[i][j]=1

                else:
                    break
            
            # Left Guarding
            i,j = ii,jj
            while j<n-1:
                j+=1
            
                if grid[i][j]!=2 and grid[i][j]!=3:
                    grid[i][j]=1

                else:
                    break
            
            # Right Guarding
            i,j = ii,jj
            while j>0:
                j-=1
            
                if grid[i][j]!=2 and grid[i][j]!=3:
                    grid[i][j]=1

                else:
                    break
        
        res = 0
        for i in range(m):
            for j in range(n):
                if grid[i][j]==0:
                    res+=1
        
        return res
       
        
```
#### [2583. Kth Largest Sum in a Binary Tree](https://leetcode.com/problems/kth-largest-sum-in-a-binary-tree/)
```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def kthLargestLevelSum(self, root: Optional[TreeNode], k: int) -> int:
        tree_queue=deque([root])
        sum_list=[]
        level_sum=0
        while len(tree_queue)!=0:
            qn = len(tree_queue)
            for i in range(qn):
                current_node = tree_queue.popleft()
                level_sum+=current_node.val
                if current_node.left!=None:
                    tree_queue.append(current_node.left)
                if current_node.right!=None:
                    tree_queue.append(current_node.right)
            
            sum_list.append(level_sum)
            level_sum=0
        
        sum_list.sort()
        sum_list.reverse()

        if k>len(sum_list):
            return -1
        else:
            return sum_list[k-1]
```
#### [2641. Cousins in Binary Tree II](https://leetcode.com/problems/cousins-in-binary-tree-ii/)
```py
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, val=0, left=None, right=None):
#         self.val = val
#         self.left = left
#         self.right = right
class Solution:
    def replaceValueInTree(self, root: Optional[TreeNode]) -> Optional[TreeNode]:
        level_sum=deque([])
        tree_queue=deque([root])


        while len(tree_queue)!=0:
            nq = len(tree_queue)
            summ=0
            for _ in range(nq):
                temp = tree_queue.popleft()
                summ+=temp.val

                if temp.left!=None:
                    tree_queue.append(temp.left)
                if temp.right!=None:
                    tree_queue.append(temp.right)
            level_sum.append(summ)
            summ=0
        
        tree_queue.append(root)
        level_sum.popleft()
        level_sum.append(0)
        root.val=0


        while len(tree_queue)!=0:
            nq=len(tree_queue)
            level_total=level_sum.popleft()

            for _ in range(nq):
                sib_sum=0
                temp = tree_queue.popleft()
                if temp.left !=None:
                    sib_sum+=temp.left.val
                if temp.right!=None:
                    sib_sum+=temp.right.val
                
                cousin_sum=level_total-sib_sum

                if temp.left!=None:
                    temp.left.val=cousin_sum
                    tree_queue.append(temp.left)
                if temp.right!=None:
                    temp.right.val=cousin_sum
                    tree_queue.append(temp.right)
                    
        return root
```

#### 2807. Insert GCD in LL
```py
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def insertGreatestCommonDivisors(self, head: Optional[ListNode]) -> Optional[ListNode]:
        def gcd(num1,num2):
            if num1>num2:
                x,y=num1,num2
            else:
                x,y=num2,num1
            while y!=0:
                x,y=y,x%y

            return x

        
        if head==None or head.next==None:
            return head
        
        l = head
        r = l.next

        while r!=None:
            gcd_val = gcd(l.val,r.val)
            gcd_node = ListNode(gcd_val)
            l.next = gcd_node
            gcd_node.next = r
            l=r
            r=r.next
        
        return head
```

#### 3043. Find the Length of the Longest Common Prefix

```py
class Solution:
    def longestCommonPrefix(self, arr1: List[int], arr2: List[int]) -> int:
        longest_prefix = 0
        num1_dic = {}

        for num1 in arr1:
            while num1!=0:
                num1_dic[num1] = True
                num1//=10
            
        
        for num2 in arr2:
            while num2!=0:
                if num2 in num1_dic:
                    length2 = len(str(num2))
                    if length2>longest_prefix:
                        longest_prefix=length2
                        break
                num2//=10

        return longest_prefix
```