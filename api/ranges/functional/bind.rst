bind
====

.. var:: constexpr inline auto tl::bind_back

    .. function:: template <class F, class... Args> constexpr auto operator()(F f, Args&&... args) const

        Binds the last `sizeof...(Args)` arguments of `f` to `args...` such that `bind_back(f, args...)(more_args...)` is equivalent to `f(more_args..., args...)`.
