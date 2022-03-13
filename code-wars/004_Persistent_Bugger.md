# Persistent Bugger.

正のパラメータ `num` を受け取り、 `num` の数字を一桁になるまで何回掛け合わせなければならないかという掛け算の回数を返す関数 `persistence` を書きなさい。

例： (Input --> Output):

```
39 --> 3 (because 3*9 = 27, 2*7 = 14, 1*4 = 4 and 4 has only one digit)
999 --> 4 (because 9*9*9 = 729, 7*2*9 = 126, 1*2*6 = 12, and finally 1*2 = 2)
4 --> 0 (because 4 is already a one-digit number)
```

## 私の解答

```clojure
(ns persistent.core)

(defn atoi [a]
  (Integer/parseInt a))

(defn split-number [num]
  (let [s (format "%s" num)
        ls (clojure.string/split s #"")]
    (map atoi ls)))

(defn helper-persistence [num acc]
  (let [prod (apply * (split-number num))]
    (cond (< num 10) acc
          (< prod 10) (+ 1 acc)
          :else (recur prod (inc acc)))))


(defn persistence [n]
  (helper-persistence n 0))
```

## Best Practice
```clojure
(ns persistent.core)

(defn persistence [n]
  (if (< n 10)
    0
    (let [digit-list (->> (str n)
                          seq
                          (map str)
                          (map read-string))]
        (if (= 1 (count digit-list))
            digit-list
            (inc (persistence (reduce * digit-list)))))))
```

