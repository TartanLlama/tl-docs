typelist
========

`Source code <https://github.com/TartanLlama/tl/blob/master/include/tl/typelist.hpp>`_

Utilities to manipulate typelists.

.. cpp:struct:: template <class... Ts> tl::typelist

    Doesn't contain anything, just used to pass around a list of types.

.. cpp:struct:: template <class List, size_t N> tl::index_typelist

    Given a typelist and an index, gives the Nth type in the list.
    Assumes that the list is long enough.

    .. cpp:type:: type = magic

        The Nth type.

.. cpp:struct:: template <class List1, class List2> tl::cat_typelist

    Concatenates two typelists.

    .. cpp:type:: type = magic

        The result.

.. cpp:struct:: template <auto... Ts> tl::vallist

    Doesn't contain anything, just used to pass around a list of compile-time values.

.. cpp:struct:: template <class List, size_t N> tl::index_vallist

    Given a typelist and an index, gives the Nth value in the list.
    Assumes that the list is long enough.

    .. cpp:var:: static constexpr auto value = magic

        The Nth value.

.. cpp:struct:: template <class List1, class List2> tl::cat_vallist

    Concatenates two vallists.

    .. cpp:var:: static constexpr auto value = magic

        The result.

