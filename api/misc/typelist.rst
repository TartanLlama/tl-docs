typelist
========

`Source code <https://github.com/TartanLlama/tl/blob/master/include/tl/typelist.hpp>`_

Utilities to manipulate typelists.

.. struct:: template <class... Ts> tl::typelist

    Doesn't contain anything, just used to pass around a list of types.

.. struct:: template <class List, size_t N> tl::index_typelist

    Given a typelist and an index, gives the Nth type in the list.
    Assumes that the list is long enough.

    .. type:: type = magic

        The Nth type.

.. struct:: template <class List1, class List2> tl::cat_typelist

    Concatenates two typelists.

    .. type:: type = magic

        The result.

.. struct:: template <auto... Ts> tl::vallist

    Doesn't contain anything, just used to pass around a list of compile-time values.

.. struct:: template <class List, size_t N> tl::index_vallist

    Given a typelist and an index, gives the Nth value in the list.
    Assumes that the list is long enough.

    .. var:: static constexpr auto value = magic

        The Nth value.

.. struct:: template <class List1, class List2> tl::cat_vallist

    Concatenates two vallists.

    .. var:: static constexpr auto value = magic

        The result.

