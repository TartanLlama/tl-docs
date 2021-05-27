cycle_view
==========

Turns a view into an infinitely cycling one.

::

  std::vector<int> v { 0, 1, 2 };
  for (auto&& item : tl::views::cycle(v)) {
    std::cout << item << ' '; 
    //0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0...
  }

.. class:: template <class V> class tl::cycle_view

  **Requires:** `forward_range<V> && view<V>`

  Reference: `range_reference_t<V>`

  Category: 

  - Random-access if `V` is random-access and sized.
  - Otherwise, bidirectional if `V` is bidirectional and common.
  - Otherwise, forward.

  Sized: Never.

  Common: Never.

  Const-iterable: If `V` is const-iterable.

  Borrowed: Never.

.. var:: constexpr inline auto tl::views::cycle

  `tl::views::cycle` is pipeable by itself, e.g. `range | tl::views::cycle`.

  .. function:: template <class V> constexpr auto operator()(V&& v) const

    Constructs a `tl::cycle_view<std::views::all_t<V>>`.

