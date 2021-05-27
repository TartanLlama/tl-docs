to
==

Converts a range into a container.

::

    std::list<int> l;
    std::map<int, int> m;

    // copy a list to a vector of the same type
    auto a = tl::to<std::vector<int>>(l);

    //Specify an allocator
    auto b = tl::to<std::vector<int, Alloc>>(l, alloc);

    // copy a list to a vector of the same type, deducing value_type
    auto c = tl::to<std::vector>(l);

    // copy to a container of types ConvertibleTo
    auto d = tl::to<std::vector<long>>(l);

    //Supports converting associative container to sequence containers
    auto f = tl::to<vector>(m); //std::vector<std::pair<int,int>>

    //Supports converting sequence containers to associative ones
    auto g = tl::to<map>(f); //std::map<int,int>

    //Pipe syntax
    auto g = l | ranges::view::take(42) | tl::to<std::vector>();

    //Pipe syntax with allocator
    auto h = l | ranges::view::take(42) | tl::to<std::vector>(alloc);

    //The pipe syntax also support specifying the type and conversions
    auto i = l | ranges::view::take(42) | tl::to<std::vector<long>>();

    // Nested ranges
    std::list<std::forward_list<int>> lst = {{0, 1, 2, 3}, {4, 5, 6, 7}};
    auto vec1 = tl::to<std::vector<std::vector<int>>>(lst);
    auto vec2 = tl::to<std::vector<std::deque<double>>>(lst); 


