transform_join
==============

Takes a function from `range_reference_t<Range>` to some `T` that models `range`. Transforms the given range by calling the function on each element, joining all `T`s into a single range.

::
   
   std::vector<int> vec{ 0,1,2 };
   auto f = [](auto i) { return std::vector<int>{i,i,i}; };

   for (auto&& e : vec | tl::views::transform_join(f)) {
      std::cout << e << ' ';
      //0 0 0 1 1 1 2 2 2
   }

`tl::transform_join_view` does not exist: `tl::views::transform_join` is implemented in terms of other range adaptors.

.. var:: constexpr inline auto tl::views::transform_join

    .. function:: template <class V, class F> constexpr auto operator()(V&& range, F f) const

        **Requires:** `viewable_range<V> && transformable_view<V, F> && (joinable_view<std::ranges::transform_view<std::views::all_t<V>, F>> || joinable_view<tl::cache_latest_view<std::ranges::transform_view<std::views::all_t<V>, F>>>)`

        The returned type has the following properties:

            Reference: `range_reference_t<range_reference_t<V>>`

            Category: At most bidirectional.

            Sized: Never.

            Common: When `V` is common and `range_reference_t<V>` is common.

            Const-iterable: Never.

            Borrowed: Never.

    .. function:: template <class V, class F> constexpr auto operator()(F f) const

        Partial application for piping, e.g. `ranges | tl::views::transform_join(func)`.