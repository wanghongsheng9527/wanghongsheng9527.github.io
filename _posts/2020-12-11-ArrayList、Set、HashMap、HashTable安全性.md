## ArrayList线程不安全的表现

1.在多个线程进行add操作时可能会导致elementData数组越界。

2.一个线程的值覆盖另一个线程添加的值



### 问题解决

1.使用`Vector`（`ArrayList`所有方法加`synchronized`，太重）。

2.使用Collections.synchronizedList(new ArrayList<>())解决该问题

3.使用CopyOnWriteArrayList，读写分离，写入时复制

CopyOnWriteArrayList是JUC下的类





## Set线程不安全

跟List类似，`HashSet`和`TreeSet`都不是线程安全的，与之对应的有`CopyOnWriteSet`这个线程安全类。这个类底层维护了一个`CopyOnWriteArrayList`数组。



#### HashSet和HashMap

`HashSet`底层是用`HashMap`实现的。既然是用`HashMap`实现的，那`HashMap.put()`需要传**两个参数**，而`HashSet.add()`只**传一个参数**，这是为什么？实际上`HashSet.add()`就是调用的`HashMap.put()`，只不过**Value**被写死了，是一个`private static final Object`对象。





## Map线程不安全

`HashMap`不是线程安全的，`Hashtable`是线程安全的，但是跟`Vector`类似，太重量级。所以也有类似CopyOnWriteMap，只不过叫`ConcurrentHashMap`。