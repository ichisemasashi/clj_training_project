# Testing 1-2-3

あなたのチームは新しいテキストエディタを開発中で、あなたは行番号の実装を任されました。

文字列のリストを受け取り、各行の先頭に正しい番号を付けて返す関数を書いてください。

行番号は1から始まり、書式は n: string です。間にコロンとスペースがあることに注意してください。

例
```
number(List<string>()) // => List<string>()
number(List<string>{"a", "b", "c"}) // => ["1: a", "2: b", "3: c"]
```

```clojure
(ns line-numbers)

(defn number [lines]
  (map #(str %1 %2 %3)
       (rest (range))
       (repeat ": ")
       lines))
```

## Best Practice
```clojure
(ns line-numbers)

(defn number [lines]
  (map (partial format "%d: %s") (iterate inc 1) lines))
```  

* partial
  関数fとfに対する通常の引数より少ない数の引数を取り、可変個数の追加引数を取るfnを返す。呼び出されると、返された関数はargs + 追加のargsでfを呼び出します。

*  (iterate f x)
  x, (f x), (f (f x)) … の遅延シーケンスを返す f は副作用がないこと

```clojure
renshu.core=> (time (take 10000 (rest (range))))
"Elapsed time: 0.237308 msecs"
renshu.core=> (time (take 10000 (iterate inc 1)))
"Elapsed time: 5.07732 msecs"
```