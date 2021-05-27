transform_maybe_view
====================

Takes a function from `range_reference_t<Range>` to `optional<U>`. Transforms the given range by calling the function on each element, but only returning the value of engaged optionals.

::
   
   std::vector<int> vec{ 0,1,2,3,4 };
   auto f = [](auto i) { return (i % 2 == 0) ? std::optional(i / 2) : std::nullopt; };

   for (auto&& e : vec | tl::views::transform_maybe(f)) {
      std::cout << e << ' ';
      //0 1 2
   }


.. class:: template <class V, class F> class tl::transform_maybe_view

    **Requires:** `input_range<V> && view<V> && std::invocable<F, range_reference_t<V>>`

    Reference: `range_reference_t<V>::value_type&`

    Category: At most bidirectional.

    Sized: Never.

    Common: When `V` is common.

    Const-iterable: Never.

    Borrowed: Never.

    .. function:: transform_maybe_view(V range, F func)

.. var:: constexpr inline auto tl::views::transform_maybe

    .. function:: template <class V, class F> constexpr auto operator()(V&& range, F f) const

        Constructs a `tl::transform_maybe_view<std::views::all_t<V>, F>`.

    .. function:: template <class V, class F> constexpr auto operator()(F f) const

        Partial application for piping, e.g. `ranges | tl::views::transform_maybe(func)`.