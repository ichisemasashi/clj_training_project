
#  Stop gninnipS My sdroW!

1つ以上の単語からなる文字列を受け取り、同じ文字列を返す関数を書いてください。ただし、5文字以上の単語はすべて逆にしてください（この型の名前と同じです）。渡される文字列は、文字とスペースだけで構成される。空白は、複数の単語が存在する場合のみ含まれる。

例： 
```
spinWords( "Hey fellow warriors" ) => "Hey wollef sroirraw"
spinWords( "This is a test") => "This is a test"
spinWords( "This is another test" )=> "This is rehtona test"
```
が返されます。

```clojure
(ns clojure.spin-words
  (:require [clojure.string :as str]))

(defn reverse-if-5more [s]
   (if (<= 5 (count s))
     (apply str (reverse s))
     s))

(defn separate [s]
  (str/split s #" "))

(defn spin-words [strng]
  (let [len (count (separate strng))]
    (if (= 1 len)
      (reverse-if-5more strng)
      (str/join " " (map reverse-if-5more (separate strng))))))
```



## Best practice
```clojure
(ns clojure.spin-words
  (:require [clojure.string :as string]))

(defn spin-words [s]
  (string/replace s #"\w{5,}" string/reverse))
```

* (replace s match replacement)
sの中のmatchの全インスタンスをreplacementで置き換える。
  match/replacementは以下のようになる。
  string / string
 char / char
 pattern / (string or function of match).
  See also replace-first.
  pattern / string 以外の場合、置換はリテラルです(つまり、どの文字も特別に扱われません)。
  pattern / string の場合、置換文字列中の $1, $2 などは、パターン中の対応する括弧で囲まれたグループにマッチした文字列で置換されます。 置換文字列 r を文字通りに使用したい場合は、replacement 引数に (re-quote-replacement r) を指定してください。 java.util.regex.Matcher の appendReplacement メソッドに関するドキュメントも参照してください。
  Example:
 (clojure.string/replace "Almost Pig Latin" #"\b(\w)(\w+)\b" "$2$1ay")
 -> "lmostAay igPay atinLay"
