<!-- .slide: data-background="#111111" -->

# Set and multiset

<a href="https://coders.school">
    <img width="500" src="../img/coders_school_logo.png" alt="Coders School" class="plain">
</a>

___

## `std::set<K>` and `std::multiset<K>` traits

* <!-- .element: class="fragment fade-in" --> The same properties as <code>std::map&lt;K, V&gt;</code> and <code>std::multimap&lt;K, V&gt;</code>
* <!-- .element: class="fragment fade-in" --> The only difference is, that <code>set</code> and <code>multiset</code> hold only an ordered keys (not key-value pairs)
* <!-- .element: class="fragment fade-in" --> Perfect when you want to always have sorted values

If we do not want the container to be always sorted, it might be better to use <code>std::vector&lt;T&gt;</code> and sort it when necessary.
<!-- .element: class="fragment fade-in" -->

If we also care about unique values, we can use <code>std::unique()</code>
<!-- .element: class="fragment fade-in" -->

___

## `std::set<K>` and `std::multiset<K>` methods #1

[`std::set<K, T>` on cppreference.org](https://en.cppreference.com/w/cpp/container/set), [`std::multiset<K, T>` on cppreference.org](https://en.cppreference.com/w/cpp/container/multiset)

* <!-- .element: class="fragment fade-in" --> adding an item: <code>insert()</code>, <code>emplace()</code>, <code>emplace_hint()</code>
* <!-- .element: class="fragment fade-in" --> modifying / accessing an item: none
* <!-- .element: class="fragment fade-in" --> size / is the container empty: <code>size()</code>, <code>empty()</code>
* <!-- .element: class="fragment fade-in" --> clear unused memory: none
* <!-- .element: class="fragment fade-in" --> first / last item: none
* <!-- .element: class="fragment fade-in" --> start / end iterator: <code>begin()</code>, <code>end()</code>
* <!-- .element: class="fragment fade-in" --> reverse iterator: <code>rbegin()</code>, <code>rend()</code>

___

## `std::set<K>` and `std::multiset<K>` methods #2

* <!-- .element: class="fragment fade-in" --> constant iterator: <code>cbegin()</code>, <code>cend()</code>, <code>crbegin()</code>, <code>crend()</code>
* <!-- .element: class="fragment fade-in" --> clearing the container: <code>clear()</code>
* <!-- .element: class="fragment fade-in" --> preparing item for removal: none
* <!-- .element: class="fragment fade-in" --> erasing items from memory: <code>erase()</code>
* <!-- .element: class="fragment fade-in" --> replacement of the entire container: <code>swap()</code>
* <!-- .element: class="fragment fade-in" --> counting elements matching a given key: <code>count()</code> (returns only 0 or 1 for <code>map</code> or any positive number from 0 to n for <code>multimap</code>)
* <!-- .element: class="fragment fade-in" --> finding an element with a given key: <code>find()</code>
* <!-- .element: class="fragment fade-in" --> contains a given key (C++20): <code>contains()</code>

___

## Operations complexity

* Insertion/deletion
  * `O(log n)`
* Access
  * `O(log n)`
* Searching
  * `O(log n)`

___

## Memory usage

* `n * (sizeof(K) + 2 * sizeof(X*))`
* `O(n)`
* Additional small constant memory for internal data is used (root, compare, allocator)

___

## Iterator invalidation

* Adding, removing and moving the elements within the map or across several maps does not invalidate the iterators or references.
* An iterator is invalidated only when the corresponding element is deleted.

___

## Example of `std::set<K>` usage

```cpp
std::vector<int> v = {5, 4, 3, 2, 1, 0, 6, 8, 7};
std::set<int> set {v.begin(), v.end()};
for (const auto el : set) {
    std::cout << el << ' ';
}
std::cout << '\n';

std::set<int, std::greater<int>> set2 {v.begin(), v.end()};
for (const auto el : set2) {
    std::cout << el << ' ';
}
std::cout << '\n';
```
<!-- .element: class="fragment fade-in" -->

Output:
<!-- .element: class="fragment fade-in" -->

```cpp
0 1 2 3 4 5 6 7 8
8 7 6 5 4 3 2 1 0
```
<!-- .element: class="fragment fade-in" -->

___

## Example of `std::multiset<K>` usage

```cpp
std::vector<int> v = {5, 4, 3, 2, 1, 0, 6, 8, 7, 1, 2, 3, 4, 5, 6};
std::multiset<int> set {v.begin(), v.end()};
for (const auto el : set) {
    std::cout << el << ' ';
}
std::cout << '\n';

std::multiset<int, std::greater<int>> set2 {v.begin(), v.end()};
for (const auto el : set2) {
    std::cout << el << ' ';
}
std::cout << '\n';
```
<!-- .element: class="fragment fade-in" -->

Output:
<!-- .element: class="fragment fade-in" -->

```cpp
0 1 1 2 2 3 3 4 4 5 5 6 6 7 8
8 7 6 6 5 5 4 4 3 3 2 2 1 1 0
```
<!-- .element: class="fragment fade-in" -->