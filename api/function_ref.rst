function_ref
============

`Source code <https://github.com/TartanLlama/function_ref/blob/master/function_ref.hpp>`_

An implementation of `function_ref <https://wg21.link/P0792>`_.

.. class:: template <class F> tl::function_ref

    A lightweight non-owning reference to a callable.

    Example: ::
    
        void foo (function_ref<int(int)> func) {
            std::cout << "Result is " << func(21); //42
        }

        foo([](int i) { return i*2; });

.. class:: template<class R, class... Args> tl::function_ref<R(Args...)>

    Specialization for function types.

    **Special Members**

    .. function:: constexpr function_ref() noexcept = delete

    .. function:: constexpr function_ref(function_ref const &rhs) noexcept

        Creates a `tl::function_ref` which refers to the same callable as `rhs`.

    .. function:: template <typename F> constexpr function_ref(F &&f) noexcept

        Creates a `tl::function_ref` which refers to `f`.

        `f` must be invocable with `Args...`, returning a type convertible to `R`.

    .. function:: function_ref & operator=(function_ref const &rhs) noexcept

        Makes `*this` refer to the same callable as `rhs`.

    .. function:: template <typename F> constexpr function_ref &operator=(F &&f) noexcept

        Makes `*this` refer to `f`.

        `f` must be invocable with `Args...`, returning a type convertible to `R`.

    .. function:: constexpr void swap(function_ref &rhs) noexcept

        Swaps the callables referred to by `*this` and `rhs`.

    .. function:: R operator()(Args... args) const

        Invoke the stored callable with the given arguments.

.. function:: template <typename R, typename... Args>\
              constexpr void swap(function_ref<R(Args...)> &lhs,\
                                  function_ref<R(Args...)> &rhs) noexcept 

    Swaps the callables referred to by `*this` and `rhs`.