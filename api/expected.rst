expected
========

`Source code <https://github.com/TartanLlama/expected/blob/master/include/tl/expected.hpp>`_

C++11/14/17 `std::expected <https://wg21.link/p0323r3>`_ with functional-style extensions and reference support.

`tl::expected`
--------------

.. class:: template<class T, class E> expected

    A `tl::expected<T, E>` object is an object that contains the storage for
    another object and manages the lifetime of this contained object `T`.
    Alternatively it could contain the storage for another unexpected object
    `E`. The contained object may not be initialized after the expected object
    has been initialized, and may not be destroyed before the expected object
    has been destroyed. The initialization state of the contained object is
    tracked by the expected object.

    `T` must not be a reference type, but it may be `void`.

    **Member Types**

    .. type:: value_type = T
    .. type:: error_type = E
    .. type:: unexpected_type = unexpected<E>

    **Special Members**

    .. function:: constexpr expected()

        Default-constructs the expected value. 
        
        Only available if `T` is default-constructible.

    .. function:: constexpr expected(expected const&)
                  constexpr expected(expected&&)

    .. function:: template<class... Args>\
                  expected(tl::in_place_t, Args&&...)
                  template<class U, class... Args>\
                  expected(tl::in_place_t, std::initializer_list<U>, Args&&...)
        
        Constructs the expected value in-place using the given arguments.

    .. function:: template<class G=E>\
                  constexpr expected (unexpected<G> const& e)
                  template<class G=E>\
                  constexpr expected (unexpected<G> && e)
                    
        Constructs the unexpected value.

        `explicit` if `e` is not implicitly convertible to `E`.

    .. function:: template<class... Args>\
                  expected(tl::unexpect_t, Args&&...)
                  template<class U, class... Args>\
                  expected(tl::unexpect_t, std::initializer_list<U>, Args&&...)
        
        Constructs the unexpected value in-place using the given arguments.

    .. function:: template <class U, class G>\
                  constexpr expected(expected<U, G> const &rhs)
                  template <class U, class G>\
                  constexpr expected(expected<U, G> &&rhs)

        Converting copy/move constructors.

        `explicit` if `U` and `G` are not implicitly convertible to `T` and `E`.

    .. function:: template<class U=T> constexpr expected(U&& v)

        Constructs the expected value with the given value.

    .. function:: template <class U = T>\
                  explicit expected& operator=(U&& v)

        If `this*` in in the expected state, assigns `v` to the expected value.
        Otherwise destructs the unexpected value and constructs the
        expected value with `v`.

    .. function:: template <class G = E>\
                  expected& operator=(tl::unexpected<G> const& e)
                  template <class G = E>\
                  expected& operator=(tl::unexpected<G> && e)
           
        If `this*` in in the unexpected state, assigns `e` to the unexpected value.
        Otherwise destructs the expected value and constructs the
        unexpected value with `e`.

    *Standard Interface*

    This part of the interface is based on the proposed `std::expected`.

    .. function:: template<class... Args>\
                  void emplace(Args &&... args)
                  template<class U, class... Args>\
                  void emplace(std::initializer_list<U>, Args &&... args)
        
        If `this*` in in the expected state, assigns a `T` constructed in-place 
        from `args...` to the expected value. 
        Otherwise destructs the unexpected value and constructs the expected value
        in-place from `args...`.
    
    .. function:: void swap(expected &rhs)

        Swaps `*this` with `rhs`.

        `noexcept` if `T` and `E` are nothrow-swappable and 
        -move-constructible.

    .. function:: constexpr T* operator->()
                  constexpr T const* operator->() const

        Returns a pointer to the expected value. Undefined behaviour
        if `*this` is in the unexpected state. Use :func:`tl::expected::value`
        for checked value retrieval.

    .. function:: constexpr T & operator*() &
                  constexpr T const & operator*() const &
                  constexpr T && operator*() &&
                  constexpr T const && operator*() const &&

        Returns the expected value. Undefined behaviour if `*this` is in the unexpected
        state. Use :func:`tl::expected::value` for checked value retrieval.

    .. function:: constexpr T & value() &
                  constexpr T const & value() const &
                  constexpr T && value() &&
                  constexpr T const && value() const &&
    
        If `*this` is in the expected state, returns the expected value.
        Otherwise throws :class:`tl::bad_expected_access`.

    .. function:: constexpr E & error() &
                  constexpr E const & error() const &
                  constexpr E && error() &&
                  constexpr E const && error() const &&
    
        If `*this` is in the unexpected state, returns the unexpected value.
        Undefined behaviour if `*this` is in the expected state. 
        Use :func:`tl::expected::has_value` or 
        :func:`tl::expected::operator bool` to check the state before
        calling.

    .. function:: constexpr bool has_value() const noexcept
                  constexpr explicit operator bool() const noexcept

        Returns whether or not `*this` is in the expected state.

    .. function:: template<class U> constexpr T value_or(U &&u) const&
                  template<class U> constexpr T value_or(U &&u) &&

        If `*this` is in the expected state, returns the expected value.
        Otherwise returns `u`.

    **Extensions**

    These functions are all extensions to the proposed `std::expected`.

    .. function:: template<class F> constexpr auto and_then(F &&f) &
                  template<class F> constexpr auto and_then(F &&f) const &
                  template<class F> constexpr auto and_then(F &&f) &&
                  template<class F> constexpr auto and_then(F &&f) const &&

        Used to compose functions which return a :class:`tl::expected`.
        If `*this` is in the expected state, applies `f` to the expected value
        and returns the result. Otherwise returns `*this` (i.e. the unexpected 
        value bubbles up).

    *Requires*: Calling the given function with the expected value must return
    a specialization of :class:`tl::expected`.

  .. function:: template<class F> constexpr auto map(F &&f) &
                template<class F> constexpr auto map(F &&f) const &
                template<class F> constexpr auto map(F &&f) &&
                template<class F> constexpr auto map(F &&f) const &&
                template<class F> constexpr auto transform(F &&f) &
                template<class F> constexpr auto transform(F &&f) const &
                template<class F> constexpr auto transform(F &&f) &&
                template<class F> constexpr auto transform(F &&f) const &&

    Apply a function to change the expected value (and possibly the type).
    If `*this` is in the expected state, applies `f` to the expected value 
    and returns the result wrapped in a `tl::expected<ResultType, E>`. 
    Otherwise returns `*this` (i.e. the unexpected value bubbles up).


  .. function:: template<class F> constexpr auto map_error(F &&f) &
                template<class F> constexpr auto map_error(F &&f) const &
                template<class F> constexpr auto map_error(F &&f) &&
                template<class F> constexpr auto map_error(F &&f) const &&

    Apply a function to change the unexpected value (and possibly the type).
    If `*this` is in the unexpected state, applies `f` to the unexpected value 
    and returns the result wrapped in a `tl::expected<T, ResultType>`. 
    Otherwise returns `*this` (i.e. the expected value bubbles up).

  .. function:: template<class F> expected<T, E> constexpr or_else(F &&f) &
                template<class F> expected<T, E> constexpr or_else(F &&f) const &
                template<class F> expected<T, E> constexpr or_else(F &&f) &&
                template<class F> expected<T, E> constexpr or_else(F &&f) const &&

    If `*this` is in the unexpected state, calls `f(this->error())` and returns the result. 
    Otherwise returns `*this`.

    *Requires*: `std::invoke_result_t<F>` must be `void` or convertible to `tl::expected<T,E>`.

.. function:: template <class T, class E, class U, class F>\
              constexpr bool operator==(expected<T, E> const &lhs,\
                                        expected<U, F> const &rhs)
              template <class T, class E, class U, class F>\
              constexpr bool operator!=(expected<T, E> const &lhs,\
                                        expected<U, F> const &rhs)

    Compare two :class:`tl::expected` objects. They are considered equal
    if they are both in the same expected/unexpected state and 
    their stored objects are equal. 

.. function:: template <class T, class E, class U>\
              constexpr bool operator==(expected<T, E> const &e,\
                                        U const &u)
              template <class T, class E, class U>\
              constexpr bool operator!=(expected<T, E> const &e,\
                                        U const &u)
              template <class T, class E, class U>\
              constexpr bool operator==(U const &u,\
                                        expected<T, E> const &e)
              template <class T, class E, class U>\
              constexpr bool operator!=(U const &u,\
                                        expected<T, E> const &e)
            
    Compare a `tl::expected` to an expected value. Only true if `e`
    stores has an expected value which is equal to `u`.

.. function:: template <class T, class E>\
              constexpr bool operator==(expected<T, E> const &e,\
                                        tl::unexpected<E> const &u)
              template <class T, class E>\
              constexpr bool operator!=(expected<T, E> const &e,\
                                        tl::unexpected<E> const &u)
              template <class T, class E>\
              constexpr bool operator==(tl::unexpected<E> const &u,\
                                        expected<T, E> const &e)
              template <class T, class E>\
              constexpr bool operator!=(tl::unexpected<E> const &u,\
                                        expected<T, E> const &e)
            
    Compare a `tl::expected` to an unexpected value. Only true if `e`
    stores has an unexpected value which is equal to `u`.

.. function:: template <class T, class E>\
              void swap(tl::expected<T,E> &lhs, tl::expected<T,E> &rhs)

    Calls `lhs.swap(rhs)`.

    `noexcept` if `lhs.swap(rhs)` is `noexcept`.


`tl::unexpected`
----------------

.. class:: template<class E> tl::unexpected

    Used as a wrapper to store the unexpected value.

    `E` must not be `void`.

    .. function:: unexpected() = delete

    .. function:: constexpr explicit unexpected(E const &e)
                  constexpr explicit unexpected(E&&)

        Copies/moves the stored value.

    .. function:: constexpr E const &value() const &
                  constexpr E & value() &
                  constexpr E && value() && 
                  constexpr E const && value() const &&

        Returns the contained value.

.. function:: template <class E>\
              constexpr bool operator==(const unexpected<E> &lhs, const unexpected<E> &rhs)
              template <class E>\
              constexpr bool operator!=(const unexpected<E> &lhs, const unexpected<E> &rhs)
              template <class E>\
              constexpr bool operator<(const unexpected<E> &lhs, const unexpected<E> &rhs)
              template <class E>\
              constexpr bool operator<=(const unexpected<E> &lhs, const unexpected<E> &rhs)
              template <class E>\
              constexpr bool operator>(const unexpected<E> &lhs, const unexpected<E> &rhs)
              template <class E>\
              constexpr bool operator>=(const unexpected<E> &lhs, const unexpected<E> &rhs)

    Compares two unexpected objects by comparing their stored value.

.. function:: template <class E>\
              unexpected<std::decay_t<E>> tl::make_unexpected(E &&e)

    Create an `unexpected` from `e`, deducing the return type
    
    Example: ::
    
        auto e1 = tl::make_unexpected(42);
        tl::unexpected<int> e2 (42); //same semantics

.. var:: static constexpr unexpect_t tl::unexpect

    A tag to tell :class:`tl::expected` to construct the unexpected value.

    Example: ::

        tl::expected<int,int> a(tl::unexpect, 42); 
 

Related Definitions
-------------------

.. class:: template <class E> bad_expected_access : public std::exception 

    Thrown when checked value accesses fail, e.g.: ::

        tl::expected<int, bool> a(tl::unexpect, false);
        a.value(); //throws bad_expected_access<bool>

    .. function:: explicit bad_expected_access(E)

    .. function:: const char *what() const noexcept override

        Returns "Bad expected access"

    .. function E const &error() const &
                E &error() &
                E const &&error() const &&
                E &&error() && 

        Access the unexpected value which was stored when a bad access
        was attempted.
        
.. var:: static constexpr tl::in_place_t tl::in_place

  A tag to tell expected to construct its value in-place
