chunk_by_key_view
=================

A view which chunks a range into subranges where the consecutive elements share the same key given by a projection function.

::

    struct cat {
        std::string name;
        int age;
    };

    std::vector<cat> cats {
        {"potato", 12},
        {"bard", 12},
        {"soft boy", 9},
        {"vincent van catto", 12},
        {"oatmeal", 12},
    };

    for (auto&& group : cats | tl::views::chunk_by_key([](auto&& c) { return c.age; })) {
        //group 1 == { potato, bard }
        //group 2 == { soft boy }
        //group 3 == { vincent van catto, oatmeal }
    }

.. class:: template <class V, class F> class tl::chunk_by_key_view

    **Requires:** `forward_range<V> && view<V> && std::invocable<F, range_reference_t<V>>`

    Reference: `std::pair<invoke_result_t<F, range_reference_t<V>>, subrange<iterator_t<V>>>`

    Category: Forward.

    Sized: Never.

    Common: Never.

    Const-iterable: Never.

    Borrowed: Never.

    .. function:: chunk_by_key_view(V range, F func)

.. var:: constexpr inline auto tl::views::chunk_by_key

    .. function:: template <class V, class F> constexpr auto operator()(V&& range, F f) const

        Constructs a `tl::chunk_by_key_view<std::views::all_t<V>, F>`.

    .. function:: template <class V, class F> constexpr auto operator()(F f) const

        Partial application for piping, e.g. `ranges | tl::views::chunk_by_key(func)`.