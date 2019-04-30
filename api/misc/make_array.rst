make_array
==========

`Source code <https://github.com/TartanLlama/tl/blob/master/include/tl/make_array.hpp>`_

Basic implementation of `make_array <https://en.cppreference.com/w/cpp/experimental/make_array>`_

.. function:: template <class... Ts>\
              constexpr std::array<std::decay_t<std::common_type_t<Ts...>>, sizeof...(Ts)>\
              tl::make_array(Ts&&... ts)

    Create a `std::array` from the given arguments, deducing the type and size
    of the array.

    Example: ::

        tl::make_array(0,1,2,3); // std::array<int,4>{0,1,2,3}