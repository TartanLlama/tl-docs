generator
========

`Source code <https://github.com/TartanLlama/expected/blob/master/tl/generator.hpp>`_

ranges-compatible generator type built on C++20 coroutines.

.. class:: template <class T> tl::generator

    A generator allows implementing sequence producers which are terse and avoid creating the whole sequence in memory.

    Example: ::

        tl::generator<int> iota(int i = 0) {
            while(true) {
                co_yield i;
                ++i;
            }
        }

    **Member Types**

    .. class:: promise

        **Member Types**

        .. type:: value_type = std::remove_reference_t<T>
        .. type:: reference_type = value_type&
        .. type:: pointer_type = value_type*

    .. class:: sentinel
    .. class:: iterator

        **Member Types**

        .. type:: promise_type = promise
        .. type:: value_type = promise::value_type
        .. type:: reference_type = promise::reference_type
        .. type:: pointer_type = promise::pointer_type
        .. type:: handle_type = std::coroutine_handle<promise>
        .. type:: difference_type = std::ptrdiff_t

        **Special Members**

        .. function:: iterator() = delete

            The iterators should only be created by `tl::generator<T>::begin`

        .. function:: iterator(iterator const&)
                      iterator& operator=(iterator const&)

            Coroutine handles point to a unique resource, so the iterators are not copyable.

        .. function:: generator(generator&& rhs)
                      generator& operator=(generator&& rhs) 

            Takes the coroutine handle from `rhs`, making `rhs` not tied to a coroutine.

        
        **Member Functions**

        .. function:: friend bool operator==(iterator const& it, sentinel)

            Returns `true` if the iterator has been moved from, or if the coroutine it is tied to has completed.

        .. function:: iterator& operator++()
                      void operator++(int)

            Resumes the coroutine until return/co_yield/exception and returns an iterator which can be used to retrieve the yielded value and drive the coroutine forward again.

            Rethrows the exception if one occurred.

        .. function:: reference_type operator*()

            Returns the last value yielded.

    .. type:: promise_type = promise
    .. type:: handle_type = std::coroutine_handle<promise_type>

    **Special Members**
    
    .. function:: generator()

        Creates a generator which is not tied to a coroutine.

    .. function:: generator(handle_type handle)

        Creates a generator for the given coroutine handle.

    .. function:: generator(generator const&) = delete
                generator& operator=(generator const&) = delete

        Coroutine handles point to a unique resource, so generators are not copyable.

    .. function:: generator(generator&& rhs)
                  generator& operator=(generator&& rhs) 

        Takes the coroutine handle from `rhs`, making `rhs` not tied to a coroutine.
    

    **Member Functions**

    .. function:: iterator begin()

        Resumes the coroutine until return/co_yield/exception and returns an iterator which can be used to retrieve the yielded value and drive the coroutine forward again.

        Rethrows the exception if one occurred.

        Calling `begin` twice on the same generator is undefined behaviour.

    .. function:: sentinel end()

.. var:: template <class T> inline constexpr bool std::ranges::enable_view<tl::generator<T>> = true

    `tl::generator<T>` is a view.