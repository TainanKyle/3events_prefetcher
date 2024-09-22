# Enhancing Bingo Prefetcher Performance - Three Events

### Introduction
This project focuses on enhancing the performance of the Bingo Prefetcher, which aims to improve cache memory
efficiency. We identified two key issues in Bingo for improvement: multiple matches in short event lookups and limited match
probability due to reliance on only two events. To address these issues, we proposed a design improvement: Three Events. The Three Events model introduces an additional event, ‘PC’, to enhance match probability.

Our evaluations demonstrate that our Three Events model enhanced the Instruction Per Cycle (IPC) and hit rates in several test cases. These findings suggest that
incorporating an additional event can substantially improve the efficiency and effectiveness of prefetching strategies in cache
memory systems.

### Method
To address the second problem of enhancing match probability for prefetching, we propose the Three Events model. This
design introduces an additional event, the program counter (PC), thereby expanding the number of events from two to three.
When no match is found using the original two events (PC+Address and PC+Offset), the model tests the same set again to find
a match using the PC event.

However, simply adding an event to the matching process is not sufficient. In Bingo, the history table is indexed using
PC+Offset. It would be inconsistent to determine the set by PC+Offset but then find matches within the set using only PC.
Therefore, we modified the history table to be indexed by PC. This change ensures that the set determination and matching
process are coherent.

It is important to note that this model might incur additional costs. In cases of a match failure, the additional event
comparison requires more time, potentially increasing latency. However, if this model effectively increases the match
probability and reduces cache misses, the overall performance improvement can outweigh these costs.

![image](https://github.com/user-attachments/assets/438342f7-d804-4c90-8535-84c133c5b38e)

### Result
For our model, 'Three Events', we observed improvements compared to Bingo. In both tracers, the Three Events
model achieved a higher IPC, indicating an overall improvement in processor performance. This enhancement is attributed to
an increased number of prefetch accesses and hits, which means that the prefetcher is effectively bringing more useful data
into the cache before it is needed. By prefetching more data that is actually used by the processor, the model reduces cache
misses, thus enhancing overall system performance.

Furthermore, despite the increased number of prefetch accesses, the Three Events model maintained a higher hit rate,
demonstrating the superior quality of its prefetching decisions. This indicates that the additional PC event in the Three Events
model effectively enhances the match probability and overall prefetching accuracy, leading to improved processor
performance and reduced cache misses.

The detailed results of these observations are presented in Table IV and Table V, which compare the IPC, prefetch
accesses, prefetch hits, and hit rates of the Three Events model against the original Bingo model. The tables illustrate the
performance gains achieved by implementing the Three Events model.

<img width="491" alt="image" src="https://github.com/user-attachments/assets/f9cdf6b3-4b46-440a-9583-09d133ecb559">

### Architecture
The 3rd Data Prefetching Championship (DPC3)

### Reference
Bakhshalipour, Mohammad, et al. "Bingo spatial data prefetcher." 2019 IEEE International Symposium on High
Performance Computer Architecture (HPCA). IEEE, 2019.
