curry
=====

.. function:: template <class F> auto uncurry(F f)

    Adapts `f` into a function that takes its arguments from a pair/tuple.

    ::

        std::vector<int> a { 0, 42, 69 };
        std::vector<int> b { 18, 64, 69 };
        auto v = tl::views::zip(a,b) 
               | std::views::filter(tl::uncurry(std::ranges::equal_to{}))
               | tl::to<std::vector>();
        //v == {(69,69)}       

.. function:: template <class F> auto curry(F f)

    Adapts `f` from taking its arguments from a pair/tuple to one that takes its arguments directly.

    Mostly provided for symmetry with `tl::uncurry`, which is super useful.