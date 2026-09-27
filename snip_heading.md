# Generic skeleton

```cpp
// <-------------------------------------------Libraries------------------------------------>
#include <iostream>
#include <cstdio>
#include <cstring>
#include <cmath>
#include <algorithm>
#include <vector>
#include <set>
#include <map>
#include <unordered_map>
#include <unordered_set>
#include <queue>
#include <stack>
#include <bitset>
#include <list>
#include <string>
#include <utility>
#include <cassert>
#include <limits>
#include <numeric>
#include <functional>
#include <iomanip>
#include <sstream>
#include <climits>
#include <cstdlib>
#include <ctime>
#include <array>
#include <cstdint>
#include <chrono>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
// <--------------------------------Libraries end------------------------------------------------>

using namespace std;
using namespace __gnu_pbds;

// <------------------------------------Debugging Macros for Conditional Output during Development---------------------------------->
#ifndef ONLINE_JUDGE
    #define debug(x)        cerr << #x << " = " << (x) << "\n"
    #define debug_pair(p)   cerr << #p << " = (" << (p).first << ", " << (p).second << ")\n"
    #define debug_vec(v)    do {                                          \
                             cerr << #v << " = [";                        \
                             for (auto& _e : (v))                        \
                                 cerr << _e << ", ";                      \
                             cerr << "]\n";                               \
                          } while (0)
    #define debug_map(m)    do {                                          \
                             cerr << #m << " = {";                        \
                             for (auto& _kv : (m))                      \
                                 cerr << "(" << _kv.first                \
                                      << ":" << _kv.second << "), ";      \
                             cerr << "}\n";                               \
                          } while (0)
#else
    #define debug(x)        do {} while (0)
    #define debug_pair(p)   do {} while (0)
    #define debug_vec(v)    do {} while (0)
    #define debug_map(m)    do {} while (0)
#endif
// <------------------------------------------------------Debugging ends --------------------------------------------------------->

#define FAST_IO do{ios_base::sync_with_stdio(false);cin.tie(nullptr);cout.tie(nullptr);}while(0)
#define FORI for (int i = 0; i < n; i++)
#define FORJ for (int j = 0; j < n; j++)
#define FOR(a, b, x) for (int a = b; a < x; a++)
#define VOUT for(auto it:nums){ cout << it; }
#define pb emplace_back
#define all(x) x.begin(), x.end()
#define int int64_t
#define ld long double
using i64 = int64_t;
using i128 = __int128_t;
#define lb lower_bound
#define ub upper_bound
#define min_heap priority_queue<int, vector<int>, greater<int>>
#define min_heap_pair priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>>
#define minh_heap_tuple priority_queue<tuple<ll,int,int>,vector<tuple<ll,int,int>>,greater<tuple<ll,int,int>>>
#define py cout<<"YES"<<endl
#define pn cout<<"NO"<<endl
#define endl "\n"
#define ps(x,y) fixed<<setprecision(y)<<x
#define numtobin(n) bitset<32>(n).to_string()
#define vi vector<int>
#define vll vector<long long>
#define vvi vector<vector<int>>
#define vb vector<bool>
#define vc vector<char>
#define vs vector<string>
#define pii pair<int,int>
#define vpii vector<pair<int,int>>
#define si set<int>
#define ff first
#define ss second
#define POPCOUNT(x) (__builtin_popcountll(x)) // counts number of 1 / set bits in x 
#define CLZ(x) (__builtin_clzll(x))           // counts leading 0s in x (before first 1 from MSB)
#define CTZ(x) (__builtin_ctzll(x))           // counts trailing 0s in x (after last 1 from LSB)
using ll = long long;
const ll mod = 1e9 + 7;
const int INF = 1e15;

// <-------------------------Modular Arithmetic Utility Functions-------------------------------->
ll mod_pow(ll a, ll b, ll m = mod) {
    ll res = 1;
    while (b) {
        if (b & 1) res = (res * a) % m;
        a = (a * a) % m;
        b >>= 1;
    }
    return res;
}

ll mod_inv(ll a, ll m = mod) {
    return mod_pow(a, m - 2, m);
}

ll mod_add(ll a, ll b, ll m = mod) {
    return ((a % m + b % m) % m + m) % m;
}

ll mod_sub(ll a, ll b, ll m = mod) {
    return ((a % m - b % m) % m + m) % m;
}

ll mod_mul(ll a, ll b, ll m = mod) {
    return ((a % m) * (b % m)) % m;
}

ll mod_div(ll a, ll b, ll m = mod) {
    return mod_mul(a, mod_inv(b, m), m);
}
// <-----------------------------------Predefined Functions-------------------------------------------------------->

bool isPrime(ll n) {
    if (n <= 1) return false;
    for (ll i = 2; i * i <= n; ++i)
        if (n % i == 0) return false;
    return true;
}

vector<ll> primefactors(ll n) {
    vector<ll> fac;
    for (ll x = 2; x * x <= n; ++x) {
        while (n % x == 0) {
            fac.pb(x);
            n /= x;
        }
    }
    if (n > 1) fac.pb(n);
    return fac;
}

ll gcd(ll a, ll b) {
    return b ? gcd(b, a % b) : a;
}

ll lcm(ll a, ll b) {
    return (a / gcd(a, b)) * b;
}

bool isPowerOfTwo(ll n) {
    return n > 0 && (n & (n - 1)) == 0;
}

bool isPerfectSquare(ll x) {
    if (x < 0) return false;
    ll r = sqrtl(x);
    return r * r == x;
}

vector<bool> SieveOfEratosthenes(ll n) {
    vector<bool> prime(n + 1, true);
    prime[0] = prime[1] = false;
    for (ll p = 2; p * p <= n; ++p) {
        if (prime[p]) {
            for (ll i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
    return prime;
}

// <----------------------------------------Templates------------------------------------------------>
template <typename T>
T floor(T a, T b) {
    return a / b - (a % b && (a ^ b) < 0);
}
template <typename T>
T ceil(T x, T y) {
    return floor(x + y - 1, y);
}
template <typename T>
bool has_kth_bit(T x, int k) {
    return x >> k & 1;
}
template <typename T>
struct Compare {
    bool operator()(const pair<T, T>& p1, const pair<T, T>& p2) {
        if (p1.first == p2.first) {
            return p1.second > p2.second;
        }
        return p1.first > p2.first;
    }
};
// <---------------------------------------Templates end------------------------------------------------>
// Ordered Set
// Use find_by_order(k) to get an iterator to the k-th (0-indexed) smallest element
// Use order_of_key(k) to get count of elements < x
template <typename T>
using ordered_set = tree<
T,
null_type,
less<T>,
rb_tree_tag,
tree_order_statistics_node_update>;

// Custom hash function
struct custom_hash {
    static uint64_t splitmix64(uint64_t x) noexcept {
        x += 0x9e3779b97f4a7c15ULL;
        x = (x ^ (x >> 30)) * 0xbf58476d1ce4e5b9ULL;
        x = (x ^ (x >> 27)) * 0x94d049bb133111ebULL;
        return x ^ (x >> 31);
    }

    // base uint64_t entrypoint
    size_t operator()(uint64_t x) const noexcept {
        static const uint64_t FIXED_RANDOM =
            chrono::steady_clock::now().time_since_epoch().count();
        return (size_t)splitmix64(x + FIXED_RANDOM);
    }

    // generic fallback for types that have std::hash<T>
    template<typename T>
    size_t operator()(const T &x) const noexcept {
        return (*this)(static_cast<uint64_t>(std::hash<T>{}(x)));
    }

    // pair<K,V> overload (so pair<int,int> works even though std::hash<pair<..>> is not standard)
    template<typename A, typename B>
    size_t operator()(const pair<A,B> &p) const noexcept {
        uint64_t h1 = uint64_t(std::hash<A>{}(p.first));
        uint64_t h2 = uint64_t(std::hash<B>{}(p.second));
        // combine like boost::hash_combine, then feed to splitmix
        uint64_t combined = h1 ^ (h2 + 0x9e3779b97f4a7c15ULL + (h1<<6) + (h1>>2));
        return (*this)(combined);
    }
};

template<typename K, typename V>
using umap = unordered_map<K, V, custom_hash>;
// <---------------------------------------Templates end------------------------------------------------>

// Problem Statement :
/*
   
*/

// Observation :
/*
   
*/

// Claims on the solution : 
/*  
   
*/

void solve() {

$2

}

int32_t main() {

// #ifndef ONLINE_JUDGE
// freopen("input.txt", "r", stdin);
// freopen("output.txt", "w", stdout);
// #endif

    FAST_IO;
    int t;
    t = 1;
    cin >> t;
    while (t--) {
        solve();
    }
    return 0;
}
```

# Precomputing nCr when I need to return modulo mod answer
```cpp
vector<Mint> fact, invfact;
int fact_computed = 0;

// Precomputing factorials up to n
void precompute(int n) {
    if (n <= fact_computed) return; 
    fact.assign(n + 1, Mint(0));
    invfact.assign(n + 1, Mint(0));
    
    fact[0] = Mint(1);
    for (int i = 1; i <= n; i++) {
        fact[i] = fact[i - 1] * Mint(i);
    }

    invfact[n] = inv(fact[n]);
    for (int i = n - 1; i >= 0; i--) {
        invfact[i] = invfact[i + 1] * Mint(i + 1);
    }
    fact_computed = n;
}

// nCr function 
Mint nCr(long long n, long long r) {
    if (r < 0 || r > n) return Mint(0);
    if (n > fact_computed) precompute(n);
    return fact[n] * invfact[r] * invfact[n - r];
}

// Multinomial Coefficient :
// Computes x! / (y1! * y2! * ... * ym!) % mod
Mint multi(int x, const vector<int> &y) {
    Mint res = fact[x];
    for (int p : y) {
        res = res * invfact[p];
    }
    return res;
}
```


# To find the nCr
```cpp
// nCr function
// Time Complexity : O(r)
long long nCr(int n, int r) {
    long long res = 1;
    for (int i = 0; i < r; i++) {
        res *= (n - i);
        res /= (i + 1);
    }
    return res;
}
```

# Disjoint Set Union (Union-Find)
```cpp
// Disjoint Set Union (Union - Find)
// Helps join two groups and find the parent (representative) of a group fast.
class DSU {
    vector<int> parent, size, rank, maxElement, minElement;

public:
    DSU(int n) {
        for(int i = 0; i < n + 1; i++) {
            size.push_back(1);
            parent.push_back(i);
            rank.push_back(0);
            maxElement.push_back(i);
            minElement.push_back(i);
        }
    }

    // Finds the parent of this node using path compression.
    // Amortized Time : O(α(n)) ≈ O(1)
    int findParent(int node) {
        if (parent[node] == node) {
            return node;
        }
        return parent[node] = findParent(parent[node]);
    }

    // Join two groups using size (attach smaller group to bigger group).
    // Amortized Time : O(α(n)) ≈ O(1)
    void unionSize(int u, int v) {
        int pu = findParent(u);
        int pv = findParent(v);

        
        if (pu == pv) return;
        
        if (size[pu] < size[pv]) {
            parent[pu] = pv;
            maxElement[pv] = max(maxElement[pu], maxElement[pv]);
            minElement[pv] = min(minElement[pu], minElement[pv]);
            size[pv] += size[pu];
        } else {
            maxElement[pu] = max(maxElement[pu], maxElement[pv]);
            minElement[pu] = min(minElement[pu], minElement[pv]);
            parent[pv] = pu;
            size[pu] += size[pv];
        }
    }

    // Join two groups using rank.
    // Amortized Time : O(α(n)) ≈ O(1)
    void unionRank(int u, int v) {
        int pu = findParent(u);
        int pv = findParent(v);

        if (pu == pv) return;

        if (rank[pu] == rank[pv]) {
            parent[pu] = pv;
            rank[pu]++;
        }
        else if (rank[pu] < rank[pv]) {
            parent[pu] = pv;
        }
        else {
            parent[pv] = pu;
        }
    }

    // To find the size of the component of any vertex u, use its parent not the vertex u itself.
    int findSize(int n) {
        return size[n];
    }
    int findMax(int n) {
        return maxElement[n];
    }
    int findMin(int n) {
        return minElement[n];
    }
};
```

# Modular Int Operations
```cpp
/*
    Modular Arithmetic Operations (ModInt)
    Source :
        - https://github.com/bqi343/cp-notebook/blob/master/Implementations/content/number-theory%20(11.1)/Modular%20Arithmetic/ModInt.h
*/

#pragma once
const int mod = 1e9 + 7; // 998244353
// primitive root for FFT (if you need it)
const int primitive_root = 5;

struct Mint {
    int x;
    explicit operator int() const { return x; }
    Mint(): x(0) {}
    Mint(long long y) {
        x = int((-mod < y && y < mod) ? y : y % mod);
        if (x < 0) x += mod;
    }
    bool operator==(const Mint& o) const { return x == o.x; }
    friend bool operator!=(const Mint& a, const Mint& b) { return !(a == b); }
    friend bool operator<(const Mint& a, const Mint& b) { return a.x < b.x; }

    // Addition assignment (modular)
    // Time Complexity: O(1)
    Mint& operator+=(const Mint& o) {
        if ((x += o.x) >= mod) x -= mod;
        return *this;
    }

    // Subtraction assignment (modular)
    // Time Complexity: O(1)
    Mint& operator-=(const Mint& o) {
        if ((x -= o.x) < 0) x += mod;
        return *this;
    }

    // Multiplication assignment (modular)
    // Time Complexity: O(1)
    Mint& operator*=(const Mint& o) {
        x = int((long long)x * o.x % mod);
        return *this;
    }

    // Division assignment (modular): multiply by inverse
    // Time Complexity: O(log mod) due to pow in inv
    Mint& operator/=(const Mint& o) { return (*this) *= inv(o); }

    // Fast exponentiation: a^p (p >= 0)
    // Time Complexity: O(log p)
    friend Mint pow(Mint a, long long p) {
        assert(p >= 0);
        Mint ans = 1;
        while (p > 0) {
            if (p & 1) {
                ans *= a;
            }
            a *= a;
            p >>= 1;
        }
        return ans;
    }

    // Multiplicative inverse using Fermat (mod must be prime)
    // Time Complexity: O(log mod)
    friend Mint inv(const Mint& a) {
        assert(a.x != 0);
        return pow(a, mod - 2);
    }
    Mint operator-() const { return Mint(-x); }
    Mint& operator++() { return *this += 1; }
    Mint& operator--() { return *this -= 1; }
    friend Mint operator+(Mint a, const Mint& b) { return a += b; }
    friend Mint operator-(Mint a, const Mint& b) { return a -= b; }
    friend Mint operator*(Mint a, const Mint& b) { return a *= b; }
    friend Mint operator/(Mint a, const Mint& b) { return a /= b; }
    friend ostream &operator<<(ostream &out, const Mint &a) {
        return out << a.x;
    }
};

// small combinations table (nCk mod mod)
// scmb[n][k] == C(n,k) as modular integers
vector<vector<Mint>> scmb; // small combinations table

// Build Pascal's triangle up to n - 1
// Time Complexity: O(n^2)
void genComb(int n) {
    scmb.assign(n, vector<Mint>(n));
    if (n <= 0) return;
    scmb[0][0] = Mint(1);
    for (int i = 1; i < n; i++) {
        for (int j = 0; j <= i; j++) {
            Mint left = scmb[i - 1][j];
            Mint right = Mint(0);
            if (j > 0) {
                right = scmb[i - 1][j - 1];
            }
            scmb[i][j] = left + right;
        }
    }
}
```

# Snippet for debugging
```cpp
// <------------------------------------Debugging Macros for Conditional Output during Development---------------------------------->
#ifndef ONLINE_JUDGE
    #define debug(x)        cerr << #x << " = " << (x) << "\n"
    #define debug_pair(p)   cerr << #p << " = (" << (p).first << ", " << (p).second << ")\n"
    #define debug_vec(v)    do {                                          \
                             cerr << #v << " = [";                        \
                             for (auto& _e : (v))                        \
                                 cerr << _e << ", ";                      \
                             cerr << "]\n";                               \
                          } while (0)
    #define debug_map(m)    do {                                          \
                             cerr << #m << " = {";                        \
                             for (auto& _kv : (m))                      \
                                 cerr << "(" << _kv.first                \
                                      << ":" << _kv.second << "), ";      \
                             cerr << "}\n";                               \
                          } while (0)
#else
    #define debug(x)        do {} while (0)
    #define debug_pair(p)   do {} while (0)
    #define debug_vec(v)    do {} while (0)
    #define debug_map(m)    do {} while (0)
#endif
// <------------------------------------------------------Debugging ends --------------------------------------------------------->
```

# Modular Functions
```cpp
long long mod_pow(long long a, long long b, long long m = mod) {
    long long res = 1;
    while (b) {
        if (b & 1) res = (res * a) % m;
        a = (a * a) % m;
        b >>= 1;
    }
    return res;
}

long long mod_inv(long long a, long long m = mod) {
    return mod_pow(a, m - 2, m);
}

long long mod_add(long long a, long long b, long long m = mod) {
    return ((a % m + b % m) % m + m) % m;
}

long long mod_sub(long long a, long long b, long long m = mod) {
    return ((a % m - b % m) % m + m) % m;
}

long long mod_mul(long long a, long long b, long long m = mod) {
    return ((a % m) * (b % m)) % m;
}

long long mod_div(long long a, long long b, long long m = mod) {
    return mod_mul(a, mod_inv(b, m), m);
}
```


Safe hash map to avoid collisions
```cpp
// Custom hash function
struct custom_hash {
    static uint64_t splitmix64(uint64_t x) noexcept {
        x += 0x9e3779b97f4a7c15ULL;
        x = (x ^ (x >> 30)) * 0xbf58476d1ce4e5b9ULL;
        x = (x ^ (x >> 27)) * 0x94d049bb133111ebULL;
        return x ^ (x >> 31);
    }

    // base uint64_t entrypoint
    size_t operator()(uint64_t x) const noexcept {
        static const uint64_t FIXED_RANDOM =
            chrono::steady_clock::now().time_since_epoch().count();
        return (size_t)splitmix64(x + FIXED_RANDOM);
    }

    // generic fallback for types that have std::hash<T>
    template<typename T>
    size_t operator()(const T &x) const noexcept {
        return (*this)(static_cast<uint64_t>(std::hash<T>{}(x)));
    }

    // pair<K,V> overload (so pair<int,int> works even though std::hash<pair<..>> is not standard)
    template<typename A, typename B>
    size_t operator()(const pair<A,B> &p) const noexcept {
        uint64_t h1 = uint64_t(std::hash<A>{}(p.first));
        uint64_t h2 = uint64_t(std::hash<B>{}(p.second));
        // combine like boost::hash_combine, then feed to splitmix
        uint64_t combined = h1 ^ (h2 + 0x9e3779b97f4a7c15ULL + (h1<<6) + (h1>>2));
        return (*this)(combined);
    }
};

template<typename K, typename V>
using umap = unordered_map<K, V, custom_hash>;
```

# For problems dealing with mex
```cpp
struct Mex {
    set<int> missing;               // Stores all potential mex values
    unordered_map<int, int> freq;   // Frequency of each element in the current set

    // Initialize with numbers from 0 to n + 1 -> O(n log n) time taken.
    Mex(int n) {
        for (int i = 0; i <= n + 1; i++) 
            missing.insert(i);
    }

    // Add an element to the set
    void add(int x) {
        if (++freq[x] == 1)          
            missing.erase(x);        // Remove from potential mex
    }

    // Remove an element from the set
    void remove(int x) {
        if (--freq[x] == 0)       
            missing.insert(x);       // Reinsert into potential mex
    }

    // Get current mex
    int get() const {
        return *missing.begin();
    }
};
```


# Kruskal's Minimum Spanning Tree
```cpp
/*
Kruskal's Minimum Spanning Tree Using DSU
For the edges vector : Create a vector<vector<int>> and just push back 
{Source, Destination, Weight} for every edge given between two vertices.
Example :
    vector<vector<int>> edges;
    for (...) {
        int u, v, w; 
        cin >> u >> v >> w; 
        edges.push_back({u, v, w})
    }
        
Convert all long doubles to int if you want answer without floating points
*/
vector<vector<int>> mstEdges;

int kruskalMST(int vertexCount, vector<vector<int>> &edges) {
    sort(edges.begin(), edges.end(), [](const vector<int> &a, const vector<int> &b) {
        return a[2] < b[2];
    });

    DSU dsu(vertexCount);
    int totalWeight = 0;
    mstEdges.clear();

    int usedEdges = 0;
    for (auto &e : edges) {
        int u = e[0], v = e[1], w = e[2];
        if (dsu.findParent(u) != dsu.findParent(v)) {
            dsu.unionSize(u, v);
            totalWeight += w;
            mstEdges.push_back(e);
            if (++usedEdges == vertexCount - 1) break;
        }
    }

    return totalWeight;
}
```


# Sieve of Eratosthenes
```cpp
vector<bool> prime;
void SieveOfEratosthenes(long long n) {
    prime = vector<bool>(n + 1, true);
    prime[0] = prime[1] = false;
    for (long long p = 2; p * p <= n; ++p) {
        if (prime[p]) {
            for (long long i = p * p; i <= n; i += p)
                prime[i] = false;
        }
    }
}
```

# PBDS Template
```cpp
// Policy Based Data Structures (PBDS)
#undef int // disables above #define int ll temporarily
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
#include <ext/pb_ds/priority_queue.hpp>
#define int long long

using namespace __gnu_pbds;

// Ordered Set
// Use find_by_order(k) to get an iterator to the k-th (0-indexed) smallest element
// Use order_of_key(k) to get count of elements < x
template <typename T>
using ordered_set = tree<T, null_type, less<T>, rb_tree_tag, tree_order_statistics_node_update>;

// Ordered multiset (allow duplicates) - store (value, unique_id)
// Use emplace({val, unique_id}) and order_of_key({x+1, MIN_ID}) to count <= x
template <typename T>
using ordered_multiset = tree< pair<T,int>, null_type, less<pair<T,int>>, rb_tree_tag, tree_order_statistics_node_update>;

// Ordered map (order statistics on keys)
// Use find_by_order(k) to get k-th key; order_of_key(key) counts keys < key
template <typename Key, typename Mapped>
using ordered_map = tree< Key, Mapped, less<Key>, rb_tree_tag, tree_order_statistics_node_update>;

// gp_hash_table (fast hash map) - similar API to unordered_map
// Example: gp_hash_table<long long,int> gph;
template <typename K, typename V>
using gp_hash_table = cc_hash_table<K, V>;

/*
Quick usage notes:
    - ordered_set<int> os; os.insert(x); os.order_of_key(x); os.find_by_order(k);
    - ordered_multiset<long long> oms; int uid=0; oms.insert({val, uid++}); oms.order_of_key({val+1, PAIR_MIN});
    - ordered_map<Key,Value> om; om.insert({k,v}); om.order_of_key(k);
    - gp_hash_table<K,V> gph; gph.emplace(k,v); gph.find(k);
*/
```

# Miller Rabin Primality Test
```cpp
// Miller-Rabin Primality Test [Deterministic for 64-bit numbers]
// Time Complexity: O(log n)
int binpower(int base, int e, int mod) { 
    int result = 1;
    base %= mod;
    while (e) {
        if (e & 1)
            result = (__int128_t)result * base % mod;
        base = (__int128_t)base * base % mod;
        e >>= 1;
    }
    return result;
}

bool check_composite(int n, int a, int d, int s) {
    int x = binpower(a, d, n);
    if (x == 1 || x == n - 1)
        return false;
    for (int r = 1; r < s; r++) {
        x = (__int128_t)x * x % n;
        if (x == n - 1)
            return false;
    }
    return true;
};

bool MillerRabin(int n) { // returns true if n is prime, else returns false.
    if (n < 2)
        return false;

    int r = 0;
    int d = n - 1;
    while ((d & 1) == 0) {
        d >>= 1;
        r++;
    }

    for (int a : {2, 3, 5, 7, 11, 13, 17, 19, 23, 29, 31, 37}) {
        if (n == a)
            return true;
        if (check_composite(n, a, d, r))
            return false;
    }
    return true;
}
```

# Mobius Function Computation
```cpp
// Möbius Function Computation
// Time Complexity: O(n log log n)
void computeMobius(int n, vector<int>& mu) {
    vector<int> is_prime(n + 1, 1);
    mu[0] = 0;
    mu[1] = 1;

    for (int i = 2; i <= n; ++i) {
        if (is_prime[i]) {
            for (int j = i; j <= n; j += i) {
                mu[j] *= -1;
                is_prime[j] = 0;
            }

            for (int j = i * i; j <= n; j += i * i) {
                mu[j] = 0; 
            }
        }
    }
}
```


# Segment Tree for sum queries
```cpp
// Segment Tree (Range Sum)
// Used to perform Range Sum Queries, range add updates using lazy propogation.
class SegmentTree_Sum {
public:
    int n;
    vector<long long> tree, lazy;

    SegmentTree_Sum(int n) : n(n) {
        tree.assign(4 * n, 0);
        lazy.assign(4 * n, 0);
    }

    // For building the tree from an array 
    // Time Complexity: O(n)
    void build(const vector<long long> &a, int node, int start, int end) {
        if (start == end) {
            tree[node] = a[start];
            return;
        }
        int mid = (start + end) / 2;
        build(a, node * 2, start, mid);
        build(a, node * 2 + 1, mid + 1, end);
        tree[node] = tree[node * 2] + tree[node * 2 + 1];
    }

    // Used for applying a lazy update to a node
    // Time Complexity: O(1)
    void apply(int node, int start, int end, long long val) {
        tree[node] += 1LL * (end - start + 1) * val;
        lazy[node] += val;
    }

    // Used for pushing pending lazy updates to children
    // Time Complexity: O(1)
    void push(int node, int start, int end) {
        if (lazy[node] == 0) return;
        int mid = (start + end) / 2;
        apply(node * 2, start, mid, lazy[node]);
        apply(node * 2 + 1, mid + 1, end, lazy[node]);
        lazy[node] = 0;
    }

    // Used for updating range [l, r] by adding val
    // Time Complexity: O(log n)
    void updateRange(int node, int start, int end, int l, int r, long long val) {
        if (l > r) return;
        if (l == start && r == end) {
            apply(node, start, end, val);
            return;
        }
        push(node, start, end);
        int mid = (start + end) / 2;
        updateRange(node * 2, start, mid, l, min(r, mid), val);
        updateRange(node * 2 + 1, mid + 1, end, max(l, mid + 1), r, val);
        tree[node] = tree[node * 2] + tree[node * 2 + 1];
    }

    // Used for finding Range Sum in [l, r]
    // Time Complexity: O(log n)
    long long query(int node, int start, int end, int l, int r) {
        if (l > r) return 0;
        if (l == start && r == end) return tree[node];
        push(node, start, end);
        int mid = (start + end) / 2;
        return query(node * 2, start, mid, l, min(r, mid))
             + query(node * 2 + 1, mid + 1, end, max(l, mid + 1), r);
    }
};
```


# 2nd Segment Tree
```cpp
class SegmentTree_Sum {
public:
    int n;
    vector<long long> tree, lazy_add, lazy_set;
    vector<bool> has_set;

    SegmentTree_Sum(int n) : n(n) {
        tree.assign(4 * n, 0);
        lazy_add.assign(4 * n, 0);
        lazy_set.assign(4 * n, 0);
        has_set.assign(4 * n, false);
    }

    void build(const vector<long long> &a, int node, int start, int end) {
        if (start == end) {
            tree[node] = a[start];
            return;
        }
        int mid = (start + end) / 2;
        build(a, node * 2, start, mid);
        build(a, node * 2 + 1, mid + 1, end);
        tree[node] = tree[node * 2] + tree[node * 2 + 1];
    }

    void apply_add(int node, int start, int end, long long val) {
        if (has_set[node]) lazy_set[node] += val;
        else lazy_add[node] += val;
        tree[node] += 1LL * (end - start + 1) * val;
    }

    void apply_set(int node, int start, int end, long long val) {
        tree[node] = 1LL * (end - start + 1) * val;
        lazy_set[node] = val;
        lazy_add[node] = 0;
        has_set[node] = true;
    }

    void push(int node, int start, int end) {
        if (start == end) return;
        int mid = (start + end) / 2;
        if (has_set[node]) {
            apply_set(node * 2, start, mid, lazy_set[node]);
            apply_set(node * 2 + 1, mid + 1, end, lazy_set[node]);
            has_set[node] = false;
        }
        if (lazy_add[node] != 0) {
            apply_add(node * 2, start, mid, lazy_add[node]);
            apply_add(node * 2 + 1, mid + 1, end, lazy_add[node]);
            lazy_add[node] = 0;
        }
    }

    void updateAdd(int node, int start, int end, int l, int r, long long val) {
        if (r < start || end < l) return;
        if (l <= start && end <= r) {
            apply_add(node, start, end, val);
            return;
        }
        push(node, start, end);
        int mid = (start + end) / 2;
        updateAdd(node * 2, start, mid, l, r, val);
        updateAdd(node * 2 + 1, mid + 1, end, l, r, val);
        tree[node] = tree[node * 2] + tree[node * 2 + 1];
    }

    void updateSet(int node, int start, int end, int l, int r, long long val) {
        if (r < start || end < l) return;
        if (l <= start && end <= r) {
            apply_set(node, start, end, val);
            return;
        }
        push(node, start, end);
        int mid = (start + end) / 2;
        updateSet(node * 2, start, mid, l, r, val);
        updateSet(node * 2 + 1, mid + 1, end, l, r, val);
        tree[node] = tree[node * 2] + tree[node * 2 + 1];
    }

    long long queryRange(int node, int start, int end, int l, int r) {
        if (r < start || end < l) return 0;
        if (l <= start && end <= r) return tree[node];
        push(node, start, end);
        int mid = (start + end) / 2;
        return queryRange(node * 2, start, mid, l, r)
             + queryRange(node * 2 + 1, mid + 1, end, l, r);
    }
};
```


# Segment Tree for min queries
```cpp
// Segment Tree (Range Min)
// Used to perform Range Min Queries and updates.
class SegmentTree_Min {
public:
    int n;
    vector<long long> tree;

    SegmentTree_Min(int n) : n(n) {
        tree.assign(4 * n, 1e18);
    }

    // Build the tree from an array
    // Time Complexity: O(n)
    void build(const vector<long long> &a, int node, int start, int end) {
        if (start == end) {
            tree[node] = a[start];
            return;
        }
        int mid = (start + end) / 2;
        build(a, node * 2, start, mid);
        build(a, node * 2 + 1, mid + 1, end);
        tree[node] = min(tree[node * 2], tree[node * 2 + 1]);
    }

    // Point update: set position idx to val
    // Time Complexity: O(log n)
    void update(int node, int start, int end, int idx, long long val) {
        if (start == end) {
            tree[node] = val;
            return;
        }
        int mid = (start + end) / 2;
        if (idx <= mid) update(node * 2, start, mid, idx, val);
        else update(node * 2 + 1, mid + 1, end, idx, val);
        tree[node] = min(tree[node * 2], tree[node * 2 + 1]);
    }

    // Query min in range [l, r]
    // Time Complexity: O(log n)
    long long query(int node, int start, int end, int l, int r) {
        if (l > r) return 1e18;
        if (l == start && r == end) return tree[node];
        int mid = (start + end) / 2;
        return min(
            query(node * 2, start, mid, l, min(r, mid)),
            query(node * 2 + 1, mid + 1, end, max(l, mid + 1), r)
        );
    }
};
```


# Segment Tree for max queries
```cpp
// Segment Tree (Range Max)
// Used to perform Range Max Queries and updates.
class SegmentTree_Max {
public:
    int n;
    vector<long long> tree;

    SegmentTree_Max(int n) : n(n) {
        tree.assign(4 * n, -1e18);
    }

    // Build the tree from an array
    // Time Complexity: O(n)
    void build(const vector<long long> &a, int node, int start, int end) {
        if (start == end) {
            tree[node] = a[start];
            return;
        }
        int mid = (start + end) / 2;
        build(a, node * 2, start, mid);
        build(a, node * 2 + 1, mid + 1, end);
        tree[node] = max(tree[node * 2], tree[node * 2 + 1]);
    }

    // Point update: set position idx to val
    // Time Complexity: O(log n)
    void update(int node, int start, int end, int idx, long long val) {
        if (start == end) {
            tree[node] = val;
            return;
        }
        int mid = (start + end) / 2;
        if (idx <= mid) update(node * 2, start, mid, idx, val);
        else update(node * 2 + 1, mid + 1, end, idx, val);
        tree[node] = max(tree[node * 2], tree[node * 2 + 1]);
    }

    // Query max in range [l, r]
    // Time Complexity: O(log n)
    long long query(int node, int start, int end, int l, int r) {
        if (l > r) return -1e18;
        if (l == start && r == end) return tree[node];
        int mid = (start + end) / 2;
        return max(
            query(node * 2, start, mid, l, min(r, mid)),
            query(node * 2 + 1, mid + 1, end, max(l, mid + 1), r)
        );
    }

    int first_greater(int idx, int l, int r, int x) {
        if (tree[idx] < x) return -1;   
        if (l == r) return l;

        int mid = (l + r) / 2;
        if (tree[2 * idx] >= x)
            return first_greater(2 * idx, l, mid, x);
        return first_greater(2 * idx + 1, mid + 1, r, x);
    }
};
```


# Segment Tree for xor queries
```cpp
// Segment Tree (Range XOR)
// Used to perform Range XOR Queries and updates.
class SegmentTree_XOR {
public:
    int n;
    vector<long long> tree;

    SegmentTree_XOR(int n) : n(n) {
        tree.assign(4 * n, 0);
    }

    // Build the tree from an array
    // Time Complexity: O(n)
    void build(const vector<long long> &a, int node, int start, int end) {
        if (start == end) {
            tree[node] = a[start];
            return;
        }
        int mid = (start + end) / 2;
        build(a, node * 2, start, mid);
        build(a, node * 2 + 1, mid + 1, end);
        tree[node] = tree[node * 2] ^ tree[node * 2 + 1];
    }

    // Point update: set position idx to val
    // Time Complexity: O(log n)
    void update(int node, int start, int end, int idx, long long val) {
        if (start == end) {
            tree[node] = val;
            return;
        }
        int mid = (start + end) / 2;
        if (idx <= mid) update(node * 2, start, mid, idx, val);
        else update(node * 2 + 1, mid + 1, end, idx, val);
        tree[node] = tree[node * 2] ^ tree[node * 2 + 1];
    }

    // Query XOR in range [l, r]
    // Time Complexity: O(log n)
    long long query(int node, int start, int end, int l, int r) {
        if (l > r) return 0;
        if (l == start && r == end) return tree[node];
        int mid = (start + end) / 2;
        return query(node * 2, start, mid, l, min(r, mid))
             ^ query(node * 2 + 1, mid + 1, end, max(l, mid + 1), r);
    }
};
```

# Segment Tree for gcd queries
```cpp
// Segment Tree (Range Gcd)
// Used to perform Range Gcd Queries and updates.
class SegmentTree_GCD {
public:
    int n;
    vector<long long> tree;

    SegmentTree_GCD(int n) : n(n) {
        tree.assign(4 * n, 0); // neutral element = 0
    }

    // Build tree from array
    // Time Complexity: O(n)
    void build(const vector<long long> &a, int node, int start, int end) {
        if (start == end) {
            tree[node] = a[start];
            return;
        }
        int mid = (start + end) / 2;
        build(a, node * 2, start, mid);
        build(a, node * 2 + 1, mid+1, end);
        tree[node] = gcd(tree[node * 2], tree[node * 2 + 1]);
    }

    // Point update: set idx to val
    // Time Complexity: O(log n)
    void update(int node, int start, int end, int idx, long long val) {
        if (start == end) {
            tree[node] = val;
            return;
        }
        int mid = (start + end) / 2;
        if (idx <= mid) update(node * 2, start, mid, idx, val);
        else update(node * 2 + 1, mid + 1, end, idx, val);
        tree[node] = gcd(tree[node * 2], tree[node * 2 + 1]);
    }

    // Query GCD in range [l, r]
    // Time Complexity: O(log n)
    long long query(int node, int start, int end, int l, int r) {
        if (l > r) return 0;
        if (l == start && r == end) return tree[node];
        int mid = (start + end) / 2;
        return std::gcd(
            query(node * 2, start, mid, l, min(r, mid)),
            query(node * 2 + 1, mid + 1, end, max(l, mid + 1), r)
        );
    }
};
```

# Segment Tree for lcm queries
```cpp
// Segment Tree (Range Lcm)
// Used to perform Range Lcm Queries and updates.
class SegmentTree_LCM {
public:
    int n;
    vector<long long> tree;

    SegmentTree_LCM(int n) : n(n) {
        tree.assign(4 * n, 1); // neutral element = 1
    }

    long long lcm(long long a, long long b) {
        if (a == 0 || b == 0) return 0;
        return a / gcd(a, b) * b;
    }

    // Build tree from array
    // Time Complexity: O(n)
    void build(const vector<long long> &a, int node, int start, int end) {
        if (start == end) {
            tree[node] = a[start];
            return;
        }
        int mid = (start + end) / 2;
        build(a, node * 2, start, mid);
        build(a, node * 2 + 1, mid+1, end);
        tree[node] = lcm(tree[node * 2], tree[node * 2 + 1]);
    }

    // Point update: set idx to val
    // Time Complexity: O(log n)
    void update(int node, int start, int end, int idx, long long val) {
        if (start == end) {
            tree[node] = val;
            return;
        }
        int mid = (start + end) / 2;
        if (idx <= mid) update(node * 2, start, mid, idx, val);
        else update(node * 2 + 1, mid + 1, end, idx, val);
        tree[node] = lcm(tree[node * 2], tree[node * 2 + 1]);
    }

    // Query LCM in range [l, r]
    // Time Complexity: O(log n)
    long long query(int node, int start, int end, int l, int r) {
        if (l > r) return 1;
        if (l == start && r == end) return tree[node];
        int mid = (start + end) / 2;
        return lcm(
            query(node*2, start, mid, l, min(r, mid)),
            query(node*2+1, mid+1, end, max(l, mid + 1), r)
        );
    }
};
```


# Segment Tree for or queries
```cpp
// Segment Tree (Range OR)
// Used to perform Range OR Queries and updates.
class SegmentTree_OR {
public:
    int n;
    vector<long long> tree;

    SegmentTree_OR(int n) : n(n) {
        tree.assign(4 * n, 0); // neutral element = 0
    }

    // Build tree from array
    // Time Complexity: O(n)
    void build(const vector<long long> &a, int node, int start, int end) {
        if (start == end) {
            tree[node] = a[start];
            return;
        }
        int mid = (start + end) / 2;
        build(a, node * 2, start, mid);
        build(a, node * 2 + 1, mid + 1, end);
        tree[node] = tree[node * 2] | tree[node * 2 + 1];
    }

    // Point update: set idx to val
    // Time Complexity: O(log n)
    void update(int node, int start, int end, int idx, long long val) {
        if (start == end) {
            tree[node] = val;
            return;
        }
        int mid = (start + end) / 2;
        if (idx <= mid) update(node * 2, start, mid, idx, val);
        else update(node * 2 + 1, mid + 1, end, idx, val);
        tree[node] = tree[node * 2] | tree[node * 2 + 1];
    }

    // Query OR in range [l, r]
    // Time Complexity: O(log n)
    long long query(int node, int start, int end, int l, int r) {
        if (l > r) return 0;
        if (l == start && r == end) return tree[node];
        int mid = (start + end) / 2;
        return query(node * 2, start, mid, l, min(r, mid))
             | query(node * 2 + 1, mid + 1, end, max(l, mid + 1), r);
    }
};
```

# Segment Tree for and queries
```cpp
// Segment Tree (Range AND)
// Used to perform Range AND Queries and updates.
class SegmentTree_AND {
public:
    int n;
    vector<long long> tree;

    SegmentTree_AND(int n) : n(n) {
        tree.assign(4 * n, (1LL << 60) - 1);
    }

    // Build tree from array
    // Time Complexity: O(n)
    void build(const vector<long long> &a, int node, int start, int end) {
        if (start == end) {
            tree[node] = a[start];
            return;
        }
        int mid = (start + end) / 2;
        build(a, node * 2, start, mid);
        build(a, node * 2 + 1, mid+1, end);
        tree[node] = tree[node * 2] & tree[node * 2 + 1];
    }

    // Point update: set idx to val
    // Time Complexity: O(log n)
    void update(int node, int start, int end, int idx, long long val) {
        if (start == end) {
            tree[node] = val;
            return;
        }
        int mid = (start + end) / 2;
        if (idx <= mid) update(node * 2, start, mid, idx, val);
        else update(node * 2 + 1, mid+1, end, idx, val);
        tree[node] = tree[node * 2] & tree[node * 2 + 1];
    }

    // Query AND in range [l, r]
    // Time Complexity: O(log n)
    long long query(int node, int start, int end, int l, int r) {
        if (l > r) return (1LL << 60) - 1;
        if (l == start && r == end) return tree[node];
        int mid = (start + end) / 2;
        return query(node * 2, start, mid, l, min(r, mid))
             & query(node * 2 + 1, mid + 1, end, max(l, mid + 1), r);
    }
};
```

# Used to perform maximum subarray sum queries with point updates.
```cpp
// Segment Tree (Maximum Subarray Sum)
// Used to perform maximum subarray sum queries with point updates.
class SegmentTree_MaxSubarray {
public:
    struct Node {
        long long sum;   // Total sum of segment
        long long pref;  // Maximum prefix sum
        long long suff;  // Maximum suffix sum
        long long ans;   // Maximum subarray sum

        Node(long long val = -(long long)4e18) {
            sum = pref = suff = ans = val;
        }
    };

    int n;
    vector<Node> tree;

    SegmentTree_MaxSubarray(int n) : n(n) {
        tree.assign(4 * n, Node());
    }

    // Used for merging two child nodes
    // Time Complexity: O(1)
    Node merge(Node left, Node right) {
        if (left.sum == -(long long)4e18) return right;
        if (right.sum == -(long long)4e18) return left;

        Node res;
        res.sum  = left.sum + right.sum;
        res.pref = max(left.pref, left.sum + right.pref);
        res.suff = max(right.suff, right.sum + left.suff);
        res.ans  = max({left.ans, right.ans, left.suff + right.pref});
        return res;
    }

    // For building the tree from an array
    // Time Complexity: O(n)
    void build(const vector<long long> &a, int node, int start, int end) {
        if (start == end) {
            tree[node] = Node(a[start]);
            return;
        }
        int mid = (start + end) / 2;
        build(a, node * 2, start, mid);
        build(a, node * 2 + 1, mid + 1, end);
        tree[node] = merge(tree[node * 2], tree[node * 2 + 1]);
    }

    // Used for point update: set index idx to val
    // Time Complexity: O(log n)
    void update(int node, int start, int end, int idx, long long val) {
        if (start == end) {
            tree[node] = Node(val);
            return;
        }
        int mid = (start + end) / 2;
        if (idx <= mid)
            update(node * 2, start, mid, idx, val);
        else
            update(node * 2 + 1, mid + 1, end, idx, val);

        tree[node] = merge(tree[node * 2], tree[node * 2 + 1]);
    }

    // Used for querying maximum subarray sum in range [l, r]
    // Time Complexity: O(log n)
    Node query(int node, int start, int end, int l, int r) {
        if (l > r) return Node();
        if (l == start && r == end)
            return tree[node];

        int mid = (start + end) / 2;
        Node left  = query(node * 2, start, mid, l, min(r, mid));
        Node right = query(node * 2 + 1, mid + 1, end, max(l, mid + 1), r);
        return merge(left, right);
    }
};
```

# Feasible LCM Template to avoid overflow.
```cpp
long long modpow(long long a, long long e, long long mod = 1e9 + 7) {
    long long r = 1;
    while (e) {
        if (e & 1) r = (r * a) % mod;
        a = (a * a) % mod;
        e >>= 1;
    }
    return r;
}

// Computes LCM of all numbers % mod in a feasible manner to avoid overflows of any kind.
// Time Complexity : O(n * sqrt(max_element(A))
long long lcm_mod(const vector<long long>& arr, long long mod = 1e9 + 7) {
    map<long long, long long> max_pow;

    for (long long x : arr) {
        long long n = x;
        for (long long p = 2; p * p <= n; p++) {
            if (n % p == 0) {
                long long cnt = 0;
                while (n % p == 0) {
                    n /= p;
                    cnt++;
                }
                max_pow[p] = max(max_pow[p], cnt);
            }
        }
        if (n > 1) {
            max_pow[n] = max(max_pow[n], 1LL);
        }
    }

    long long ans = 1;
    for (auto &[prime, exp] : max_pow) {
        ans = (ans * modpow(prime % mod, exp)) % mod;
    }
    return ans;
}
```

# Extended GCD/Euclidean Algorithm
```cpp
// Extended GCD/Euclidean Algorithm :
// Its used to :
//  1. Find x, y for eqns where => ax + by = gcd(a, b)
//  2. Solve linear diophantine eqns. ax + by = c, where c is a multiple of gcd(a, b)
//  3. Solve linear congruences like => ax ≡ b (mod m)  
// Time Complexity : O(log n)
long long extendedGCD(long long a, long long b, long long &x, long long &y) {
    if (b == 0) {
        x = 1;
        y = 0;
        return a;
    }
    long long x1, y1;
    long long g = extendedGCD(b, a % b, x1, y1);
    x = y1;
    y = x1 - y1 * (a / b);
    return g;
}
```

# Code for Fenwick Tree or BIT
```cpp
class FenwickTree {
public:
    int n;
    vector<long long> bit; // 0-indexed tree

    FenwickTree(int n) : n(n) {
        bit.assign(n, 0);
    }

    // BIT from an array in O(n)
    void build(const vector<long long> &a) {
        for (int i = 0; i < n; i++) {
            update(i, a[i]); 
        }
    }

    // Point update: add val to index idx (0-indexed)
    // Time Complexity: O(log n)
    void update(int idx, long long val) {
        for (; idx < n; idx = idx | (idx + 1)) {
            bit[idx] += val;
        }
    }

    // Prefix sum query: sum of [0, idx]
    // Time Complexity: O(log n)
    long long query(int idx) {
        long long res = 0;
        for (; idx >= 0; idx = (idx & (idx + 1)) - 1) {
            res += bit[idx];
        }
        return res;
    }

    // Range sum query: sum of [l, r]
    // Time Complexity: O(log n)
    long long query(int l, int r) {
        if (l > r) return 0;
        return query(r) - (l ? query(l - 1) : 0);
    }

    // Lower Bound: first index such that prefix sum >= x
    // Returns n if no such index exists
    // Time Complexity: O(log n)
    int lower_bound(long long x) {
        int idx = -1;
        long long sum = 0;
        for (int i = 31 - __builtin_clz(n); i >= 0; i--) {
            int next = idx + (1 << i);
            if (next < n && sum + bit[next] < x) {
                sum += bit[next];
                idx = next;
            }
        }
        return idx + 1;
    }

    // Point update
    // Supports adding val to index i
    // Time Complexity: O(log n)
    void add(int i, long long val) {
        update(i, val);
    }

    // Range update
    // Supports adding val to range [l, r]
    // Time Complexity: O(log n)
    void add_range(int l, int r, long long val) {
        update(l, val);
        if (r + 1 < n) update(r + 1, -val);
    }
};
```

# Cartesian Tree to perform RMQ
```cpp
class CartesianTree {
public:
    int n, root;
    vector<int> l, r; // nearest greater on left/right
    vector<array<int,2>> adj; // adj[u][0] = left child, adj[u][1] = right child
    vector<vector<int>> up; // binary lifting table for LCA
    vector<int> depth;                      

    CartesianTree(const vector<int> &a) : n(a.size()), l(n), r(n), adj(n, {-1,-1}), depth(n) {
        buildTree(a); // O(n)
        prepareLCA(); // O(n log n)
    }

private:
    // Build the tree using nearest greater element method
    // Time Complexity: O(n)
    void buildTree(const vector<int> &a) {
        for (int i = 0; i < n; i++) {
            l[i] = i - 1;
            while (l[i] >= 0 && a[l[i]] <= a[i]) l[i] = l[l[i]];
        }
        for (int i = n - 1; i >= 0; i--) {
            r[i] = i + 1;
            while (r[i] < n && a[r[i]] < a[i]) r[i] = r[r[i]];
        }
        for (int i = 0; i < n; i++) {
            if (l[i] == -1 && r[i] == n) {
                root = i;
            } else if (l[i] == -1) {
                adj[r[i]][0] = i;
            } else if (r[i] == n) {
                adj[l[i]][1] = i;
            } else if (a[l[i]] <= a[r[i]]) {
                adj[l[i]][1] = i;
            } else {
                adj[r[i]][0] = i;
            }
        }
    }

    // DFS to compute depth and 2^k ancestors for LCA
    // Time Complexity: O(n log n)
    void dfs(int u, int p) {
        up[u][0] = p;
        for (int k = 1; k < (int)up[u].size(); k++) {
            if (up[u][k-1] != -1) up[u][k] = up[up[u][k-1]][k-1];
        }
        for (int c : adj[u]) {
            if (c != -1) {
                depth[c] = depth[u] + 1;
                dfs(c, u);
            }
        }
    }

    // Prepare binary lifting table for LCA queries
    // Time Complexity: O(n log n)
    void prepareLCA() {
        int LOG = 20; // enough for n <= 1e6
        up.assign(n, vector<int>(LOG, -1));
        depth[root] = 0;
        dfs(root, -1);
    }

public:
    // Compute LCA of nodes u and v
    // Time Complexity: O(log n)
    int getLCA(int u, int v) {
        if (depth[u] < depth[v]) swap(u,v);
        int LOG = up[0].size();
        for (int k = LOG-1; k >= 0; k--) {
            if (up[u][k] != -1 && depth[up[u][k]] >= depth[v]) u = up[u][k];
        }
        if (u == v) return u;
        for (int k = LOG-1; k >= 0; k--) {
            if (up[u][k] != -1 && up[u][k] != up[v][k]) {
                u = up[u][k]; v = up[v][k];
            }
        }
        return up[u][0];
    }
};
```

# Trie for getting Min/Max Xors
```cpp
class Trie_Xor {
public:
    struct Node {
        Node* child[2];  // For binary trie (0 and 1)
        bool isEnd;      // Optional, to mark end of a number

        Node() {
            child[0] = child[1] = nullptr;
            isEnd = false;
        }
    };

    Node* root;

    Trie_Xor() {
        root = new Node();
    }

    // Insert a number into the trie
    // Time Complexity: O(LOG)
    void insert(int num, int LOG = 31) {
        Node* node = root;
        for (int i = LOG; i >= 0; i--) {
            int bit = (num >> i) & 1;
            if (!node->child[bit])
                node->child[bit] = new Node();
            node = node->child[bit];
        }
        node->isEnd = true;
    }

    // Check if a number exists in the trie
    // Time Complexity: O(LOG)
    bool search(int num, int LOG = 31) {
        Node* node = root;
        for (int i = LOG; i >= 0; i--) {
            int bit = (num >> i) & 1;
            if (!node->child[bit]) return false;
            node = node->child[bit];
        }
        return node->isEnd;
    }

    // Find minimum XOR with a given number
    // Time Complexity: O(LOG)
    int minXOR(int num, int LOG = 31) {
        Node* node = root;
        int res = 0;
        for (int i = LOG; i >= 0; i--) {
            int bit = (num >> i) & 1;
            // Prefer SAME bit to minimize XOR
            if (node->child[bit]) {
                node = node->child[bit];
            } else {
                res |= (1 << i);
                node = node->child[1 - bit];
            }
        }
        return res;
    }

    // Find maximum XOR with a given number
    // Time Complexity: O(LOG)
    int maxXOR(int num, int LOG = 31) {
        Node* node = root;
        int res = 0;
        for (int i = LOG; i >= 0; i--) {
            int bit = (num >> i) & 1;
            if (node->child[1 - bit]) {
                res |= (1 << i);
                node = node->child[1 - bit];
            } else {
                node = node->child[bit];
            }
        }
        return res;
    }
};


# Trie for getting Strings
class Trie_String {
public:
    struct Node {
        Node* child[26];
        bool isEnd;

        Node() {
            memset(child, 0, sizeof(child));
            isEnd = false;
        }
    };

    Node* root;

    Trie_String() {
        root = new Node();
    }

    // Insert a word
    // Time: O(length)
    void insert(const string& s) {
        Node* node = root;
        for (char c : s) {
            int idx = c - 'a';
            if (!node->child[idx])
                node->child[idx] = new Node();
            node = node->child[idx];
        }
        node->isEnd = true;
    }

    // Search exact word
    // Time: O(length)
    bool search(const string& s) {
        Node* node = root;
        for (char c : s) {
            int idx = c - 'a';
            if (!node->child[idx]) return false;
            node = node->child[idx];
        }
        return node->isEnd;
    }

    // Check if any word starts with prefix
    // Time: O(length)
    bool startsWith(const string& prefix) {
        Node* node = root;
        for (char c : prefix) {
            int idx = c - 'a';
            if (!node->child[idx]) return false;
            node = node->child[idx];
        }
        return true;
    }
};
```


# Euler Tour Technique
```cpp
// Euler Tour Technique
// Used for flattening a tree and finding the subtree for any node.
class EulerTour {
public:
    int n, timer;
    vector<vector<int>> adj;
    vector<int> tin, tout, flat;

    EulerTour(int n) : n(n) {
        timer = 0;
        adj.assign(n + 1, {});
        tin.assign(n + 1, 0);
        tout.assign(n + 1, 0);
        flat.assign(n + 1, 0);
    }

    // Add undirected edge 
    void addEdge(int u, int v) {
        adj[u].push_back(v);
        adj[v].push_back(u);
    }

    // DFS to flatten the tree
    // Time Complexity: O(n)
    void dfs(int u, int parent) {
        tin[u] = ++timer;
        flat[timer] = u;

        for (int v : adj[u]) {
            if (v == parent) continue;
            dfs(v, u);
        }

        tout[u] = timer;
    }

    // Call this once after building edges
    void build(int root = 1) {
        dfs(root, 0);
    }

    // Returns subtree range of node u
    pair<int, int> subtree(int u) {
        return {tin[u], tout[u]};
    }
};
```

# Random Number Generator
```cpp
mt19937_64 RNG(chrono::steady_clock::now().time_since_epoch().count());
```


# Smallest Prime Factor Sieve
```cpp
vector<int> spf;
void spf_SieveOfEratosthenes(int n) {
    spf = vector<int>(n + 1);
    iota(spf.begin(), spf.end(), 0);
    for (int i = 2; i * i <= n; i++) {
        if (spf[i] == i) {
            for (int j = i * i; j <= n; j += i) {
                if (spf[j] == j) {
                    spf[j] = i;
                }
            }
        }
    }
}
```
