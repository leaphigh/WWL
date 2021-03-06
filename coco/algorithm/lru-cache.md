```java
import java.util.HashMap;

class LRUCache {

    private HashMap<Integer, Slot> cache;
    private int updateSequence = Integer.MIN_VALUE;
    private final int capacity;

    public LRUCache(final int capacity) {
        this.capacity = capacity;
        this.cache = new HashMap<>(capacity);
    }
    
    public int get(final int key) {
        if (this.cache.containsKey(key)) {
            Slot slot = this.cache.get(key);
            slot.update(updateSequence++);
            return slot.getValue();
        }
        return -1;
    }
    
    public void put(final int key, final int value) {
        Slot slot = new Slot(value, updateSequence++);
        
        if (this.cache.containsKey(key)) {
            this.cache.replace(key, slot);
            return ;
        }
        
        if (this.cache.size() >= this.capacity) {
            evict();
        }

        this.cache.put(key, slot);
    }
    
    public void evict() {
        int targetKey = 0;
        int leastSequence = Integer.MAX_VALUE;
        
        for (Integer key : this.cache.keySet()) {
            int seqOfKey = this.cache.get(key).getSequence();
            if (leastSequence > seqOfKey) {
                leastSequence = seqOfKey;
                targetKey = key;
            }
        }
        
        this.cache.remove(targetKey);
    }
    
    
    private class Slot {
        private int value;
        private int seq;
        
        public Slot(final int value, final int seq) {
            this.value = value;
            this.seq = seq;
        }
        
        public int getValue() {
            return this.value;
        }
        
        public int getSequence() {
            return this.seq;
        }
        
        public void update(final int seq) {
            this.seq = seq;            
        }
    }
}
```