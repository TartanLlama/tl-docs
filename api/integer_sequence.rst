integer_sequence
================

`Source code <https://github.com/TartanLlama/tl/blob/master/include/tl/integer_sequence.hpp>`_

An C++11 implementation of C++14's `compile-time integer sequences 
<https://en.cppreference.com/w/cpp/utility/integer_sequence>`_,
along with some utilities.

These constructs are typically used to implement the `indices trick 
<https://stackoverflow.com/questions/31463388/can-someone-please-explain-the-indices-trick>`_

.. cpp:struct:: template<class T, T... Ns> tl::integer_sequence

    A compile-time sequence of integers.

    .. cpp:type:: type = integer_sequence

    .. cpp:type:: value_type = T

    .. cpp:function:: static constexpr std::size_t size()

        The number of integers stored (`sizeof...(Ns)`).

.. cpp:type:: template<class T, std::size_t N>\
              tl::make_integer_sequence = magic

    Creates a :cpp:class:`tl::integer_sequence` from `0` to `N-1`.

    Example: ::

        tl::make_integer_sequence<int, 3>; //tl::integer_sequence<int,0,1,2>

.. cpp:type:: template<std::size_t... Idx>\
              tl::index_sequence = integer_sequence<std::size_t, Idx...>

    Alias for integer sequences of type `std::size_t`, which comes up a lot
    with utilities like `std::get`.

.. cpp:type:: template<std::size_t N>\
              tl::make_index_sequence = make_integer_sequence<std::size_t, N>

    Alias for making an integer sequence of `std::size_t` s.

.. cpp:type:: template<class... Ts>\
              tl::index_sequence_for = make_index_sequence<sizeof(Ts...)>

    Make an index sequence to index a parameter pack.

.. cpp:type:: template <std::size_t From, std::size_t N>\
              tl::make_index_range = magic

    Make in index sequence spanning the specified range.

    Example: ::

        make_index_range<3,2>; //tl::index_sequence<3,4>
        make_index_range<5,4>; //tl::index_sequence<5,6,7,8>