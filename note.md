# Minimap2-GPU notes

## profiling result

pipeline:

* chaining
* collect-seed-hits
* extension

**Dataset: SRR9190254**

**Reference: GRCh38 (hg38)**

| simd   | hotspot           | time | threads    | total runtime |
| ------ | ----------------- | ---- | ---------- | ------------- |  
| sse    | extension         | 50%  | default(3) |     481s      |
| sse    | collect-seed-hits | 22%  | default(3) |     481s      |
| sse    | chaining          | 8%   | default(3) |     481s      |
| avx512 | extension         | 37%  | default(3) |     387s      |
| avx512 | collect-seed-hits | 33%  | default(3) |     387s      |
| avx512 | chaining          | 10%  | default(3) |     387s      |

```flow
st=>start
th=>operation: thread task assignment
oth=>operation: other work
cm=>operation: collect minimizer 
csh=>operation: collect seed hits
ca=>operation: chaining
al=>operation: align_regs
e=>end

st->th
th->oth->e
th->cm->csh->ca->al->e
```
