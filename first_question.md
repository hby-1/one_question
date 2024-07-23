# 数据流中的第K大元素
设计一个找到数据流中第 k 大元素的类（class）。注意是排序后的第 k 大元素，不是第 k 个不同的元素。

请实现 KthLargest 类：
- KthLargest(int k, int[] nums) 使用整数 k 和整数流 nums 初始化对象。
- int add(int val) 将 val 插入数据流 nums 后，返回当前数据流中第 k 大的元素。

### 示例：
**输入**:\
["KthLargest", "add", "add", "add", "add", "add"]
[[3, [4, 5, 8, 2]], [3], [5], [10], [9], [4]]

**输出**:
[null, 4, 5, 5, 8, 8]

----

**代码**:

1.

    public class KthLargest {
        int k;
        List<int> newNums=new List<int>{};
        public KthLargest(int k, int[] nums){
            this.k=k;
            foreach(int num in nums){
                this.newNums.Add(num);
            }
        }  
        public int Add(int val) { 
            newNums.Add(val);
            newNums.Sort();
            return newNums[newNums.Count-k];
        }
    }

2.

    public class KthLargest {
        private int k;
        private PriorityQueue<int, int> minHeap;
        public KthLargest(int k, int[] nums) {
            this.k = k;
            minHeap = new PriorityQueue<int, int>(Comparer<int>.Create((a, b) => a - b));
            foreach (int num in nums) {
                Add(num);
            }
        }
        public int Add(int val) {
            if (minHeap.Count < k) {
                minHeap.Enqueue(val, val);
            } else if (val > minHeap.Peek()) {
                minHeap.Dequeue();
                minHeap.Enqueue(val, val);
            }
            return minHeap.Peek();
        }
    }

3.

    public class KthLargest {
        int k;
        PriorityQueue<int, int> pq;
        public KthLargest(int k, int[] nums) {
            this.k = k;
            pq = new PriorityQueue<int, int>();
            int length = nums.Length;
            for (int i = 0; i < length; i++) {
                pq.Enqueue(nums[i], nums[i]);
                if (pq.Count > k) {
                    pq.Dequeue();
                }
            }
        }
        public int Add(int val) {
            pq.Enqueue(val, val);
            if (pq.Count > k) {
                pq.Dequeue();
            }
            return pq.Peek();
        }
    }




