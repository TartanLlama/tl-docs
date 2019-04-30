optional
========

`Source code <https://github.com/TartanLlama/optional/blob/master/tl/optional.hpp>`_

C++11/14/17 `std::optional` with functional-style extensions and reference support.

tl::optional
------------

.. class:: tl::optional

  An optional object is an object that contains the storage for another
  object and manages the lifetime of this contained object, if any. The
  contained object may be initialized after the optional object has been
  initialized, and may be destroyed before the optional object has been
  destroyed. The initialization state of the contained object is tracked by
  the optional object.
  
  **Member Types**

  .. type:: value_type = T

  **Special Members**

  .. _optional-constructors:

  .. function:: constexpr optional() noexcept
                constexpr optional(tl::nullopt_t) noexcept

    Constructs an optional that does not contain a value.

  .. function:: constexpr optional(optional const & rhs)
                constexpr optional(optional && rhs)

    Copy and move constructors. If `rhs` contains a value, the 
    stored value is direct-initialized with it. Otherwise, the 
    constructed optional is empty.

  .. function:: template <class... Args> \
                constexpr explicit optional(tl::in_place_t, Args &&...)
                template <class U, class... Args> \
                constexpr explicit optional(tl::in_place_t, std::initializer_list<U>, Args &&...)

    Constructs the stored value in-place using the given arguments.

  .. function:: template <class U = T> constexpr optional(U &&u) 

    Constructs the stored value with `u`.

    `explicit` if `u` is convertible to `T`. 

  .. function:: template<class U> optional(optional<U> const & rhs)
                    template<class U> optional(optional<U> && rhs)

    Converting copy and move constructors. If `rhs` contains a value, the 
    stored value is direct-initialized with it. Otherwise, the 
    constructed optional is empty.

    `explicit` if the value of `rhs` is convertible to `T`.

  .. function:: optional &operator=(nullopt_t) noexcept

    Makes the optional empty, destroying the stored value if there is one.

  .. function:: optional &operator=(optional const &rhs)
                optional &operator=(optional &&rhs)

    Copy and move assignment operators. Copies/moves the value from `rhs` if there
    is one. Otherwise makes the optional empty, destroying the stored value
    if there is one.

  .. function:: template <class U = T> optional &operator=(U &&u)

    Assigns the stored value from `u`, destroying the old value if there 
    was one.

  .. function:: template <class U> optional &operator=(const optional<U> &rhs)

    Converting copy/move assignment operators. Copies/moves the value from `rhs`
    if there is one. Otherwise makes the optional empty, destroying the stored
    value if there is one.

  .. function:: ~optional()

    Destroys the stored value if there is one.

  **Standard Optional Features**

  These features are all the same as `std::optional`.

  .. function:: template <class... Args> T &emplace(Args &&... args)

    Constructs the value in-place, destroying the current one if there is one.

  .. function:: void swap(optional &rhs)

    Swaps this optional with the other.

    If neither optionals have a value, nothing happens.
    If both have a value, the values are swapped.
    If one has a value, it is moved to the other and the movee is left
    valueless.

    `noexcept` if `T` is nothrow swappable and move constructible.

  .. function:: constexpr T* operator->()
                constexpr T const* operator->() const
    
     Returns a pointer to the stored value. Undefined behaviour if there
     is no value. Use :func:`tl::optional::value` for checked value 
     retrieval.


  .. function:: constexpr T & operator*() &
                constexpr T const & operator*() const &
                constexpr T && operator*() &&
                constexpr T const && operator*() const &&

    Returns the stored value. Undefined behaviour if there is no value.
    Use :func:`tl::optional::value` for checked value retrieval.

  .. function:: constexpr T & value() &
                constexpr T const & value() const &
                constexpr T && value() &&
                constexpr T const && value() const &&
    
    Returns the stored value if there is one, otherwise throws
    :class:`tl::bad_optional_access`.

  .. function:: constexpr bool has_value() const noexcept
                constexpr explicit operator bool() const noexcept

    Returns whether or not the optional has a value.

  .. function template<class U> constexpr T value_or(U &&u) const&
              template<class U> constexpr T value_or(U &&u) &&

    Returns the stored value if there is one, otherwise returns `u`.

  .. function reset() noexcept

    Destroys the stored value if one exists, making the optional empty.

  **Extensions**

  These features are all extensions to `std::optional`.

  .. function:: template<class F> constexpr auto and_then(F &&f) &
                template<class F> constexpr auto and_then(F &&f) const &
                template<class F> constexpr auto and_then(F &&f) &&
                template<class F> constexpr auto and_then(F &&f) const &&

    Used to compose functions which return a :class:`tl::optional`.
    Applies `f` to the value stored in the optional and returns the result.
    If there is no stored value, then it returns an empty optional.

    *Requires*: Calling the given function with the stored value must return
    a specialization of :class:`tl::optional`.

  .. function:: template<class F> constexpr auto map(F &&f) &
                template<class F> constexpr auto map(F &&f) const &
                template<class F> constexpr auto map(F &&f) &&
                template<class F> constexpr auto map(F &&f) const &&
                template<class F> constexpr auto transform(F &&f) &
                template<class F> constexpr auto transform(F &&f) const &
                template<class F> constexpr auto transform(F &&f) &&
                template<class F> constexpr auto transform(F &&f) const &&

    Apply a function to change the value (and possibly the type) stored.
    Applies `f` to the value stored in the optional and returns the result
    wrapped in an optional. If there is no stored value, then it returns an
    empty optional.

  .. function:: template<class F> optional<T> constexpr or_else(F &&f) &
                template<class F> optional<T> constexpr or_else(F &&f) const &
                template<class F> optional<T> constexpr or_else(F &&f) &&
                template<class F> optional<T> constexpr or_else(F &&f) const &&

    Calls `f` if the optional is empty and returns the result. If the optional
    already has a value, returns `*this`.

    *Requires*: `std::invoke_result_t<F>` must be `void` or convertible to `tl::optional<T>`.

  .. function:: template <class F, class U> U map_or(F &&f, U &&u) &
                template <class F, class U> U map_or(F &&f, U &&u) const &
                template <class F, class U> U map_or(F &&f, U &&u) &&
                template <class F, class U> U map_or(F &&f, U &&u) const &&

    Maps the stored value with `f` if there is one, otherwise returns `u`.

  .. function:: template <class U> constexpr optional<std::decay_t<U>> conjunction(U &&u) const

     Returns `u` if `*this` has a value, otherwise an empty optional.

  .. function:: constexpr optional disjunction(const optional &rhs) &
                constexpr optional disjunction(const optional &rhs) const &
                constexpr optional disjunction(const optional &rhs) &&
                constexpr optional disjunction(const optional &rhs) const &&

    Returns `rhs` if `*this` is empty, otherwise the current value.

  .. function:: optional take()

    Takes the value out of the optional, leaving it empty

.. function:: template<class T, class U>\
              constexpr bool operator==(tl::optional<T> const&, tl::optional<U> const&)
              template<class T, class U>\
              constexpr bool operator!=(tl::optional<T> const&, tl::optional<U> const&)
              template<class T, class U>\
              constexpr bool operator<(tl::optional<T> const&, tl::optional<U> const&)
              template<class T, class U>\
              constexpr bool operator<=(tl::optional<T> const&, tl::optional<U> const&)
              template<class T, class U>\
              constexpr bool operator>(tl::optional<T> const&, tl::optional<U> const&)
              template<class T, class U>\
              constexpr bool operator>=(tl::optional<T> const&, tl::optional<U> const&)

  If both optionals contain a value, they are compared with `T` s
  relational operators. Otherwise `lhs` and `rhs` are equal only if they are
  both empty, and `lhs` is less than `rhs` only if `rhs` is empty and `lhs` is not.

.. function:: template <class T>\
              constexpr bool operator==(tl::optional<T> const &, tl::nullopt_t)
              template <class T>\
              constexpr bool operator!=(tl::optional<T> const &, tl::nullopt_t)
              template <class T>\
              constexpr bool operator<(tl::optional<T> const &, tl::nullopt_t)
              template <class T>\
              constexpr bool operator<=(tl::optional<T> const &, tl::nullopt_t)
              template <class T>\
              constexpr bool operator>(tl::optional<T> const &, tl::nullopt_t)
              template <class T>\
              constexpr bool operator>=(tl::optional<T> const &, tl::nullopt_t)
              template <class T>\
              constexpr bool operator==(tl::nullopt_t, tl::optional<T> const &)
              template <class T>\
              constexpr bool operator!=(tl::nullopt_t, tl::optional<T> const &)
              template <class T>\
              constexpr bool operator<(tl::nullopt_t, tl::optional<T> const &)
              template <class T>\
              constexpr bool operator<=(tl::nullopt_t, tl::optional<T> const &)
              template <class T>\
              constexpr bool operator>(tl::nullopt_t, tl::optional<T> const &)
              template <class T>\
              constexpr bool operator>=(tl::nullopt_t, tl::optional<T> const &)

  Equivalent to comparing the optional to an empty optional  

       
.. function:: template<class T> void swap(tl::optional<T>& lhs, tl::optional<T>& rhs)
  
  Calls lhs.swap(rhs).

  *noexcept* if lhs.swap(rhs) is noexcept

tl::optional<T&>
----------------

.. class:: template<class T> tl::optional<T&>

  Specialization for when `T` is a reference. `optional<T&>` acts similarly
  to a `T*`, but provides more operations and shows intent more clearly.
 
  *Examples*: ::
 
    int i = 42;
    tl::optional<int&> o = i;
    *o == 42; //true
    i = 12;
    *o = 12; //true
    &*o == &i; //true
 
  Assignment has rebind semantics rather than assign-through semantics: ::
 
    int j = 8;
    o = j;
    
    &*o == &j; //true

  .. type:: value_type = T&

  **Special Members**

  .. function:: constexpr optional() noexcept
                constexpr optional(tl::nullopt_t) noexcept

    Constructs an optional that does not contain a reference.

  .. function:: constexpr optional(optional const & rhs)
                constexpr optional(optional && rhs)

    Copy and move constructors. If `rhs` contains a reference, makes the 
    stored reference point at the same object. Otherwise, the 
    constructed optional is empty.

  .. function:: template <class U = T> constexpr optional(U &&u)

    Makes the stored reference point at `u`.

    `u` must be an lvalue.

  .. function:: template<class U> optional(optional<U> const & rhs)

    Converting copy constructor. If `rhs` contains a reference, makes the
    stored reference point at the same object. Otherwise, the 
    constructed optional is empty.
    
  .. function:: optional &operator=(nullopt_t) noexcept

    Makes the optional empty.

  .. function:: optional &operator=(optional const &rhs)

    Copy assignment operator. If `rhs` contains a reference,
    makes the stored reference point at the same object. Otherwise, the
    constructed optional is empty.

  .. function:: template <class U = T> optional &operator=(U &&u)

    Makes the stored reference point at the same object.

    `u` must be an lvalue.

  .. function:: template <class U> optional &operator=(const optional<U> &rhs)

    Converting copy assignment operator. If `rhs` contains a reference,
    makes the stored reference point at the same object. Otherwise, the
    constructed optional is empty.

  .. function:: ~optional()

    No-op

  **Standard Optional Features**

  These features are modelled after those in `std::optional`.
  
  .. function:: void swap(optional &rhs) noexcept

    Swaps this optional with the other.

    If neither optionals have a reference, nothing happens.
    If both have a reference, the references are swapped.
    If one has a reference, it is moved to the other and the movee is left
    referenceless.

  .. function:: constexpr T* operator->()
                constexpr T const* operator->() const
    
     Returns a pointer to the stored value.

  .. function:: constexpr T & operator*() &
                constexpr T const & operator*() const &
                constexpr T && operator*() &&
                constexpr T const && operator*() const &&

    Returns the stored value. Undefined behaviour if there is no value.
    Use :func:`tl::optional<T&>::value` for checked value retrieval.

  .. function:: constexpr T & value() &
                constexpr T const & value() const &
                constexpr T && value() &&
                constexpr T const && value() const &&
    
    Returns the stored value if there is one, otherwise throws
    :class:`tl::bad_optional_access`.

  .. function:: constexpr bool has_value() const noexcept
                constexpr explicit operator bool() const noexcept

    Returns whether or not the optional has a value.

  .. function template<class U> constexpr T value_or(U &&u) const&
              template<class U> constexpr T value_or(U &&u) &&

    Returns the stored value if there is one, otherwise returns `u`.

  .. function reset() noexcept

    Makes the optional empty.

  **Extensions**

  These features are all extensions to `std::optional`.

  .. function:: template<class F> constexpr auto and_then(F &&f) &
                template<class F> constexpr auto and_then(F &&f) const &
                template<class F> constexpr auto and_then(F &&f) &&
                template<class F> constexpr auto and_then(F &&f) const &&

    Used to compose functions which return a :class:`tl::optional`.
    Applies `f` to the value stored in the optional and returns the result.
    If there is no stored value, then it returns an empty optional.

    *Requires*: Calling the given function with the stored value must return
    a specialization of :class:`tl::optional`.

  .. function:: template<class F> constexpr auto map(F &&f) &
                template<class F> constexpr auto map(F &&f) const &
                template<class F> constexpr auto map(F &&f) &&
                template<class F> constexpr auto map(F &&f) const &&
                template<class F> constexpr auto transform(F &&f) &
                template<class F> constexpr auto transform(F &&f) const &
                template<class F> constexpr auto transform(F &&f) &&
                template<class F> constexpr auto transform(F &&f) const &&

    Apply a function to change the value (and possibly the type) stored.
    Applies `f` to the value stored in the optional and returns the result
    wrapped in an optional. If there is no stored value, then it returns an
    empty optional.

  .. function:: template<class F> optional<T> constexpr or_else(F &&f) &
                template<class F> optional<T> constexpr or_else(F &&f) const &
                template<class F> optional<T> constexpr or_else(F &&f) &&
                template<class F> optional<T> constexpr or_else(F &&f) const &&

    Calls `f` if the optional is empty and returns the result. If the optional
    already has a value, returns `*this`.

    *Requires*: `std::invoke_result_t<F>` must be `void` or convertible to `tl::optional<T>`.

  .. function:: template <class F, class U> U map_or(F &&f, U &&u) &
                template <class F, class U> U map_or(F &&f, U &&u) const &
                template <class F, class U> U map_or(F &&f, U &&u) &&
                template <class F, class U> U map_or(F &&f, U &&u) const &&

    Maps the stored value with `f` if there is one, otherwise returns `u`.

  .. function:: template <class U> constexpr optional<std::decay_t<U>> conjunction(U &&u) const

     Returns `u` if `*this` has a value, otherwise an empty optional.

  .. function:: constexpr optional disjunction(const optional &rhs) &
                constexpr optional disjunction(const optional &rhs) const &
                constexpr optional disjunction(const optional &rhs) &&
                constexpr optional disjunction(const optional &rhs) const &&

    Returns `rhs` if `*this` is empty, otherwise the current value.

  .. function:: optional take()

    Takes the reference out of the optional, leaving it empty

Related Definitions
-------------------

.. class:: template<class T> std::hash<tl::optional<T>>
  
  .. function:: std::size_t operator()(tl::optional<T> const&) const

    Returns the hash of the stored value if one exists. Otherwise returns `0`.

.. class:: tl::monostate

  Used to represent an optional with no data; essentially a bool

.. var:: static constexpr tl::in_place_t tl::in_place

  A tag to tell optional to construct its value in-place

.. var:: static constexpr tl::nullopt_t tl::nullopt

  Represents an empty optional

  *Examples*: ::
 
    tl::optional<int> a = tl::nullopt;
    void foo (tl::optional<int>);
    foo(tl::nullopt); //pass an empty optional

.. class:: tl::nullopt_t

.. class:: tl::bad_optional_access : public std::exception
