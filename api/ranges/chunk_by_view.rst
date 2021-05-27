chunk_by_view
=============

A view which chunks a range into subranges where the consecutive elements satisfy a binary predicate.

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

  for (auto&& group : cats | tl::views::chunk_by([](auto&& left, auto&& right) { return left.age == right.age; })) {
    //group 1 == { potato, bard }
    //group 2 == { soft boy }
    //group 3 == { vincent van catto, oatmeal }
  }

.. class:: template <class V, class F> class tl::chunk_by_view

    **Requires:** `forward_range<V> && view<V> && std::predicate<F, range_reference_t<V>, range_reference_t<V>>`

    Reference: `subrange<iterator_t<V>>`
    
    Category: Forward.

    Sized: Never.

    Common: Never.

    Const-iterable: Never.

    Borrowed: Never.
    
    .. function:: chunk_by_view(V range, F func)

.. var:: constexpr inline auto tl::views::chunk_by

    .. function:: template <class V, class F> constexpr auto operator()(V&& range, F f) const

       Constructs a `tl::chunk_by_view<std::views::all_t<V>, F>`.

    .. function:: template <class V, class F> constexpr auto operator()(F f) const

        Partial application for piping, e.g. `ranges | tl::views::chunk_by(func)`.