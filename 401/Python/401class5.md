# Linked Lists
## What is a Linked List
- Linked List is a sequence of Nodes that are connected/linked to each other. Each Node references teh next Node in the link.
- There are two types of LL: Singly and Doubly.
## Terminology
- Linked List - a data structure that contains nodes that links to the next node in the list.
- Singly - refers to the number of references the node has. Singly means that there is only one reference, which points to the next node in the list.
- Doubly - refers to there being two (doubly) references within the node (next and previous nodes).
- Node - individual items/links that live in a linked list. Each node contains teh data for each link.
- Next - Each node contains a property called next, which contains a reference to the next node.
- Head - a reference of type Node to the frist node in a linked list.
- Current - a reference of type Node to the node that is currently being looked at. When traversing, you create a new (Current) variable at the Head to guarantee you are starting from the beginning of the linked list.

## Traversal
- You're not able to use a foreach or for loop when traversing a linked list.
- Next value guides where the next reference is pointing.
- While() loop is the best way to move through a linked list because it allows us to continually check that the Next node in the list is not null.
- Current variable tells us where exactly in the linked list we are and allows us to move forward util we hit the end.
ALGORITHM Includes (value)
// INPUT <-- integer value
// OUTPUT <-- boolean

  Current <-- Head

  WHILE Current is not NULL
    IF Current.Value is equal to value
      return TRUE

    Current <-- Current.Next

  return FALSE

1. Create Current at the Head to make sure we are starting from the beginning.
2. Create while loop which will only run if the node that Current is pointing towards isn't null.
3. Once in while loop, code checks if the value of the current node is equal to the value we are looking at.
4. If Current node does not contain the value, we must move Current to the next node that is being referenced.
5. Step 3 & 4 will continue until Current reaches the end of the LinkedList.
6. Once we hit the end, we know that we did not find the value and and return true at any point., so the value is not in the LinkedList. We return false.

## Traversal Big O
- Big O of time for Includes would be O(n) because at its worse case, the node we are looking for will be the very last node in teh list. N represents the number of nodes in the list.
- Big O of space for Includes would be O(1) because there is no additional space being used than what is already given to use with the linked list input.
- Big O notation is a way to evaluate the performance of an algorithm.
- The amount of time that a function, action or algo takes to run based on how many elements we pass to that function. Essentially, it's all about the way an algorithm grows when it runs.
- Regarding linked list, the two types of Big O equations to remember are O(1) and O(n).
- O(1) function takes constant time (doesn't matter how many elements or how big the input is): it'll always take the same amount of time and memory to run our algorithm.
- O(n) function is linear, which means that as our input grows, the space and time that we need to run that algo grow linearly.

# What's a Linked List?
- Linked Lists are linear data structures, which means that there is a sequence and an order to how they are constructed and traversed.

## Memory Management
- when we use arrays in our code, we are implementing a linear data structure.
- The biggest difference between arrays and linked list is the way that they use memory in our machines.
- when an array is created, it nees a certain amount of memory. 7 letters equals 7 bytes of memory to represent that array and it needs to be one contiguous block of bytes.
- linked list doesn't require 7 bytes of memory all in one place. It's dynamic.
- Arrays are static data structures, while linked list are dynamic data structures.
- A dynamic data structure can grow and shrink in memory and doesn't need a set amount of memory to be allocated in order to exist.

## Parts of a linked list
- Made up of a series of Nodes.
- The Head is the starting point/first node. 
- The end of the list isn't a node, but rather a node that points to null, or empty value.
- Node is comprised of just two parts: data, or teh information that the node contains, and a reference to the next node.
- A node only knows about what data is contains, and who its neighbor is.
- A node uses the "address" or reference to the next node to locate them in memory.


