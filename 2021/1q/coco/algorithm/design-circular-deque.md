```java
class MyCircularDeque {

    private final int capacity;
    private int size;
    private Node front;
    private Node rear;
    
    public MyCircularDeque(int k) {
        this.capacity = k;
        this.size = 0;
    }
    
    private void initializeFirstNode(Node newNode) {
        this.front = newNode;
        this.rear = newNode;
    }
    
    public boolean insertFront(int value) {
        if (isFull()) {
            return false;
        }
        
        Node newNode = new Node(value);
        
        if (isEmpty()) {
            initializeFirstNode(newNode);
        } else {
            newNode.setNext(this.front);
            this.front.setPrev(newNode);
            this.front = newNode;
        }

        this.size++;
        
        return true;
    }
    
    public boolean insertLast(int value) {
        if (isFull()) {
            return false;
        }

        Node newNode = new Node(value);
        
        if (isEmpty()) {
            initializeFirstNode(newNode);
        } else {
            newNode.setPrev(this.rear);
            this.rear.setNext(newNode);
            this.rear = newNode;
        }

        this.size++;

        return true;
    }
    
    public boolean deleteFront() {
        if (isEmpty()) {
            return false;
        }
        
        this.front = this.front.getNext();
        this.size--;
        
        if (isEmpty()) {
            this.rear = null;
        }

        return true;
    }
    
    public boolean deleteLast() {
        if (isEmpty()) {
            return false;
        }
        
        this.rear = this.rear.getPrev();
        this.size--;
        
        if (isEmpty()) {
            this.front = null;
        }

        return true;
    }
    
    public int getFront() {
        return isEmpty() ? -1 : this.front.getValue();
    }
    
    public int getRear() {
        return isEmpty() ? -1 : this.rear.getValue();
    }
    
    public boolean isEmpty() {
        return (this.size == 0) ? true : false;
    }
    
    public boolean isFull() {
        return (this.size == this.capacity) ? true : false; 
    }
    
    private class Node {
        
        private final int value;
        private Node prev;
        private Node next;
        
        public Node(final int value) {
            this.value = value;
        }
        
        public void setPrev(final Node prev) {
            this.prev = prev;
        }
        
        public void setNext(final Node next) {
            this.next = next;
        }
        
        public Node getPrev() {
            return this.prev;
        }

        public Node getNext() {
            return this.next;
        }        

        public int getValue() {
            return this.value;
        }
    }
}
```