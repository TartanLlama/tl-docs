enumerate_view
==============

A view which lets you iterate over the items in a range and their indices at the same time.

::

    std::vector<int> v;
    for (auto&& [index, item] : tl::views::enumerate(v)) {
        //...
    }
    for (auto&& [index, item] : tl::enumerate_view(v)) {
        //...
    }
    for (auto&& [index, item] : v | tl::views::enumerate) {
        //...
    }

.. class:: template <class V> class tl::enumerate_view

    **Requires:** `input_range<V> && view<V>`

    Reference: `std::pair<size_type, range_reference_t<V>>`

    Category: At most random-access.

    Sized: When `V` is sized.

    Common: When `V` is common.

    Const-iterable: When `V` is const-iterable.

    Borrowed: When `V` is borrowed.
    
    .. function:: enumerate_view(V range)

.. var:: constexpr inline auto tl::views::enumerate

  `tl::views::enumerate` is pipeable by itself, e.g. `range | tl::views::enumerate`.

    .. function:: template <class V> constexpr auto operator()(V&& range) const

        Constructs a `tl::enumerate_view<std::views::all_t<V>>`.