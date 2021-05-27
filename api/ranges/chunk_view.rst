chunk_view
==========

A view which chunks a range into subranges of the given size.

::

  std::vector<int> vec { 0,1,2,3,4,5,6,7,8,9,10 };

  for (auto&& group : vec | tl::views::chunk(4)) {
    std::cout << "Group: ";
    for (auto&& e : group) {
      std::cout << e << ' ';
    }
    std::cout << '\n';
  }
  //Group: 0 1 2 3
  //Group: 4 5 6 7
  //Group: 8 9 10

.. class:: template <class V> class tl::chunk_view

    **Requires:** `forward_range<V> && view<V>`.

    Reference: `subrange<iterator_t<V>>`.

    Category: At most random-access.

    Sized: When `V` is sized, in which case the size is `(size(v) + chunk_size - 1) / chunk_size`.

    Common: When `V` is common and either it's sized or non-bidirectional.

    Const-iterable: When `V` is const-iterable.

    Borrowed: When `V` is borrowed.
    
    .. function:: chunk_view(V range, F func)

.. var:: constexpr inline auto tl::views::chunk

  .. function:: template <class V> constexpr auto operator()(V&& range, std::ranges::range_difference_t<V> n) const

    Constructs a `tl::chunk_view<std::views::all_t<V>>`.

  .. function:: template <class V, class N> constexpr auto operator()(N n) const

    **Requires:** `std::integral<N>`.

    Partial application for piping, e.g. `range | tl::views::chunk(size)`.