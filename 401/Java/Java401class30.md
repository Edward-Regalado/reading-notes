# Basics of Hash Tables

- Hashing is a technique that is used to uniquely identify a specific object from a group of similar objects.
- In hashing, large keys are converted into small keys by using a hash function and the values are then stored in a data structure called a hash table.
- used to distribute entries (key/value paris) uniformly across an array.
- each element is assigned a key (converted key).
- can access elment using the key in O(1) time.
- element is comverted into an integer by using a hash function- this element can be used as an index to store the original element, which falls into the hash table.
- elment is stored in the hash table where it can be quickly retrieved using the hashed key.

## Hash Function

- any function that can be used to map a data set of an random size to a data set of a fixed size, which falls into th ehash table.
- values returned by a hash function are called hash values, hash codes, hash sums or simply hashes.
- to achieve a good hash function it must be easy to compute, uniform distribution and less collisions.

## Hash Table

- data structure used to store key/value pairs.
- uses a has function to compute an index into an array in which an element will be inserted or searched.
- average time to search for an element is O(1)

## Collision resolution techniques

- Seperate chaining (open hashing) is the most commonly used collision resolution techniques.
- implemented using linked list.
- each element of the hash table is a linked list and to store an element in the hash table you must insert it into a specific linked list.
- if there is any collision, then store both elements in the same linked list.
- chained hash tables are effectdive even when the number of table entries (N) is much higher than the number of slots.

```
implementation of hash tables with separate chaining (open hashing)

Assumption

Hash function will return an integer from 0 to 19.

vector <string> hashTable[20];
    int hashTableSize=20;
Insert

   void insert(string s)
    {
                // Compute the index using Hash Function
        int index = hashFunc(s);
        // Insert the element in the linked list at the particular index
        hashTable[index].push_back(s);
    }
Search

   void search(string s)
    {
        //Compute the index by using the hash function
        int index = hashFunc(s);
        //Search the linked list at that specific index
        for(int i = 0;i < hashTable[index].size();i++)
        {
            if(hashTable[index][i] == s)
            {
                cout << s << " is found!" << endl;
                return;
            }
        }
        cout << s << " is not found!" << endl;
    }

```

## Linear probing (open addressing or closed hashing)

- In open addressing, instead of linked list, all entry records are store in the array itself.
- when inserting, the hash index of the hashed value is computed and then the array is examined (starting with the hashed index).
- If the slot at the hashed index is unoccupied, then the entry is inserted in slot at the hashed inde, else it proceeds in some prob sequence util it finds an unoccupied slot.
- when searching, the array is scanned in the same sequence until either the target element is found or an unused slot is found- indicates that there is no such key in the table.


```
ash collision is resolved by open addressing with linear probing. Since CodeMonk and Hashing are hashed to the same index i.e. 2, store Hashing at 3 as the interval between successive probes is 1.

Implementation of hash table with linear probing

Assumption

There are no more than 20 elements in the data set.
Hash function will return an integer from 0 to 19.
Data set must have unique elements.
 string hashTable[21];
    int hashTableSize = 21;
Insert

void insert(string s)
    {
        //Compute the index using the hash function
        int index = hashFunc(s);
        //Search for an unused slot and if the index will exceed the hashTableSize then roll back
        while(hashTable[index] != "")
            index = (index + 1) % hashTableSize;
        hashTable[index] = s;
    }
Search

   void search(string s)
    {
        //Compute the index using the hash function
        int index = hashFunc(s);
         //Search for an unused slot and if the index will exceed the hashTableSize then roll back
        while(hashTable[index] != s and hashTable[index] != "")
            index = (index + 1) % hashTableSize;
        //Check if the element is present in the hash table
        if(hashTable[index] == s)
            cout << s << " is found!" << endl;
        else
            cout << s << " is not found!" << endl;
    }
```

## Quadratic Probing

- similar to linear probing and the only difference is the interval between successive probes or entry slots.
- when the slot at a hashed index for an entry record is already occupied, you must start traversing until you find an unoccupied slot.
- interval between slots is computed by adding the successive value of an arbitrary polynomial in the original hashed index.

```
mplementation of hash table with quadratic probing

Assumption

There are no more than 20 elements in the data set.
Hash function will return an integer from 0 to 19.
Data set must have unique elements.
string hashTable[21];
    int hashTableSize = 21;
Insert

   void insert(string s)
    {
        //Compute the index using the hash function
        int index = hashFunc(s);
        //Search for an unused slot and if the index will exceed the hashTableSize roll back
        int h = 1;
        while(hashTable[index] != "")
        {
            index = (index + h*h) % hashTableSize;
                 h++;
        }
        hashTable[index] = s;
    }
Search

void search(string s)
    {
        //Compute the index using the Hash Function
        int index = hashFunc(s);
         //Search for an unused slot and if the index will exceed the hashTableSize roll back
       int h = 1;
        while(hashTable[index] != s and hashTable[index] != "")
        {
            index = (index + h*h) % hashTableSize;
                 h++;
        }
        //Is the element present in the hash table
        if(hashTable[index] == s)
            cout << s << " is found!" << endl;
        else
            cout << s << " is not found!" << endl;
    }
```

## Double Hashing

- similar to linear probing, but the only difference is the interval between probs is computed by using two hash functions.

```
Implementation of hash table with double hashing

Assumption

There are no more than 20 elements in the data set.
Hash functions will return an integer from 0 to 19.
Data set must have unique elements.
    string hashTable[21];
    int hashTableSize = 21;
Insert

  void insert(string s)
    {
        //Compute the index using the hash function1
        int index = hashFunc1(s);
        int indexH = hashFunc2(s);
        //Search for an unused slot and if the index exceeds the hashTableSize roll back
        while(hashTable[index] != "")
            index = (index + indexH) % hashTableSize;
        hashTable[index] = s;
    }
Search

  void search(string s)
    {
        //Compute the index using the hash function
        int index = hashFunc1(s);
        int indexH = hashFunc2(s);
         //Search for an unused slot and if the index exceeds the hashTableSize roll back
        while(hashTable[index] != s and hashTable[index] != "")
            index = (index + indexH) % hashTableSize;
        //Is the element present in the hash table
        if(hashTable[index] == s)
            cout << s << " is found!" << endl;
        else
            cout << s << " is not found!" << endl;
    }
```

# Hash Table (Wiki)

- hash table (hash map) is a datastructure that implements an associatvie array abstract data type, a structure that can map keys to values.
- hash table uses a hash function to compute an index (hash code) into an array of buckets or slots, from which the desired value can be found.
- during lookup, the key is hashed and the resulting hash indicates where the corresponding value is stored.
- in the perfect world, the hash function will assign each key to a unique bucket, but most hash tables designs employ an imperfect hash function, which may cause collisions where the HF generates the same index for more than one key.

## Sources

[Hackerearth](https://www.hackerearth.com/practice/data-structures/hash-tables/basics-of-hash-tables/tutorial/)
[Wikipedia](https://en.wikipedia.org/wiki/Hash_table)
[Paul Programming](https://www.youtube.com/watch?v=MfhjkfocRR0)