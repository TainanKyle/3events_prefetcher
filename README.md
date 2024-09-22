# Enhancing Bingo Prefetcher Performance

### Introduction
This project focuses on enhancing the performance of the Bingo Prefetcher, which aims to improve cache memory
efficiency. We identified two key issues in Bingo for improvement: multiple matches in short event lookups and limited match
probability due to reliance on only two events. To address these issues, we proposed two design improvements: Global Match
and Three Events. The Global Match model adjusts the prefetch decision threshold to a global percentage across the entire
history table rather than a local percentage within a matching set. The Three Events model introduces an additional event,
‘PC’, to enhance match probability.

Our evaluations demonstrate that while the Global Match approach did not yield performance improvements, our Three
Events model enhanced the Instruction Per Cycle (IPC) and hit rates in several test cases. These findings suggest that
incorporating an additional event can substantially improve the efficiency and effectiveness of prefetching strategies in cache
memory systems.

### Proposal
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


