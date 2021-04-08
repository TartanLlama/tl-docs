ranges
========

`Source code <https://github.com/TartanLlama/ranges/tree/main/include/tl>`_

Implementations of ranges that didn't make C++20.

`tl::enumerate_view`/`tl::views::enumerate`
-------------------------------------------

.. class:: template <class V> class tl::enumerate_view : public std::ranges::view_interface<enumerate_view<V>>

    **Requires:** `std::ranges::input_range<V> && std::ranges::view<V>`

    A view which lets you iterate over the items in a range and their indices at the same time.

    Examples: ::

        std::vector<int> v;
        for (auto&& [index, item] : tl::views::enumerate(v)) {
            //...
        }
        for (auto&& [index, item] : tl::enumerate_view(v)) {
            //...
        }
        for (auto&& [index, item] : v | tl::views::enumerate) {
            //...
        }

    **Member Types**

    .. class:: template <bool Const> sentinel

        **Member Types**

        .. type:: private Base = std::conditional_t<Const, const V, V>

        **Special Members**

        .. function:: sentinel() = default
        .. function:: constexpr explicit sentinel(std::ranges::sentinel_t<Base> end)

        .. function:: constexpr sentinel(sentinel<!Const> other) 
        
            **Requires:** `Const && std::convertible_to<std::ranges::sentinel_t<V>, std::ranges::sentinel_t<Base>>`

            Const-converting constructor.

        **Member Functions**

        .. function:: constexpr std::ranges::sentinel_t<Base> base() const

            Retrieve the base sentinel.

        **Friend Functions**

        .. function:: friend constexpr bool operator==(const iterator<Const>& x, const sentinel& y)
        .. function:: friend constexpr std::ranges::range_difference_t<Base> operator-(const iterator<Const>& x, const sentinel& y) 
                      friend constexpr std::ranges::range_difference_t<Base> operator-(const sentinel& x, const iterator<Const>& y) 
            
            **Requires:** `std::sized_sentinel_for<std::ranges::sentinel_t<Base>, std::ranges::iterator_t<Base>>`

    .. class:: template <bool Const> iterator

        **Member Types**

        .. type:: private Base = std::conditional_t<Const, const V, V>
        .. type:: private count_type = std::conditional_t<std::ranges::sized_range<V>, std::ranges::range_size_t<V>, std::make_unsigned_t<std::ranges::range_difference_t<V>>>;
        .. type:: iterator_category = typename std::iterator_traits<std::ranges::iterator_t<Base>>::iterator_category
        .. type:: reference = std::pair<count_type, std::ranges::range_reference_t<Base>>;
        .. type:: value_type = std::pair<count_type, std::ranges::range_value_t<Base>>
        .. type:: difference_type = std::ranges::range_difference_t<Base>

        **Special Members**

        .. function:: iterator() = default

            Construct an iterator not tied to a base iterator.

        .. function:: constexpr explicit iterator(std::ranges::iterator_t<Base> current, difference_type pos)

            Construct an iterator wrapping the given base iterator at the given index.

        .. function:: constexpr iterator(iterator<!Const> i) 

            **Requires**: `Const && std::convertible_to<std::ranges::iterator_t<V>, std::ranges::iterator_t<Base>>`
            
            Const-converting constructor.
 
        **Member Functions**

        .. function:: constexpr std::ranges::iterator_t<Base> base() const&

            **Requires:** `std::copyable<std::ranges::iterator_t<Base>>`
            
            Retrieve the base iterator.

        .. function:: constexpr std::ranges::iterator_t<Base> base() && 

            Retrieve the base iterator.

        .. function:: constexpr reference operator*() const

            Retrieve a pair of the current index and element.

        .. function:: constexpr reference operator[](difference_type x) const

            **Requires:** `std::ranges::random_access_range<Base>`

            Retrieve the pair of the index and element at an offset of `x`.

        .. function:: constexpr iterator& operator++()
        .. function:: constexpr void operator++(int)

            **Requires:** `!std::ranges::forward_range<Base>`

        .. function:: iterator operator++(int)

            **Requires:** `std::ranges::forward_range<Base>`

        .. function:: constexpr iterator& operator--()
                      constexpr iterator operator--(int)

            **Requires:** `std::ranges::bidirectional_range<Base>`

        .. function:: constexpr iterator& operator+=(difference_type x)
                      constexpr iterator& operator-=(difference_type x)

            **Requires:** `std::ranges::random_access_range<Base>`

        **Friend Functions**

        .. function:: friend constexpr bool operator==(const iterator& x, const iterator& y)

            **Requires:** `std::equality_comparable<std::ranges::iterator_t<Base>>`
        
        .. function:: friend constexpr bool operator<(const iterator& x, const iterator& y)
                      friend constexpr bool operator>(const iterator& x, const iterator& y)
                      friend constexpr bool operator<=(const iterator& x, const iterator& y)
                      friend constexpr bool operator>=(const iterator& x, const iterator& y)

            **Requires:** `std::ranges::random_access_range<Base>`

        .. function:: friend constexpr auto operator<=>(const iterator& x, const iterator& y)

            **Requires:** `std::ranges::random_access_range<Base> && std::three_way_comparable<std::ranges::iterator_t<Base>>`

        .. function:: friend constexpr iterator operator+(const iterator& x, difference_type y)
                      friend constexpr iterator operator+(difference_type x, const iterator& y)
                      friend constexpr iterator operator-(const iterator& x, difference_type y)
                      friend constexpr iterator operator-(difference_type x, const iterator& y)
            
            **Requires:** `std::ranges::random_access_range<Base>`

    **Special Members**

    .. function:: enumerate_view() = default
    .. function:: enumerate_view(V base)

    **Member Functions**

    .. function:: constexpr iterator<false> begin()

        **Requires:** `!simple_view<V>`

    .. function:: constexpr iterator<true> begin() const

        **Requires:** `simple_view<V>`

    .. function:: constexpr sentinel<false> end()
    .. function:: constexpr iterator<false> end()

        **Requires:** `std::ranges::common_range<V>&& std::ranges::sized_range<V>`

    .. function:: constexpr sentinel<true> end() const
    .. function:: constexpr iterator<true> end() const

        **Requires:** `std::ranges::common_range<V>&& std::ranges::sized_range<V>`

    .. function:: constexpr std::ranges::size_t<V> size() 
    
        **Requires:** `std::ranges::sized_range<V>`

    .. function:: constexpr std::ranges::size_t<const V> size() 
    
        **Requires:** `std::ranges::sized_range<const V>`

    .. function:: constexpr V base() const& 
    
        **Requires:** `std::copy_constructible<V>`

    .. function:: constexpr V base() && 

.. class:: tl::views::detail::enumerate_fn

    .. function:: template <class V> constexpr tl::enumerate_view<deduced> operator()(V&& v) const
                  template <class V> friend constexpr auto operator|(V&& v, enumerate_fn)
    
        **Requires:** `std::ranges::viewable_range<V>`

        Create a `tl::enumerate_view` from the given range.

.. var:: constexpr inline tl::views::detail::enumerate_fn enumerate

    Instance of `tl::views::detail::enumerate_fn` to allow piping, e.g.: ::

        for (auto&& [index, item] : v | tl::views::enumerate) {
            //...
        }
  