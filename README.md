## `Ciallo, World～(∠・ω< )⌒☆`
窩不知道要寫什麼，那就來線段樹吧（
```cpp
template <class T>
class SegTree {
    vector<T> tree;
    vector<T> a;
    int n;
    T def = 0; //numeric_limits<T>::max();
private:
    T marge(T a, T b) {
        return a^b;
    }
    T _query(int idx, int l, int r, int ql, int qr) {
        if (qr < l || ql > r) return def;
        if (ql <= l && r <= qr) return tree[idx];

        int mid = (l + r) / 2;
        int lchild = 2 * idx + 1, rchild = 2 * idx + 2;
        return marge(_query(lchild, l, mid, ql, qr), _query(rchild, mid + 1, r, ql, qr));
    }
    void _update(int idx, int l, int r, int pos, T val) {
        if (l == r) {
            a[l] = val;
            tree[idx] = val;
            return;
        }
        int mid = (l + r) / 2;
        int lchild = 2 * idx + 1, rchild = 2 * idx + 2;
        if (pos <= mid) _update(lchild, l, mid, pos, val);
        else _update(rchild, mid + 1, r, pos, val);
        tree[idx] = marge(tree[lchild], tree[rchild]);
    }

public:
    SegTree(const vector<T>& v) {
        a = v;
        n = v.size();
        tree.resize(n * 4);
        build(0, 0, n - 1);
    }

    void build(int idx, int l, int r) {
        if (l == r) {
            tree[idx] = a[l];
            return;
        }
        int mid = (l + r) / 2;
        int lchild = 2 * idx + 1, rchild = 2 * idx + 2;
        build(lchild, l, mid);
        build(rchild, mid + 1, r);
        tree[idx] = marge(tree[lchild], tree[rchild]);
    }
    T query(int l, int r) {
        return _query(0, 0, n - 1, l, r);
    }
    void update(int pos, T val) {
        _update(0, 0, n - 1, pos, val);
    }
};
```
