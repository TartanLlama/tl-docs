curry
=====

.. function:: template <class F> auto curry(F f)

    Adapts `f` into a function that takes its arguments from a pair/tuple.

    ::

        std::vector<int> a { 0, 42, 69 };
        std::vector<int> b { 18, 64, 69 };
        auto v = tl::views::zip(a,b) 
               | std::views::filter(tl::curry(std::ranges::equal_to{}))
               | tl::to<std::vector>();
        //v == {(69,69)}       