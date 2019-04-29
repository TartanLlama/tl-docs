type_traits
===========

`Source code <https://github.com/TartanLlama/tl/blob/master/include/tl/type_traits.hpp>`_

Implementations of some type traits from C++17 and Lib Fundamentals v2 TS, 
and C++14-style type aliases for C++11.

.. cpp:type:: template<bool B> tl::bool_constant = std::integral_constant<bool, B>

.. cpp:type:: template<std::size_t N> tl::index_constant = std::integral_constant<std::size_t, N>

.. cpp:struct:: template<class... Cs> tl::conjunction

    .. cpp:var:: static constexpr bool value

        The result of `&&` ing together `C::value` for each `C` in `Cs`.

        Like doing `(Cs::value && ...)` in C++17.

     .. cpp:type:: type = tl::bool_constant<value>


.. cpp:struct:: template<class... Cs> tl::disjunction

    .. cpp:var:: static constexpr bool value

        The result of `||` ing together `C::value` for each `C` in `Cs`.

        Like doing `(Cs::value || ...)` in C++17.

     .. cpp:type:: type = tl::bool_constant<value>

.. cpp:struct:: template<class B> tl::negation : tl::bool_constant<!B::value>

    Negates a type trait result.

.. cpp:type:: template<class...> tl::void_t = void

    Turns any number of types into `void`.

    This is useful as a `metaprogramming trick <https://stackoverflow.com/questions/27687389/how-does-void-t-work>`_.

.. cpp:type:: template <template <class...> class Trait, class... Args>\
              tl::is_detected = magic

    Checks if `Trait<Args...>` is a valid specialization. Implements
    `std::experimental::is_detected <https://en.cppreference.com/w/cpp/experimental/is_detected>`_
    from Lib Fundamentals V2 TS. Useful for detecting the presence of a given type member. Example: ::

        template<class T>
        using make_cute_t = decltype(std::declval<T>().make_cute());

        template<class T>
        using can_make_cute = tl::is_detected<make_cute_t, T>;

        struct cat{ void make_cute(); };
        struct abstract_concept_of_fear{};

        static_assert(can_make_cute<cat>::value);
        static_assert(!can_make_cute<abstract_concept_of_fear>::value);

.. cpp:struct template <class Pack> tl::variadic_size

    Extract the number of template parameters in some template specialization.

    Example: ::

        template<class...> struct types{};
        static_assert(tl::variadic_size<types<int,void>::value == 2);
        static_assert(tl::variadic_size<types<int,void,char>::value == 3);

.. cpp:type:: template <typename T> tl::safe_underlying_type_t = magic

    Like `std::underlying_type <https://en.cppreference.com/w/cpp/types/underlying_type>`_, but
    if `T` is not an enum then there's just no `type` member rather than being UB. Essentially
    implements `P0340 <https://wg21.link/p0340r1>`_.

C++14-style alias templates
---------------------------

.. cpp:type:: template <class T> tl::remove_cv_t = typename std::remove_cv<T>::type 
.. cpp:type:: template <class T> tl::remove_const_t = typename std::remove_const<T>::type
.. cpp:type:: template <class T> tl::remove_volatile_t  = typename std::remove_volatile<T>::type
.. cpp:type:: template <class T> tl::add_cv_t  = typename std::add_cv<T>::type
.. cpp:type:: template <class T> tl::add_const_t  = typename std::add_const<T>::type
.. cpp:type:: template <class T> tl::add_volatile_t  = typename std::add_volatile<T>::type
.. cpp:type:: template <class T> tl::remove_reference_t  = typename std::remove_reference<T>::type
.. cpp:type:: template <class T> tl::add_lvalue_reference_t  = typename std::add_lvalue_reference<T>::type
.. cpp:type:: template <class T> tl::add_rvalue_reference_t  = typename std::add_rvalue_reference<T>::type
.. cpp:type:: template <class T> tl::remove_pointer_t  = typename std::remove_pointer<T>::type
.. cpp:type:: template <class T> tl::add_pointer_t  = typename std::add_pointer<T>::type
.. cpp:type:: template <class T> tl::make_signed_t  = typename std::make_signed<T>::type
.. cpp:type:: template <class T> tl::make_unsigned_t  = typename std::make_unsigned<T>::type
.. cpp:type:: template <class T> tl::remove_extent_t  = typename std::remove_extent<T>::type
.. cpp:type:: template <class T> tl::remove_all_extents_t  = typename std::remove_all_extents<T>::type
.. cpp:type:: template <std::size_t N, std::size_t AN> tl::aligned_storage_t  = typename std::aligned_storage<N,A>::type
.. cpp:type:: template <std::size_t N, class... Ts> tl::aligned_union_t  = typename std::aligned_union<N,Ts...>::type
.. cpp:type:: template <class T> tl::decay_t  = typename std::decay<T>::type
.. cpp:type:: template <bool E, class Tvoid> tl::enable_if_t  = typename std::enable_if<E,T>::type
.. cpp:type:: template <bool B, class T, class F> tl::conditional_t  = typename std::conditional<B,T,F>::type
.. cpp:type:: template <class... Ts> tl::common_type_t  = typename std::common_type<Ts...>::type
.. cpp:type:: template <class T> tl::underlying_type_t  = typename std::underlying_type<T>::type
.. cpp:type:: template <class T> tl::result_of_t  = typename std::result_of<T>::type

