pipeable
========

.. var:: constexpr inline auto tl::pipeable

    .. function:: template <class F> constexpr auto operator()(F f) const

        Makes the given function pipeable to other functions and pipeable from ranges.

        ::

            range | pipeable(f); // equivalent to f(range)
            pipeable(f1) | pipeable(f2); // equivalent to compose(f2, f1)

        All range views in the `tl` namespace are already pipeable. This function is useful for adapting views from other libraries or the standard library. E.g.:

        ::

            auto enumerate_reverse = tl::views::enumerate | tl::pipeable(std::views::reverse);
            for (auto e : my_vec | enumerate_reverse) {
                //...
            } 