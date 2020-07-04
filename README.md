# Find median from data stream
## https://leetcode.com/problems/find-median-from-data-stream

# Implementation :
```java
class MedianFinder {
    PriorityQueue<Integer> minHeap;
    PriorityQueue<Integer> maxHeap;
    int minHeapSize, maxHeapSize;
    /** initialize your data structure here. */
    public MedianFinder() {
        minHeap = new PriorityQueue<>();
        maxHeap = new PriorityQueue<>((a,b) -> b - a);
    }
    
    public void addNum(int num) {
        if(minHeapSize == 0) {
            minHeap.add(num); minHeapSize++;
            return;
        }
        if(maxHeapSize == 0) {
            if(num < minHeap.peek()) {
                maxHeap.add(num);
            } else {
                maxHeap.add(minHeap.poll());
                minHeap.add(num);
            }
            maxHeapSize++;
            return;
        }
        if(num < minHeap.peek()) {
            maxHeap.add(num); maxHeapSize++;
        } else {
            minHeap.add(num); minHeapSize++;
        }
        balance();
    }
    
    private void balance() {
        if(Math.abs(maxHeapSize - minHeapSize) <= 1) return;
        
        if(maxHeapSize > minHeapSize) {
            minHeap.add(maxHeap.poll());
            maxHeapSize--; 
            minHeapSize++;
        } else {
            maxHeap.add(minHeap.poll());
            minHeapSize--;
            maxHeapSize++;
        }
            
    }
    
    public double findMedian() {
        if(maxHeapSize > minHeapSize) {
            return maxHeap.peek();
        } 
        if(minHeapSize > maxHeapSize) {
            return minHeap.peek();
        } else{
            return (maxHeap.peek() + minHeap.peek()) / 2.0;
        }
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
```

# References :
https://www.youtube.com/watch?v=TzkPMVoIgWM
https://www.youtube.com/watch?v=Z1ffjjh_xkY
