# LRU


# LRU缓存实现

在计算机科学中，最近最少使用（LRU，Least Recently Used）算法是一种常见的页面替换算法，用以管理缓存。当缓存满时，该算法会优先淘汰最长时间未被使用的数据。本题解中，我们将探讨如何使用`Java`语言实现一个基于LRU算法的缓存系统。

## 题目分析

实现`LRUCache`类，它应该支持以下操作：

- `get(key)`：如果关键字`key`存在于缓存中，则返回`key`的值，否则返回-1。
- `put(key, value)`：如果关键字已经存在，则变更其数据值；如果关键字不存在，则插入该组`key-value`。当缓存容量达到上限时，它应该在写入新数据之前删除最久未使用的数据值，从而为新的数据值留出空间。

## 解题思路

要实现上述要求，我们可以利用`Java`中的`LinkedHashMap`类，该类内部通过双向链表维护元素的插入顺序，因此可以很自然地模拟LRU缓存的行为。

### 核心逻辑

1. **初始化**：通过指定容量`capacity`初始化LRU缓存。
2. **访问数据（get操作）**：若`key`存在，需要将其调整到双向链表的尾部，表示最近被访问过。
3. **写入数据（put操作）**：如果`key`已存在，更新其值并调整到双向链表的尾部。如果`key`不存在，先检查缓存是否已满。如果已满，删除链表头部的节点（最久未使用的数据），然后将新的`key-value`对插入到链表的尾部。

### 代码实现

```java
class LRUCache {
    int cap; // 缓存容量
    LinkedHashMap<Integer, Integer> cache = new LinkedHashMap<>();

    public LRUCache(int capacity) {
        this.cap = capacity;
    }
    
    public int get(int key) {
        if(!cache.containsKey(key)){
            return -1;
        }
        makeRecently(key);
        return cache.get(key);
    }
    
    public void put(int key, int value) {
        if(cache.containsKey(key)){
            cache.put(key, value);
            makeRecently(key);
            return;
        }

        if(cache.size() >= this.cap){
            int oldest = cache.keySet().iterator().next();
            cache.remove(oldest);
        }

        cache.put(key, value);
    }

    private void makeRecently(int key) {
        int val = cache.get(key);
        cache.remove(key);
        cache.put(key, val);
    }
}






