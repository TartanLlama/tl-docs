decay_copy
==========

`Source code <https://github.com/TartanLlama/tl/blob/master/include/tl/decay_copy.hpp>`_

An implementation of `decay_copy <http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2011/n3255.html>`_.

.. cpp:function:: template <class T> std::decay_t<T> tl::decay_copy (T&& t)

    Creates a copy of `t`, decaying the type. Used to produce an rvalue from
    some expression without accidentally moving lvalues.