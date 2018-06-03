### 继承Collection接口
1.List
2.Set
3.Queue

### Map接口
1.HashMap实现原理
2.其它Map实现类

# List、Queue、Set、Map

# List
> ArrayList、LinkedList

> ArrayList 底层是数组存储元素  

> LinkedList 底层是链表存储元素  

##### ArrayList
get(int index) : O(1) <---  ArrayList<E>的主要优点
add(E element) : 基本是O(1) , 因为动态扩容的关系，最差时是 O(n) 
add(int index, E element) : 基本是O( n - index) , 要将index后面的元素一个一个往后移动位置，所以是O( n - index)

remove(int index) : O(n - index) (例如，移除最后一个元素，是 O(1))
Iterator.remove() : O(n - index)
ListIterator.add(E element) : O(n - index)


##### LinkedList
get(int index) : O(n)
add(E element) : O(1)
add(int index, E element) : O(n)
remove(int index) : O(n)
Iterator.remove() : O(1) <--- LinkedList<E>的主要优点
ListIterator.add(E element) is O(1) <---  LinkedList<E>的主要优点

LinkedList更适合从中间插入或者删除
ArrayList更适合检索和在末尾插入或删除（数组的特性）。




# Set
> HashSet、LinkedHashSet、TreeSet（SortSet）

Set不重复
HashSet中的元素是没有被排序
LinkedHashSet是用一个链表实现来扩展HashSet类，它支持对规则集内的元素排序
TreeSet是树形集是一个有序的Set，其底层是一颗树

# Queue
> Queue
接口Deque，是一个扩展自Queue的双端队列

# Map
> HashMap、TreeMap、ConcurrentHashMap

HashMap是无序
LinkedHashMap继承自HashMap，它主要是用链表实现来扩展HashMap类，HashMap中条目是没有顺序的，但是在LinkedHashMap中元素既可以按照它们插入图的顺序排序，也可以按它们最后一次被访问的顺序排序

TreeMap基于红黑树数据结构的实现，键值可以使用Comparable或Comparator接口来排序。TreeMap继承自AbstractMap，同时实现了接口NavigableMap，而接口NavigableMap则继承自SortedMap。SortedMap是Map的子接口，使用它可以确保图中的条目是排好序的。

