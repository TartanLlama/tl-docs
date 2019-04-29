apply
=====

`Source code <https://github.com/TartanLlama/tl/blob/master/include/tl/apply.hpp>`_

A C++11 implementation of C++17's `std::apply <https://en.cppreference.com/w/cpp/utility/apply>`_.

.. cpp:function:: template <class F, class Tuple>\
                  auto tl::apply(F&& f, Tuple&& tuple)

    Calls `f` with the contents of `tuple` as arguments.

    Equivalent to: ::

        f(std::get<0>(tuple), std::get<1>(tuple), /*..*/ std::get<N>(tuple));

    SFINAE-friendly.
    
    `noexcept` if the call to `f` is `noexcept`.