ranges
========

`Source code <https://github.com/TartanLlama/ranges/tree/main/include/tl>`_

Implementations of ranges that didn't make C++20.

**Understanding Range adaptors**

The documentation for each range adaptor provides the following information:

    **Requires:** Any constraints on constructing the adaptor.

    Reference: The type you get by dereferencing the adaptor's iterator type.

    Category: The range category for the adaptor, which is either `input <https://en.cppreference.com/w/cpp/ranges/input_range>`_, `output <https://en.cppreference.com/w/cpp/ranges/output_range>`_, `forward <https://en.cppreference.com/w/cpp/ranges/forward_range>`_, `bidirectional <https://en.cppreference.com/w/cpp/ranges/bidirectional_range>`_, `random-access <https://en.cppreference.com/w/cpp/ranges/random_access_range>`_, or `contiguous <https://en.cppreference.com/w/cpp/ranges/contiguous_range>`_. 

    Sized: When the view is a `sized_range <https://en.cppreference.com/w/cpp/ranges/sized_range>`_, i.e. you can call `std::ranges::size` to get its size in O(1).
    
    Common: When the view is a `common_range <https://en.cppreference.com/w/cpp/ranges/common_range>`_, i.e. the iterator and sentinel for the view are the same type.

    Const-iterable: When `const TheRangeAdaptor` is a range.

    Borrowed: When the view is a `borrowed_range <https://en.cppreference.com/w/cpp/ranges/borrowed_range>`_ i.e. iterators produced by the view can outlive the view itself.

**Contents**

.. toctree::
   :maxdepth: 2
   :glob:

   ./*
   ./functional/index
   

