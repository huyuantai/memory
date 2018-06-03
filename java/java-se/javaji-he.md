### 继承Collection接口
1.List
2.Set
3.Queue

### Map接口
1.HashMap实现原理
2.其它Map实现类

# List、Queue、Set、Map

List
> ArrayList、LinkedList

> ArrayList 底层是数组存储元素  

> LinkedList 底层是链表存储元素  

get(int index) : O(1) <---  ArrayList<E>的主要优点
add(E element) : 基本是O(1) , 因为动态扩容的关系，最差时是 O(n) 
add(int index, E element) : 基本是O( n - index) , 要将index后面的元素一个一个往后移动位置，所以是O( n - index)

remove(int index) : O(n - index) (例如，移除最后一个元素，是 O(1))
Iterator.remove() : O(n - index)
ListIterator.add(E element) : O(n - index)



Set
> HashSet、LinkedHashSet、TreeSet（SortSet）

Queue
> Queue

Map
> HashMap、TreeMap、ConcurrentHashMap

