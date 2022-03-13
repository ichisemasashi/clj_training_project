# Number of trailing zeros of N!

与えられた数値の階乗における末尾のゼロの数を計算するプログラムを作成しなさい。

```
N! = 1 * 2 * 3 * ... * N
```

1000！は2568桁なので要注意...。

For more info, see: http://mathworld.wolfram.com/Factorial.html

Examples

```
zeros(6) = 1
# 6! = 1 * 2 * 3 * 4 * 5 * 6 = 720 --> 1 trailing zero

zeros(12) = 2
# 12! = 479001600 --> 2 trailing zeros
```

## 私の解答

```clojure
(ns leading-zeros)

;; from expression(3) of http://mathworld.wolfram.com/Factorial.html
(defn zeros [n]
  (let [k_start 1
        k_max (Math/floor (/ (Math/log n) (Math/log 5)))
        r (range k_start (inc k_max))]
    (int (reduce + (map #(Math/floor (/ n (Math/pow 5 %))) r)))))
```    

## the best practice

```clojure
(ns leading-zeros)

(defn zeros [n] 
  (loop [factor 5 result 0]
    (if (= 0 (quot n factor))
      result
      (recur (* 5 factor) (+ result (quot n factor))))))
```


* (quot num div)

numをdivで割った商。

## The clever

```clojure
(ns leading-zeros)

(defn zeros [n] 
 (if (= n 0) 0
  (let [d (quot n 5)] (+ d (zeros d)) )
 ) 
)
```

```clojure
(ns leading-zeros)

(defn zeros
  "Calculate number of trailing zeros in factorial(n).
  Solved by counting all factors of 5 in range. There
  must be at least one factor of 2 for each factor of 5,
  and each 2*5 pair gives us another trailing zero."  
  [n]
  (->> (iterate (partial * 5) 5N)     ; powers of 5
       (map #(bigint (/ n %)))        ; n/5, n/25, n/125, n/625 etc.
       (take-while pos?)              ; positive values only
       (apply +)                      ; add them together
   )
  )
```