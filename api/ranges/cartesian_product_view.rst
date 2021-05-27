cartesian_product_view
======================

A view representing the `cartesian product <https://en.wikipedia.org/wiki/Cartesian_product>`_ of any number of other views.

::
    
    std::vector<int> v { 0, 1, 2 };
    for (auto&& [a,b,c] : tl::views::cartesian_product(v, v, v)) {
        std::cout << a << ' ' << b << ' ' << c << '\n';
        //0 0 0
        //0 0 1
        //0 0 2
        //0 1 0
        //0 1 1
        //...
    }

.. class:: template <class... Vs> class tl::cartesian_product_view

    **Requires:** `((forward_range<Vs> && view<Vs>) && ...)`

    Reference: `std::tuple<range_reference_t<Vs>...>`

    Category: 
    
    - Random access if all `Vs` are random access, sized, and common.
    - Otherwise, bidirectional if all `Vs` are bidirectional and common.
    - Otherwise, forward.

    Sized: When all `Vs` are sized, in which case the product of their sizes.
    
    Common: When all `Vs` are common, or when all `Vs` are random-access and sized.

    Const-iterable: Always.

    Borrowed: Never.

    .. function:: cartesian_product_view(Vs... ranges)

.. var:: constexpr inline auto tl::views::cartesian_product

    `tl::views::cartesian_product` does not support partial application, e.g. `r1 | tl::views::cartesian_product(r2)` is invalid.

    .. function:: template <class V> constexpr auto operator()(Vs&&... ranges) const

        Constructs a `tl::cartesian_product_view<std::views::all_t<Vs>...>`.
 