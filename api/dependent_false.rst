dependent_false
===============

`Source code <https://github.com/TartanLlama/tl/blob/master/include/tl/dependent_false.hpp>`_

A `static_assert` helper.

.. cpp:struct:: template<class T> tl::dependent_false : std::false_type

    Always false, but dependent on a template parameter, so can be used
    in `static_asserts` which you want to always fail.

    Example: ::

        template <class T> void f(std::vector<T>){
            // ...
        }

        template <class T> void f(T) {
            static_assert(false, "T must be a specialization of std::vector");
        }

    The above code is ill-formed, no diagnostic required due to 
    `[temp.res]/8.1 <http://eel.is/c++draft/temp#res-8.1>`_:

        The program is ill-formed, no diagnostic required, if: 
        
        - no valid specialization can be generated for a template [...]

    One can get around this using `dependent_false`: ::

        template <class T> void f(std::vector<T>){
            // ...
        }

        template <class T> void f(T) {
            static_assert(tl::dependent_false<T>::value, "T must be a specialization of std::vector");
        }