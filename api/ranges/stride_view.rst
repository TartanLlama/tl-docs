stride_view
===========

A view which walks over the given range with the given stride size.

::

  std::vector<int> v{ 0, 1, 2, 3, 4, 5, 6 };

  for (auto&& e : v | tl::views::stride(3)) {
    std::cout << e << ' ';
    //0 3 6
  }

.. class:: template <class V> class tl::stride_view

    **Requires:** `forward_range<V> && view<V>`.

    Reference: `range_reference_<V>`.

    Category: At most random-access.

    Sized: When `V` is sized, in which case the size is `(size(v) + stride_size - 1) / stride_size`.

    Common: When `V` is common and either it's sized or non-bidirectional.

    Const-iterable: When `V` is const-iterable.

    Borrowed: When `V` is borrowed.
    
    .. function:: stride_view(V range, F func)

.. var:: constexpr inline auto tl::views::stride

  .. function:: template <class V> constexpr auto operator()(V&& range, std::ranges::range_difference_t<V> n) const

    Constructs a `tl::stride_view<std::views::all_t<V>>`.

  .. function:: template <class V, class N> constexpr auto operator()(N n) const

    **Requires:** `std::integral<N>`.

    Partial application for piping, e.g. `range | tl::views::stride(size)`.