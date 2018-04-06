# C++ port of https://github.com/mourner/flatbush

This is a straightforward port of https://github.com/mourner/flatbush.

To test: `clang++ --std=c++11 -Wall -O2 -o test test.cpp && ./test`

Note that this is actually a point index, so you are only guaranteed to
find an object when it's center lies inside the query box.

Example:
```cpp
flatbush::FlatBush<float> fb;
fb.Reserve(items.size()); // this is optional, to avoid heap allocs as the array grows during insertion
for (const auto& item: items) {
    fb.Add(item.MinX(), item.MinY(), item.MaxX(), item.MaxY());
}
fb.Finish();

// query
auto results = fb.Search(minx, miny, maxx, maxy);
// results are an array of indices. The index starts at zero, and is the order in which you inserted
// elements into the tree.
```
