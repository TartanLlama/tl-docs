overload
========

`Source code <https://github.com/TartanLlama/tl/blob/master/include/tl/overload.hpp>`_

A rudimentary implementation of `overload <http://open-std.org/JTC1/SC22/WG21/docs/papers/2016/p0051r2.pdf>`_.

Used for in-place visitation of `std::variant`: ::

    variant<int,float,std::string> my_variant;
    auto do_something = overload(
        [](int i) { /* do something with int */ },
        [](float f) { /* do something with float */ },
        [](std::string s) { /* do something with string */ }
    );
    visit(do_something, my_variant);

.. cpp:function:: template <class... Fs> auto overload(Fs&&... fs)

    Create a single function object with a call operator overloaded by
    all function objects in `fs...`.