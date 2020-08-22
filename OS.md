# OS 

## Stride 调度算法：

### 考题类型1:请描述stride调度算法的思路？stride算法的特征是什么？stride调度算法是如何避免stride溢出问题的？

思路：

- 每个进程有两个属性：
  - pass：当前位置
  - stride：一次要前进的步数
  - stride ∝ 1 / priority
- 选择进程的方法：
  - 执行当前pass最小的进程
  - 该进程的pass += stride
  - 重复该过程

特征：

- stride越小（优先级越高），被调度的次数会越多
- 基于优先级（priority-based）
- 调度选择是确定的（deterministic）

避免stride溢出的方法：

- uint32存储、int32相减比较
- 最大步进值-最小步进值<无符号整数/2
- 具体可参见Piazza帖子https://piazza.com/class/i5j09fnsl7k5x0?cid=357



### 考题类型2:在lab6中，我们实现了Stride Scheduling调度算法，并声称它对“进程的调度次数正比于其优先级”。对于优先级为2、3、5、7的4个进程，选取210为MAX_STRIDE，则：

1. 简要描述Stride Scheduling调度算法。
2. 四个进程的步长分别为：**、**、**、**。
3. 假设四个进程的初始stride值均为0，证明：总有一个时刻，四个进程的stride值都是210，且此时四个进程被调度的次数正比于其优先级。

答：

Stride调度算法：

- 每个进程有一个priority（优先级），pass和stride
- stride = BigStride / priority
- 每次调度时选择pass值最小的进程，更新该进程的pass：pass += stride

步长分别为105、70、42和30。

## 信号量

### 信号量的实现（P & V）

```c++
class semaphore {
  int sem;
  struct process *q;// wait queue
}

P(semaphore *S) {
  S->sem--;
  if(S->sem < 0) {
    add process to S->q
    block()
  }
}

V(semaphore *S) {
  S->sem++;
  if(S->sem <= 0) {
    remove a process P from S->q
    wakeup(P)
  }
}
```

这种实现方式没有忙等待的问题，sem为正时表示可用资源数，为负时表示等待队列中的进程数

### 生产者&消费者问题

```c++
// n 缓冲区个数
// mutex 缓冲池访问互斥
// empty 空的缓冲区数量
// full 满的缓冲区数量
int n;
semaphore mutex = 1;
semaphore empty = n;
semaphore full = 0;

// producer
do {
  // produce
  wait(empty);
  wait(mutex);
  // add product to the buffer
  signal(mutex)
  signal(full);
} while(true)
  
// consumer
do {
  wait(full);
  wait(mutex);
  // remove an item form buffer
  signal(mutex)
  signal(empty);
  //consume
} while(true)
```

### 读者&写者问题

```c++
// rw_mutex读者写者共用
// mutex保证更新变量read_count时互斥
semaphore rw_mutex = 1;
semaphore mutex = 1;
int read_count = 0;

// writer
do {
  wait(rw_mutex);
  // write
  signal(rw_mutex);
} while(true)

//reader
do {
  wait(mutex);
  read_count++;
  if(read_count == 1) 
    wait(rw_mutex);
  signal(mutex);
  // read 
  wait(mutex);
  read_count--;
  if(read_count == 0)
    signal(rw_mutex);
  signal(mutex);
} while(true)
```

这种实现中，作者可能饥饿 