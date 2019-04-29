casts
=====

`Source code <https://github.com/TartanLlama/tl/blob/master/include/tl/casts.hpp>`_

A handful of handy casts.

.. cpp:function:: template <class To, class From> To tl::bit_cast (From const& from)

    Casts the bit representation of `from` to a `To`. Use this instead of type punning
    through a union or `reinterpret_cast`. Essentially does: ::

        To to;
        std::memcpy(&to, &from, sizeof(to));

.. cpp:function:: template <class E> auto underlying_cast (E e)

    Casts an enumerator value to its underlying type.

    SFINAE-friendly.