# Beginner Series #3 Sum of Numbers

2つの整数a,bが与えられ、それらは正でも負でもよいので、それらの間のすべての整数の和を求め、それを返せ。2つの数値が等しい場合はaかbを返す。

注意： a と b は順序付けされていない!

例 (a, b) --> 出力 (説明)

```
(1, 0) --> 1 (1 + 0 = 1)
(1, 2) --> 3 (1 + 2 = 3)
(0, 1) --> 1 (0 + 1 = 1)
(1, 1) --> 1 (1 since both are same)
(-1, 0) --> -1 (-1 + 0 = -1)
(-1, 2) --> 2 (-1 + 0 + 1 + 2 = 2)
```

## 私の解答

```clojure
(ns clojure.numbers-sum)

(defn get-sum [a b]
  (let [from (min a b)
        to (max a b)]
    (if (= from to) from
      (reduce + (range from (inc to))))))
```

# The Best practice

```clojure
(ns clojure.numbers-sum)

(defn get-sum [a b]
   (apply + (range (min a b) (inc (max a b)))))
```

