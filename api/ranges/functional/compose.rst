compose
=======

.. var:: constexpr inline auto tl::compose

    .. function:: template <class F, class G> constexpr auto operator()(F f, G g) const

        Composes `f` and `g` into a new function such that `compose(f,g)(args...)` is equivalent to `f(g(args...))`.
