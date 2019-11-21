# Triangle Counting Benchmark V2
## Baseline

| dataset                   | Max NodeId  | claimed edges | N(V)      | N(E)          | N(T)              |
| ------------------------- | ----------- | ------------- | --------- |-------------- | ----------------- |
| soc-LiveJournal1.bin      | 4,847,571   | 68,993,773    | 4,847,571 | 42,851,237    | 285,730,264       |
| s24.kron.edgelist.bin     | 16,777,216  | 268,435,456   | 8,871,830 | 260,379,850   | 10,286,638,314    |
| s28.e15.kron.edgelist.bin | 268,435,456 | 4,026,531,840 |           | 3,973,862,397 | 199,196,078,202   |
| s29.e10.kron.edgelist.bin | 536,870,909 | 5,368,709,120 |           | 5,333,466,522 | 164,015,236,714   |

The homepage of LiveJournal dataset is hosted at [stanford](https://snap.stanford.edu/data/soc-LiveJournal1.html), both datasets are temporarily accessible at [LiveJournal1](http://datafountain.int-yt.com/BDCI2019/FeiMa/soc-LiveJournal1.bin) and [s24-kron](http://datafountain.int-yt.com/BDCI2019/FeiMa/s24.kron.edgelist.bin). These temporary data download links may be invalid. Notice that the record may have self looped edges and some edge occurs twice in the form (u, v) and (v, u) but some occurs only once. These details need some preprocessing task. Also the label of the node may not be continuous from 0 to |V| -1. Some mapping conversion is necessary.

These results are obtained on a Ubuntu server with 32 CPU cores of Intel(R) Xeon(R) CPU E5-2620 v4 @ 2.10GHz.

| dataset | method                     | times(s) |
| ------- | -------------------------- | -------- |
| journal | single threaded node_first | 63       |
| journal | single threaded edge_first | 610      |
| journal | 32 threads node_first      | 15       |
| journal | 32 threads edge_first      | 102      |
| kron    | single threaded node_first | 16567    |

## History

Originally, [TrCounting Benchmark](https://github.com/zhaofeng-shu33/triangle_counting_benchmark) is used.
However, there is an mistake about putting a large file in Git LFS. This makes cloning and updating 
repository much more difficult as it requires Git plugins. Also, the free limit is only 1.0GB per month for download 
usage. It means only 5 cloning of the original repository is possible. Therefore, the original repository is abandoned.

### About Kronecker graph dataset
These are artificial dataset used to model the social network. 
See [wiki](https://en.wikipedia.org/wiki/Kronecker_graph) for detailed explanation. [There](https://github.com/snap-stanford/snap/tree/master/examples/krongen) is a generator in C++, which uses a 2 times 2 matrix as a base graph.
The generated graph has 2^n nodes, as shown by the filename s24, s28 and s29. Also e15 means the number of edges is simply 15 times of the number of node. Maybe the generation process is run 15 times and the generated results are concatenated together.

There is [another repository](http://github.com/graph500/graph500) which could generate kronecker graph using a 2 times 2 matrix. 
There is no executable to generate the graph directly in the latest release. If you need one, you can download [2.1.4](https://github.com/graph500/graph500/tree/graph500-2.1.4) from the release page. The node id is saved in `int64_t`.
