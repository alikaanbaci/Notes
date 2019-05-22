			
# TIME COMPLEXITY OF JAVA COLLECTIONS

|  **LISTS**| Add  |  Remove | Get | Contains | Data Structure
| -- | -- | -- | -- | -- |-- |
|  ArrayList| O(1) | O(n) | O(1) | O(n)|   Array|
|  LinkedList| O(1) | O(1) | O(n) | O(n)|   LinkedList|
|  CopyonWriteArrayList| O(n) | O(n) | O(1) | O(n)|   Array|

|  **SET**|	  **Add**  |  **Contains**| **Next**| **Data Structure**| 	
| -- | -- | -- | -- | -- |
|  HashSet|   O(1) | O(1) | O(h/n) | Hash Table| 
|  LinkedHashSet| O(1) | O(1) | O(1) | Hash Table + Linked List|
|  EnumSet| O(1) | O(1) | O(1) | Bit Vector| 
|  TreeSet| O(log n) | O(log n) | O(log n) | Red-black tree|   
|  CopyonWriteArraySet| O(n) | O(n) | O(1) | Array |
|  ConcurrentSkipList| O(log n) | O(log n) | O(1) | Skip List|

|  **MAP**|	  **Get**| **ContainsKey**| **Next**| **Data Structure**| 	 
| -- | -- | -- | -- | -- |
|  HashMap|   O(1) | O(1) | O(h/n) | Hash Table| 
|  LinkedHashMap| O(1) | O(1) | O(1) | Hash Table + Linked List|
|  IdentityHashMap| O(1) | O(1) | O(h/n) | Array| 
|  WeakHashMap| O(1) | O(1) | O(h/n) | Hash Table| 
|  EnumMap| O(1) | O(1) | O(1) | Array| 
|  TreeMap| O(log n) | O(log n) | O(log n) | Red-black tree|  
|  ConcurrentHashMap| O(1) | O(1) | O(h/n) | Hash Table|
|  ConcurrentSkipListMap| O(log n) | O(log n) | O(1) | Skip List|  


