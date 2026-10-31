<h1 align="center">vector.mq</h1>

Vector math and nearest-neighbour search for [mq](https://github.com/harehare/mq), as a module. Vectors are plain arrays of numbers.

## Installation

`vector.mq` imports [ds.mq](https://github.com/harehare/ds.mq) for its heap, which is included as a git submodule:

```sh
git clone --recurse-submodules https://github.com/harehare/vector.mq
```

Use it by adding both directories to the module path:

```sh
mq -L vector.mq -L vector.mq/vendor/ds.mq -I null 'import "vector" | vector::cosine([1, 0], [1, 1])'
```

## Usage

```sh
mq -L . -L vendor/ds.mq -I null '
  import "vector"
  | vector::nearest([1, 0], [[0, 1], [1, 0.1], [1, 1]], 2)
'
# [[0.9950371902099893, 1], [0.7071067811865475, 2]]
```

| Function | Description |
| --- | --- |
| `dot(a, b)` / `norm(a)` | dot product / Euclidean length |
| `add(a, b)` / `sub(a, b)` / `scale(a, k)` | element-wise arithmetic |
| `normalize(a)` | unit-length copy, the zero vector is returned as is |
| `cosine(a, b)` | cosine similarity, 0 when either vector is the zero vector |
| `euclidean(a, b)` | Euclidean distance |
| `mean(vectors)` | element-wise mean of a non-empty array of vectors |
| `nearest(query, vectors, k)` | the `k` most similar vectors as `[score, index]`, highest first |
| `nearest_by_distance(query, vectors, k)` | the `k` closest vectors as `[distance, index]`, closest first |

Vectors of different lengths are an error. Searching costs O(n log k) for `n` vectors.

## Development

```sh
git submodule update --init
mq-test -L vendor/ds.mq vector_tests.mq
```
