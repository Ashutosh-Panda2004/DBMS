**Introduction to Cache Replacement Policies:**

A cache is a smaller, faster memory component placed between a processor (or other hardware) and a larger, slower memory. Its purpose is to store a subset of data from the larger memory so that future requests for that data can be served more quickly. When the cache is full and a new item needs to be placed in it, the system must decide which existing item to evict. This decision is governed by the **cache replacement policy**.

There are several well-known cache replacement policies, each with its own strengths and weaknesses. The choice of a policy affects the cache’s hit rate and overall system performance.

Below, we will explain the most common cache replacement policies in detail and illustrate them with a step-by-step numerical example. We will consider a scenario where the cache can hold a certain limited number of blocks (or lines) and we have a sequence of memory references. For each policy, we will show how it decides which block to evict and how that affects hits and misses.

---

**Common Cache Replacement Policies:**

1. **First-In, First-Out (FIFO)**
2. **Least Recently Used (LRU)**
3. **Least Frequently Used (LFU)**
4. **Random Replacement**
5. **Optimal Replacement (Belady’s Algorithm)**

For simplicity, let’s assume:

- **Cache Size:** 3 blocks (the cache can hold 3 items at a time).
- **Reference String (Access Pattern):** 2, 3, 2, 1, 5, 2, 4, 2, 3, 2, 7
  - These are the memory block numbers requested in order.

We will walk through each policy with the same reference string and track cache states, hits, and misses.

---

### 1. First-In, First-Out (FIFO)

**Concept:**  
The oldest entry to enter the cache is the first to be replaced. This does not consider how recently or frequently a block was used. You literally queue the entries and when a new block must be added, you remove the block that has been in the cache the longest.

**Detailed Steps with the Example:**

- **Cache size:** 3 blocks
- **Initial Cache State:** Empty
- **Reference sequence:** 2, 3, 2, 1, 5, 2, 4, 2, 3, 2, 7

Let’s tabulate the process:

| Access | Action (FIFO)                                         | Cache State (after access) | Hit/Miss |
|---------|--------------------------------------------------------|-----------------------------|----------|
| 2       | Cache empty → insert 2                                 | [2, -, -]                  | Miss     |
| 3       | Cache has 2. Insert 3                                  | [2, 3, -]                  | Miss     |
| 2       | 2 is already in cache (first slot).                    | [2, 3, -]                  | **Hit**  |
| 1       | Cache full? Not yet (2 empty slots used?), we have 2 and 3, we add 1 → Actually we still have an empty slot, add 1 | [2, 3, 1]    | Miss     |
| 5       | Cache full now. Need to evict the oldest (FIFO: oldest is 2, it came first). Evict 2, insert 5 | [5, 3, 1]    | Miss     |
| 2       | Not in cache (5,3,1). Evict oldest: after last insertion, the queue of insertion was [2(old), 3, 1 → replaced 2 with 5, so oldest now is 3]. Actually, careful: The order of arrival: 2 (oldest), then 3, then 1. After we replaced 2 with 5, the order of arrival is 3 (oldest), 1 (middle), 5 (newest). Evict 3, insert 2 | [5, 1, 2]    | Miss     |
| 4       | Not in cache (5,1,2). Evict oldest: currently oldest is 1 (3 was evicted earlier, so order is now 1, then 5, then 2—need to track carefully. Let’s track insert order precisely:  
   - Insert order so far: Initially inserted 2, then 3, then 1. Evicted 2 and inserted 5 → now order is (3,1,5). Next evicted 3 for 2 → order is (1,5,2).  
   Evict oldest: oldest is 1. Insert 4. | [5, 2, 4] | Miss     |
| 2       | 2 is already in cache (5,2,4).                        | [5, 2, 4]                  | **Hit**  |
| 3       | Not in cache. Evict oldest: Current order after last insertion was (5,2,4). Oldest is 5. Evict 5, insert 3 | [3, 2, 4]    | Miss     |
| 2       | 2 is in cache.                                         | [3, 2, 4]                  | **Hit**  |
| 7       | Not in cache. Evict oldest: Current order (3,2,4), oldest is 2 because it was inserted earlier than 4 in this sequence? Careful: Let’s precisely track order after each insertion:  
   After inserting 4, order: (5,2,4) replaced 1. Actually, let’s freeze after each step:  
   - After inserting first three: (2,3,1)  
   - Insert 5 evicting 2: order now (3,1,5)  
   - Insert 2 evicting 3: order now (1,5,2)  
   - Insert 4 evicting 1: order now (5,2,4)  
   - Hit 2 does not change order. Still (5,2,4).  
   - Insert 3 evicting 5: order now (2,4,3)  
   - Hit 2 does not change order: (2,4,3)  
   Now we need to insert 7, evict oldest from (2,4,3). Oldest is 2. Insert 7 | [7, 4, 3] | Miss     |

**Counting Hits and Misses (FIFO):**  
- Misses: 2, 3, (2 was a hit), 1, 5, 2, 4, (2 was hit), 3, (2 hit), 7  
- Miss count: 2 (first), 3, 1, 5, 2 (second time), 4, 3 (again), 7 = 8 misses  
- Hits: Three times we accessed 2 where it was in cache: those are 3rd, 8th, and 10th accesses. Actually, the 3rd and 8th and 10th references were hits. So 3 hits.

---

### 2. Least Recently Used (LRU)

**Concept:**  
The block that has not been used for the longest time is the first to be replaced. This tries to keep recently accessed items in the cache, under the assumption that past recent access predicts near-future access.

**Detailed Steps with the Example:**

| Access | Action (LRU)                                              | Cache State (after) | Hit/Miss |
|---------|-----------------------------------------------------------|---------------------|----------|
| 2       | Cache empty, load 2                                       | [2, -, -]          | Miss     |
| 3       | Insert 3                                                  | [2, 3, -]          | Miss     |
| 2       | 2 is in cache, accessed recently now. Update LRU info.     | [2, 3, -]          | **Hit**  |
| 1       | Need to insert 1. There’s still space.                     | [2, 3, 1]          | Miss     |
| 5       | Cache full. Must evict LRU. Which is LRU? Access order so far: last used: just used 2 at third step, then loaded 1. The LRU is the one least recently used: After the third access (2), usage was 2(used on step 3), 3(used on step 2), 1(used on step 4). LRU is 3 because it was used least recently (at step 2, earlier than 2 at step 3 and 1 at step 4). Evict 3, insert 5. | [2, 5, 1] | Miss |
| 2       | 2 is in cache. Update usage.                              | [2, 5, 1]          | **Hit**  |
| 4       | Not in cache. Evict LRU. After last step usage:  
   - Step 5: used 5 newly, step 4: used 1, step 6: used 2.  
   Most recent uses: Step 6 used 2, Step 5 used 5, Step 4 used 1  
   LRU is 1. Evict 1, insert 4.                                      | [2, 5, 4]          | Miss     |
| 2       | 2 in cache. Update usage.                                 | [2, 5, 4]          | **Hit**  |
| 3       | Not in cache. Evict LRU. Recent uses: step 8 used 2, step 7 inserted 4 (used at step 7), step 5 inserted 5 (used at step 5). The oldest use among these is 5 (not used since step 5), then 4 was used at step 7, and 2 at step 8. LRU is 5. Evict 5, insert 3.  | [2, 3, 4] | Miss |
| 2       | 2 in cache. Hit.                                          | [2, 3, 4]          | **Hit**  |
| 7       | Not in cache. Evict LRU. Recent usage before this: step 10 used 2, step 9 inserted 3 (used at step 9), step 8 used 2 again and step 7 inserted 4. Actually, we need the most recent usage per block:  
   - 2 was just used at step 10 (very recent)  
   - 3 was used at step 9  
   - 4 was used at step 7  
   LRU is 4 (longest since last use). Evict 4, insert 7.             | [2, 3, 7]          | Miss     |

**Counting Hits and Misses (LRU):**  
- Misses on references: 2, 3, 1, 5, 4, 3, 7 = 7 misses  
- Hits on references: The hits occur for references 2 (3rd, 6th, 8th, 10th time we see 2) and that yields 4 hits. Actually let’s list hits accurately:  
  - 3rd access (2) - hit  
  - 6th access (2) - hit  
  - 8th access (2) - hit  
  - 10th access (2) - hit  
  That’s 4 hits.  
**Note:** The reference string had multiple 2’s: The first time we bring in 2 (miss), second time is at 3rd access (hit), 6th access (hit), 8th access (hit), 10th access (hit).

---

### 3. Least Frequently Used (LFU)

**Concept:**  
The block that has been used the fewest times overall is replaced first. Over time, each block accumulates a usage count. When a replacement is needed, the block with the lowest frequency count is evicted. If there’s a tie, some tie-breaker like LRU among the tied blocks is often used.

**Detailed Steps with the Example:**  
We must keep track of frequencies of each cached block.

| Access | Action (LFU)                                                 | Cache State (after)     | Frequency Counts                   | Hit/Miss |
|---------|--------------------------------------------------------------|-------------------------|------------------------------------|----------|
| 2       | Empty cache, insert 2                                        | [2, -, -]              | freq(2)=1                          | Miss     |
| 3       | Insert 3                                                     | [2, 3, -]              | freq(2)=1, freq(3)=1               | Miss     |
| 2       | 2 in cache, increment freq(2)                                | [2, 3, -]              | freq(2)=2, freq(3)=1               | **Hit**  |
| 1       | Insert 1 (still space)                                       | [2, 3, 1]              | freq(2)=2, freq(3)=1, freq(1)=1    | Miss     |
| 5       | Need to evict. Check frequencies: freq(2)=2, freq(3)=1, freq(1)=1. The lowest frequencies are for 3 and 1. Among them, evict the least recently used or just pick one (policy dependent). Commonly, LFU might evict the one that was used least recently among the LFU. Let’s say we break ties by LRU order:  
   - Access order so far: 2(last used at step 3), 3(last used at step 2), 1(last used at step 4). Among the lowest freq (3 and 1), both have freq=1, the older last use is 3 (used at step 2), so evict 3. Insert 5. | [2, 1, 5] | freq(2)=2, freq(1)=1, freq(5)=1 | Miss |
| 2       | 2 in cache, freq(2)=3 now                                    | [2, 1, 5]              | freq(2)=3, freq(1)=1, freq(5)=1    | **Hit**  |
| 4       | Need to evict: freq(2)=3, freq(1)=1, freq(5)=1. Lowest freq is (1 and 5). Between 1 and 5, 1 was used at step 4, 5 was used at step 5. LRU among these is 1 (used longer ago), evict 1. Insert 4. | [2, 4, 5] | freq(2)=3, freq(5)=1, freq(4)=1 | Miss |
| 2       | 2 in cache, freq(2)=4 now                                    | [2, 4, 5]              | freq(2)=4, freq(4)=1, freq(5)=1    | **Hit**  |
| 3       | Need to evict: freq(2)=4, freq(4)=1, freq(5)=1. Lowest freq is (4 and 5) both =1. Check who is older: 4 was inserted at step 7, 5 at step 5. Actually, after step 7 we inserted 4 (most recent among low freq?), 5 was used at step 5. The older usage is 5, so evict 5. Insert 3. | [2, 4, 3] | freq(2)=4, freq(4)=1, freq(3)=1 | Miss |
| 2       | 2 in cache, freq(2)=5                                        | [2, 4, 3]              | freq(2)=5, freq(4)=1, freq(3)=1    | **Hit**  |
| 7       | Need to evict: freq(2)=5, freq(4)=1, freq(3)=1. Lowest freq is (4 and 3). Among them, which is older? 4 inserted at step 7, 3 inserted at step 9. 4 is older. Evict 4, insert 7. | [2, 7, 3] | freq(2)=5, freq(3)=1, freq(7)=1 | Miss |

**Counting Hits and Misses (LFU):**  
- Misses: 2(first), 3, 1, 5, 4, 3(again), 7  
  That’s 7 misses.
- Hits: Every time we accessed 2 after the first miss was a hit. The sequence: 2 (miss), 3 (miss), 2 (hit), 1 (miss), 5 (miss), 2 (hit), 4 (miss), 2 (hit), 3 (miss), 2 (hit), 7 (miss)  
  Hits are on 3rd, 6th, 8th, 10th accesses: total 4 hits.

---

### 4. Random Replacement

**Concept:**  
When the cache is full and a new block must be inserted, choose a block at random to evict. This is simple to implement in hardware but does not usually yield as high a hit rate as more informed strategies.

**Detailed Steps with Example:**  
We will assume a random choice each time we need to evict. Let’s pick a plausible random outcome for demonstration purposes. (In reality, the block evicted would depend on some hardware-generated random number.)

| Access | Action (Random)                                      | Cache State (after)   | Hit/Miss |
|---------|-------------------------------------------------------|-----------------------|----------|
| 2       | Insert 2                                             | [2, -, -]            | Miss     |
| 3       | Insert 3                                             | [2, 3, -]            | Miss     |
| 2       | Already in cache                                      | [2, 3, -]            | Hit      |
| 1       | Insert 1                                              | [2, 3, 1]            | Miss     |
| 5       | Cache full, choose a victim randomly: suppose we evict 3 at random | [2, 5, 1] | Miss |
| 2       | In cache                                               | [2, 5, 1]            | Hit      |
| 4       | Need to evict randomly: suppose we evict 1             | [2, 5, 4]            | Miss     |
| 2       | In cache                                               | [2, 5, 4]            | Hit      |
| 3       | Evict randomly: suppose we evict 5                     | [2, 3, 4]            | Miss     |
| 2       | In cache                                               | [2, 3, 4]            | Hit      |
| 7       | Evict randomly: suppose we evict 4                     | [2, 3, 7]            | Miss     |

**Counting Hits and Misses (Random example):**  
- Misses: On references 2(first), 3, 1, 5, 4, 3(again), 7 = 7 misses  
- Hits: On references to 2 after first load = steps 3, 6, 8, 10 are hits: 4 hits.

Note: Actual results depend on the random choices made.

---

### 5. Optimal Replacement (Belady’s Algorithm)

**Concept:**  
This is a theoretical policy used for analysis. It evicts the block that will not be used for the longest time in the future. Since it requires future knowledge of the request sequence, it’s not implementable in real-time systems, but it’s useful as a benchmark to measure how other policies perform.

**Detailed Steps with the Example:**

Reference sequence: 2, 3, 2, 1, 5, 2, 4, 2, 3, 2, 7  
For each miss, we look ahead and see which cache block won’t be needed for the longest time and evict that one.

| Access | Future Accesses                 | Decision (Optimal)                         | Cache State (after) | Hit/Miss |
|---------|---------------------------------|---------------------------------------------|---------------------|----------|
| 2       | Future: 3,2,1,5,2,4,2,3,2,7     | Cache empty, just add 2                    | [2, -, -]          | Miss     |
| 3       | Future: 2,1,5,2,4,2,3,2,7       | Add 3                                      | [2, 3, -]          | Miss     |
| 2       | Future: 1,5,2,4,2,3,2,7         | 2 in cache                                 | [2, 3, -]          | Hit      |
| 1       | Future: 5,2,4,2,3,2,7           | Add 1 (still space)                        | [2, 3, 1]          | Miss     |
| 5       | Future: 2,4,2,3,2,7             | Need to evict someone. Current: [2,3,1]  
   Future use of these:
   - 2 appears at next step (imminent need)
   - 3 appears later at step: ... we see 3 at 9th access (farther down)
   - 1 appears nowhere else in the future (no future access to 1)
   Optimal evict: 1 (not used again)  
   Insert 5                                  | [2, 3, 5]          | Miss     |
| 2       | Future: 4,2,3,2,7               | 2 in cache          | [2, 3, 5]          | Hit      |
| 4       | Future: 2,3,2,7                 | Need to evict from [2,3,5]:
   Future uses:
   - 2 will appear at future steps
   - 3 will appear soon at step 9
   - 5 will appear… checking future: no 5 in future
   Evict 5. Insert 4                       | [2, 3, 4]          | Miss     |
| 2       | Future: 3,2,7                  | 2 in cache           | [2, 3, 4]          | Hit      |
| 3       | Future: 2,7                   | 3 in cache? Yes      | [2, 3, 4]          | Hit      |
| 2       | Future: 7                     | 2 in cache           | [2, 3, 4]          | Hit      |
| 7       | Future: none                  | Need to evict:
   Check [2,3,4]:
   Future use:
   - 2 no future uses
   - 3 no future uses
   - 4 no future uses
   Any can be evicted. Usually pick any since all are not needed again. Evict 4. Insert 7 | [2, 3, 7] | Miss |

**Counting Hits and Misses (Optimal):**  
- Misses: 2(first), 3, 1, 5, 4, 7 = 6 misses
- Hits: All other references are hits. We had a total of 11 accesses, 6 misses, so 5 hits.

This minimal number of misses proves that optimal is the best you can theoretically do for this sequence.

---

**Summary of Each Policy’s Key Idea and Result from Example:**

- **FIFO:** Evicts the oldest inserted block. Simple but doesn’t consider usage.  
  Misses: ~8 in this example.

- **LRU:** Evicts the block not used for the longest time. Very effective in practice.  
  Misses: ~7 in this example.

- **LFU:** Evicts the block with the fewest uses. Good if frequently used items are beneficial over time, but might suffer from “cold starts.”  
  Misses: ~7 in this example.

- **Random:** Evicts a random block. Easy to implement but not optimal.  
  Misses: ~7 in the chosen random scenario.

- **Optimal:** Evicts the block that won’t be used for the longest time in the future. Theoretically minimal misses but not practical without future knowledge.  
  Misses: ~6 in this example.

**Note:** Actual numbers can vary slightly with tie-breaking strategies and the exact reference string, but the general trends hold.

---

**Conclusion:**

Cache replacement policies guide which cache entry to remove when a new entry must be added to a full cache. Each has different logic:

- **FIFO**: Replace the oldest.
- **LRU**: Replace the least recently used.
- **LFU**: Replace the least frequently used.
- **Random**: Replace a random block.
- **Optimal**: Replace the one that will not be used for the longest time in the future (theoretical benchmark).

In real systems, LRU or approximations to LRU are common because they often perform well without requiring future knowledge.