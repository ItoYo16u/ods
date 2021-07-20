# Open Data Structures (in Rust)

[Open Data Structures](https://opendatastructures.org/) is a textbook and source list about data structures.  
This is the Rust version of Open Data Structures. Only safe Rust.

*Advice and pull requests are welcome!*

* chapter01 (Interface)
    * [trait Queue](/chapter01/src/interface.rs#L1)
    * [trait Stack](/chapter01/src/interface.rs#L6)
    * [trait List](/chapter01/src/interface.rs#L11)
    * [trait USet](/chapter01/src/interface.rs#L19)
    * [trait SSet](/chapter01/src/interface.rs#L26)
    * [trait Graph](/chapter01/src/interface.rs#L33)
* chapter02 (Array-Based Lists)
    * [ArrayStack](/chapter02/src/arraystack.rs)
    * [ArrayQueue](/chapter02/src/arrayqueue.rs)
    * [ArrayDeque](/chapter02/src/arraydeque.rs)
    * [BDeque](/chapter02/src/boundeddeque.rs)
    * [DualArrayDeque](/chapter02/src/dualarraydeque.rs)
    * [RootishArrayStack](/chapter02/src/rootisharraystack.rs)
* chapter03 (Linked Lists)
    * [SLList](/chapter03/src/sllist.rs)
    * [DLList](/chapter03/src/dllist.rs)
    * [SEList](/chapter03/src/selist.rs)
* chapter04 (Skiplists)
    * [SkiplistSSet](/chapter04/src/skiplistsset.rs)
    * [SkiplistList](/chapter04/src/skiplistlist.rs)
* chapter05 (Hash Tables)
    * [ChainedHashTable](/chapter05/src/chainedhashtable.rs)
    * [LinearHashTable](/chapter05/src/linearhashtable.rs)
* chapter06 (Binary Trees)
    * [BinaryTree](/chapter06/src/binarytree.rs)
    * [BinarySearchTree](/chapter06/src/binarysearchtree.rs)
* chapter07 (Random Binary Search Trees)
    * [Treap](/chapter07/src/treap.rs)
* chapter08 (Scapegoat Trees)
    * [ScapegoatTree](/chapter08/src/scapegoattree.rs)
* chapter09 (Red-Black Trees)
    * [RedBlackTree](/chapter09/src/redblacktree.rs)
* chapter10 (Heaps)
    * [BinaryHeap](/chapter10/src/binaryheap.rs)
    * [MeldableHeap](/chapter10/src/meldableheap.rs)
* chapter11 (Sorting Algorithms)
    * [Merge-Sort](/chapter11/src/mergesort.rs)
    * [Quicksort](/chapter11/src/quicksort.rs)
    * [Heap-sort](/chapter11/src/heapsort.rs), using [BinaryHeap](/chapter10/src/binaryheap.rs#L87)
    * [Counting Sort](/chapter11/src/countingsort.rs)
    * [Radix-Sort](/chapter11/src/radixsort.rs)
* chapter12 (Graphs)
    * [AdjacencyMatrix](/chapter12/src/adjacencymatrix.rs)
    * [AdjacencyLists](/chapter12/src/adjacencylists.rs)
    * [Breadth-First Search](/chapter12/src/bfs.rs)
    * [Depth-First Search](/chapter12/src/dfs.rs)
* chapter13 (Data Structures for Integers)
    * [BinaryTrie](/chapter13/src/binarytrie.rs)
    * [XFastTrie](/chapter13/src/xfasttrie.rs)
    * [YFastTrie](/chapter13/src/yfasttrie.rs)
* chapter14 (External Memory Searching)
    * [BTree](/chapter14/src/btree.rs)

----
COPY FROM QIITA [『みんなのデータ構造』を読んで Rust で実装した. ](https://qiita.com/o8vm/items/713ad93bd3fa7aa548fc)

---
title: 『みんなのデータ構造』を読んで Rust で実装した
tags: Rust OpenDataStructures DataStructures
author: o8vm
slide: false
---
「みんなのデータ構造」を Rust で実装してみました。
この記事では、すすめ方、気になったところや躓いたところなどについて書きたいと思います。

## 実装したもの
実装したものは以下になります。効率などを考えるとunsafeが必須なのかもとも思いましたが、今回は Rust の勉強を兼ねているので、Safe Rust のみで実装してみました。
一応簡単なテストコードも付属しています。(`cargo test`で試せます)。

[Open Data Structures (in Rust)](https://github.com/o8vm/ods) 

時々見直したり書き直したりもしていますが、前半の章よりも後半のほうがより Rust らしくかけているのではないかなと思います。
ちなみに一番うまく実装できたと思うお気に入りのデータ構造は `RedBlackTree` です。

## きっかけ
ぼくはいわゆる日曜プログラマーで、趣味で低レイヤー活動をしたり Rust でプログラミングをしています。ただ、これまで"データ構造とアルゴリズム" などの分野を学んだことはなかったので、OSの勉強などをしていてリストや木構造などデータ構造の話題がでてきても、苦手意識から適当に流すか無視してしまっていました。

そして、そろそろこれではいけないと Rust でデータ構造を学べる教材を探していた時[^1]に、「みんなのデータ構造」を見つけました[^2]。
書籍は C++ での実装でしたが、訳者まえがきの内容がとてもよく、また、「[『みんなのデータ構造』発売および予約開始のお知らせ](https://www.lambdanote.com/blogs/news/article-6)」のページにて以下文言を発見し、Rust版が無いなら自分で実装しながら学んでみようと思い、本書に取り組むことに決めました。また、この報告を一番乗りでやってみたかったのもあります。

> 『みんなのデータ構造』を読んでRustで実装した」といった報告をお待ちしています！

[^1]: Rust にハマっていたので Rust で学べる教材をと思っていました。
[^2]: twitter で、英語で勉強方法を募集したところ、twitter で知り合った Red ○at の Kiali のメンテナの方に「エンジニアを目指すならまずデータ構造とアルゴリズムやれ、 ODS はいい教科書」と教えてもらっていたのでした。

## 読みすすめ方
初学者は第一章から地道に読み進めたほうがいいと思いました。

この書籍は数学も交えて各データ構造をシンプルに、それでいてとてもわかりやすく解説してくれています。
曖昧なごまかしもなく、大変よいのですが、それらを理解するのに必要な、最低限の知識や概念は第一章で説明されています。なので、ここを読み飛ばすと痛い目にあいます[^3]。逆に第一章をクリアすればその後の説明も比較的すんなり理解できるようになると思います。

[^3]: ぼくは最初読み飛ばしてしまい、ひどい目にあいました。

他の技術書を読む上でもとても大切な内容だと考えられるので、訳者前書きと第一章だけでも読んだほうがいいと思います[^4][^5]。

[^4]: https://sites.google.com/view/open-data-structures-ja/home
[^5]: https://www.lambdanote.com/products/opendatastructures

全体としては、一章ずつ読んで理解できたと思ったら実装してみる、という感じで進めました。
また、各データ構造についてわからなくなった時には、自分で絵を書いてみることが驚くほどの効果を発揮してくれるように思えました。詰まっている人はお試しください。

以降、Rust でどう実装していったかに焦点をあてていきます。

## 各章の実装概要
### 第１章(インターフェース部分)
第一章では、基本的なデータ構造のインターフェースについても説明されています。なお、Rust では共通の振る舞いは trait を使って定義できるので、まず最初に、以下リンクのように各インターフェースを定義してしまいました。

[interface.rs](https://github.com/o8vm/ods/blob/master/chapter01/src/interface.rs)
例:

```Rust
pub trait List<T: Clone> {
    fn size(&self) -> usize;
    fn get(&self, i: usize) -> Option<T>;
    fn set(&mut self, i: usize, x: T) -> Option<T>;
    fn add(&mut self, i: usize, x: T);
    fn remove(&mut self, i: usize) -> Option<T>;
}

pub trait USet<T: PartialEq + Clone> {
    fn size(&self) -> usize;
    fn add(&mut self, x: T) -> bool;
    fn remove(&mut self, x: &T) -> Option<T>;
    fn find(&self, x: &T) -> Option<T>;
}
```

各インターフェースで扱うデータの特徴については、トレイト境界で指定できます(たとえば、`SSet`インターフェースでは`PartialOrd`もしくは`Ord`が必要ですし、USetでは`PartialEq`もしくは`Eq`が必要でしょう)。
なお、リストや木構造などで`RefCell`を使用する関係で、Clone もトレイト境界に指定してあります。`borrow()`から参照を返すことができないので、`get()`や`find()`で`clone()`した値を返すことにしたためです。

[How do I return a reference to something inside a RefCell without breaking encapsulation?](https://stackoverflow.com/questions/29401626/how-do-i-return-a-reference-to-something-inside-a-refcell-without-breaking-encap)

関連型か trait のメソッドの返り値に`impl Deref<Target = T>`を使用できればよかったのですが、現在は使用できないようだったのでこのような形としています。
他にもっと良いやり方があれば教えてください。

[Is it possible to use `impl Trait` as a function's return type in a trait definition?
](https://stackoverflow.com/questions/39482131/is-it-possible-to-use-impl-trait-as-a-functions-return-type-in-a-trait-defini)

### 第２章(配列ベースのリスト)
配列ベースのリストでは、データ構造としても、Rust としても、とくに難しい部分ありませんでした。
どのデータ構造も、基本的にデータを格納するバッファがあって、目的の扱い方ができるように、その扱い方に影響する要素とともにラップするような形になっています。このバッファに `Vec`を使ったほうが楽だろうなとも思いましたが、`resize()`などの実装も書籍の内容とできるだけ合わせたかったので、今回は Boxed Slice を使用しました。

なお、要素が存在しない場合のデフォルトの状態を `Option` 型の `None` 値としたかったので、例えば `ArrayStack` は以下のような感じで定義しています。

```Rust
pub struct Array<T> {
    a: Box<[Option<T>]>,
    n: usize,
}
```

また、この章のデータ構造は、`List` インターフェースを実装する `ArrayStack` が基本となっているため、`ArrayStack` を実装できればあとは比較的単純です。

ところで、型 `T` には、後のリンクリストや木構造のために、`Clone`がトレイト境界に指定してあり、`get()`や`find()`では参照を返さないのでした。今回　`ArrayStack` に実装した `List` インターフェースの `get()` でも参照を返さずに `clone()` した値を `Option` に包んで返しています。

```Rust
    fn get(&self, i: usize) -> Option<T> {
        self.a.get(i)?.as_ref().map(|x| x.clone())
    }
```

このため、上記を利用する `RootishArrayStack` では、`Rc<[T]>`がベースになっているのが味噌です。

```Rust
pub struct Array<T> {
    blocks: ArrayStack<Rc<[RefCell<Option<T>>]>>,
    n: usize,
}
```

こうすることで内部可変性のパターンにしたがって `List` インターフェースを実装できます。

```Rust
    fn set(&mut self, i: usize, x: T) -> Option<T> {
        let b = Self::i2b(i);
        let j = i - b * (b + 1) / 2;
        self.blocks.get(b)?[j].borrow_mut().replace(x)
    }
```

他にも良いやり方があるのかもしれませんが、今回はこれでよしとしてしまいました。
もしもっとマシなやり方があればぜひ教えてください。

### 第３章、第４章(リンクリスト)
この章からが最初の壁だと思いますが、リンクリストは各ノードについて複数の所有者が存在しうるパターンなので、`Rc`や`RefCell`を使えばいいことを思いつければ、実はそんなに難しくありません。
ここでは各ノードのリンクを表すのに、以下のような型を用いました。

```Rust
type Link<T> = Option<Rc<RefCell<Node<T>>>>;
```

Skiplistは一見して処理が複雑に見えますが、これも書籍をよくよみ、絵を書いたりすると、実際はかなり単純だと気がつけます。Redis でも使用されているデータ構造なので学んでおいて損はないと思いました。また、Rust だから難しいというような部分もないと思います。

それよりも若干考えにくかったのが双方向連結リスト(`DLList`)と `SEList` でした。
書籍の通りの実装だと循環参照により、Debug 出力がスタックオーバーフローを発生させてしまいます。
循環参照をどのようになくすのかがポイントになりますが、今回は`head`と`tail`として dummy ノードを２個用意し、後方へのリンクは `Weak`としました。こうすることで循環参照を回避できます。

```Rust

type Link<T> = Option<Rc<RefCell<Node<T>>>>;
type Wink<T> = Option<Weak<RefCell<Node<T>>>>;

#[derive(Clone, Debug, Default)]
pub struct DLList<T> {
    head: Link<T>,
    tail: Wink<T>,
    n: usize,
}

#[derive(Clone, Debug, Default)]
pub struct Node<T> {
    x: T,
    next: Link<T>,
    prev: Wink<T>,
}
```

リンクを`Option<Rc<RefCell<Node<T>>>>`で表してしまったので、これまでにくらべると書くコード量が若干多くなっています。しかし、全体で見ればそれほどでもありません。Rust でリストは難しいとか聞いており恐れていましたが、むしろ拍子抜けするぐらいでした。

なお、後ほど木構造を実装していて思ったのですが、`RefCell<Option<Rc<Node<T>>>>` のような型で実装したほうがもっとスッキリかけたのではないかと考えています。
実際、`XFastTrie`というトライ木でも双方向連結リストを使用しますが、こちらは`RefCell<Option<Rc<Node<T>>>>`を使用しており、この章で実装したリンクリストよりもかなりシンプルに実装できたと思っています(個人の感想)。
やっていることは全く同じですが、後ほど書き直すかもしれません。  

### 第５章(ハッシュテーブル)
この章では `ChainedHashTable`と`LinearHashTable`を実装しますが、いずれも Rust でも素直に実装できるようでした。

たとえば、`Hash` トレイトを実装していれば、型 `T` の値 `x`のハッシュ値も下記のように簡単に計算できます。トレイト境界に `Hash`を指定してあげるだけです（たぶんこれで良いはず）。

```Rust
pub fn hashcode<T: Hash>(x: &T) -> usize {
    let mut s = DefaultHasher::new();
    x.hash(&mut s);
    s.finish() as usize
}
```

上記を利用して、`ChainedHashTable`と`LinerHashTable`でそれぞれ乗算ハッシュ法と64bitのTabulation Hashing を実装しています。
以下は Tabulation Hashing の例です。

```Rust
// tabulation hashing
lazy_static! {
    pub static ref TAB: [[u64; 256]; 8] = {
        let mut array = [[0; 256]; 8];
        for i in 0..8 {
            thread_rng().fill(&mut array[i]);
        }
        array
    };
}
pub fn byte_chunks_64(h: u64) -> [u8; 8] {
    [
        (h & 0xff) as u8,
        ((h >> 8) & 0xff) as u8,
        ((h >> 16) & 0xff) as u8,
        ((h >> 24) & 0xff) as u8,
        ((h >> 32) & 0xff) as u8,
        ((h >> 40) & 0xff) as u8,
        ((h >> 48) & 0xff) as u8,
        ((h >> 56) & 0xff) as u8,
    ]
}
...
    fn hash(&self, x: &T) -> usize {
        // u64 tabulation hashing

        let mut v = 0u64;
        let h = x.hashcode();
        let chunks = byte_chunks_64(h as u64);
        for (i, c) in chunks.iter().enumerate() {
            v ^= TAB[i][*c as usize];
        }
        v = v.overflowing_shr(Self::W - self.d).0;
        v as usize
    }
```

なお、配列ベースのリストと同様、`grow()`などのの実装も書籍の内容に近くしたかったため、Boxed Slice をベースにしています。

```Rust
// ChainedHashTable
#[derive(Clone, Debug, Default, Eq, Ord, PartialEq, PartialOrd)]
pub struct ChainedHashTable<T> {
    t: Box<[ArrayStack<T>]>,
    n: usize,
    d: usize,
    z: usize,
}

// LinerHashTable
#[derive(Clone, Debug, Eq, Ord, PartialEq, PartialOrd, Copy)]
enum Elem<T> {
    Val(T),
    Null,
    Del,
}
#[derive(Clone, Debug, Default, Eq, Ord, PartialEq, PartialOrd)]
pub struct LinearHashTable<T> {
    t: Box<[Elem<T>]>,
    n: usize,
    q: usize,
    d: u32,
}
```

### 第６章~第１０章(木、木、木、、、)
６章から、１０章までは `BinaryHeap` を除いて、ベースとなる構造がほとんど同じ木構造を扱います。
`BinaryTree`, `BinarySearchTree`, `Treap`, `ScapegoatTree`, `RedBlackTree`, `MeldableHeap` のどれもが、以下のようなデータ構造をベースにして実装できました。
ちなみに、`RedBlackTree` 以外はとても素直に実装できたのでそれほど難しくもありませんでした。

```Rust
#[derive(Clone, Debug, Default)]
pub struct BTNode {
    left: RefCell<Option<Rc<BTNode>>>,
    right: RefCell<Option<Rc<BTNode>>>,
    parent: RefCell<Option<Weak<BTNode>>>,
}
```

ほとんどリンクリストで用いたときの構造と同じです。
最初は、`Option<Rc<RefCell<Node>>>`で書き始めていましたが、メソッドチェーンが長くなり、全体としてもかなり煩雑にみえたので、何回か書き直した結果このカタチに落ち着きました。
きちんと分析したわけではないですが、かなりスッキリしたのではないかと思っています。

上記のデータ構造に対して、必要な要素を加えるだけで、他の色々な木構造を表せます。たとえば、`RedBlackTree`は以下のようにしました。値と色の情報を加えるだけです。

```Rust
pub enum Color {
    Red,    // 0
    Black,  // 1
    WBlack, // 2
}

#[derive(Clone, Debug, Default)]
pub struct RBTNode<T> {
    color: RefCell<Color>,
    x: RefCell<T>,
    left: RefCell<Option<Rc<RBTNode<T>>>>,
    right: RefCell<Option<Rc<RBTNode<T>>>>,
    parent: RefCell<Option<Weak<RBTNode<T>>>>,
}
```

ただ、この構造では書籍の通りに `RedBlackTree` を扱うのが少し難しく、実装に手間取りました。

ODS の RedBlackTree の実装では、本来ノードが存在しない部分も外部ノードNil(黒色を持つ)として、赤黒木の性質（「黒の高さの性質」、「赤の辺の性質」、「左傾性」）を保つための処理に積極的に関わってきます。もちろん外部ノードは、要素がNilなだけで、色だけでなく親の情報も持っていますので、書籍の実装ではこれらの処理もそれほど難しそうではありませんでした。
一方で上記の Rust での実装では、存在しないノードは単純に `None`となるので、親や色の情報を持てません。このため。赤黒木の性質を満たすための処理をこのままで実装するのがとても難しく思えたのでした。

「これは終わった。。。」としばらく諦めていましたが、なんども読み込んで絵を書いてを繰り返しているうちにあることに気が付きました。
外部ノードが処理にかかわるのは高々１回だけで、実際の処理に大きく影響するのはその親と自身の色情報だけだったのです(もっと早く気がつけという話ですが)。そうすると、あとは簡単に一般化もできて実装もそれほど難しくはなりませんでした。

例えば以下のように、色情報と親ノードをあらかじめ取得してこれを扱うような実装にしておけばよいだけです。`None`から親をたどることはできませんが、親からは`None`の子もその色も把握できます（あ、Noneはもともと黒でした）。

Rust実装:

```Rust
fn remove_fixup(&mut self, mut color: isize, mut u: Tree<T>, mut p: Tree<T>)
```

C++実装:

```c++
void removeFicup(Node *u)
```

上記のようにRust実装では、ノード`u`だけでなく、その親`p`と自身の色`color`を渡すようにしています。
細かい実装が気になる方はぜひソースリストの方をご参照ください。
赤黒木の性質（「黒の高さの性質」、「赤の辺の性質」、「左傾性」）を満たしているかどうか確認するためのメソッドも定義してあります。

`BinaryHeap` は他の木構造とは異なり配列ベースのデータ構造で素直に実装できるので、Rust で実装するうえでも一番簡単かなと思います。

```Rust
pub struct BinaryHeap<T> {
    a: Box<[Option<T>]>,
    n: usize,
}
```

### 第１１章(整列アルゴリズム)
木がたくさんすぎてアレルギーになりそうなところに、整列アルゴリズムが湧いて出てくれて救われました。
とくに難しい部分もなく Rust でも素直に実装できると思います。

### 第１２章(グラフ)
グラフの概念は初めて触れましたが、隣接行列も隣接リストもどちらも、配列ベースのデータ構造で素直に実装でき、とても簡単でした。
Graphインターフェースのほとんどが、スライス、Vec、ArrayStack が本来備えてるメソッドを利用して実装できます。

```Rust
// AsjacencyMatrix
pub struct AdjacencyMatrix {
    n: usize,
    a: Vec<Vec<bool>>,
}
...
    fn get_mut(&mut self, i: usize, j: usize) -> Option<&mut bool> {
        if let Some(ii) = self.a.get_mut(i) {
            ii.get_mut(j)
        } else {
            None
        }
    }
...
    fn add_edge(&mut self, i: usize, j: usize) {
        if let Some(e) = self.get_mut(i, j) {
            *e = true;
        }
    }
```

```Rust
// AdjacencyList
pub struct AdjacencyLists {
    n: usize,
    adj: Vec<ArrayStack<usize>>,
}
...
    fn add_edge(&mut self, i: usize, j: usize) {
        if let Some(e) = self.adj.get_mut(i) {
            e.add(e.size(), j);
        }
    }
```

### 第１３章(トライ木)
この章では、`BinaryTrie`, `XFastTrie`, `YFastTrie` の三種類のトライ木を実装します。
トライ木は整数を扱うデータ構造ですが、木というだけあって、`BinaryTree`で用いたようなデータ構造をベースとするところも同じです。
ただ一つ厄介な部分があり、それは、内部で双方向連結リストも利用することです。

たとえば、`BinaryTrie`は最終的には下記のようなデータ構造に落ち着きました。

```Rust
pub struct BTNode<T: USizeV + Default> {
    x: RefCell<T>,
    child: [RefCell<Option<Rc<BTNode<T>>>>; 2], // 0 = left, 1 = right
    jump: RefCell<Option<Rc<BTNode<T>>>>,
    parent: RefCell<Option<Weak<BTNode<T>>>>,
    prev: RefCell<Option<Weak<BTNode<T>>>>, // left
    next: RefCell<Option<Rc<BTNode<T>>>>,   // right
}
pub struct BinaryTrie<T: USizeV + Default> {
    n: usize,
    r: Rc<BTNode<T>>,
    head: Option<Rc<BTNode<T>>>,   // dummy1
    tail: Option<Weak<BTNode<T>>>, // dummy2
}
```

C++ の場合と見比べてみてください。

```c++
	T x;
	N *jump;
	N *parent;
	union {
		struct {
			N *left;
			N *right;
		};
		struct {
			N *prev;
			N *next;
		};
		N* child[2];
	};
```

Safe Rust では C++ のように `Union` を使うことはできません。それに、双方向連結リストは `Weak` なポインタが必要なので、仮に Safe Rust で `Union` のような定義ができるとしても、ノードの子へのポインタの片方が `Weak` になってしまったらリンクは切れて意味がなくなってしまいます。

そこで今回は双方向連結リスト用に `prev`と`next`のポインタを別途持たせることにしました。空間使用量は少し増えてしまいますが(`Rc`に包んでいるのでそれほどでもないとは思いますが)、こうしたことで実装はかなりシンプルになったと思います。

なお、トライ木は非負整数値を導出できるデータ構造ならなんでも良いらしいので、以下のような非負整数値を出力するメソッドを持つトレイトを定義し、このトレイトを実装したデータ構造なら受け入れ可能としています。

```Rust
pub trait USizeV {
    fn usize_value(&self) -> usize;
}
```

つづいて、`XFastTrie`ですが、このデータ構造は、ノードの探索にビット値の prefix をキーにしたハッシュテーブル使用するようにしただけです。以下のような形としました。ハッシュ値を取り扱うためにノードに `Hash` を実装する必要がありますが、`Hash`さえ実装していれば前に実装しておいた `LinerHashtable`がそのまま使用できます。

```Rust
pub struct BTNode<T: USizeV + Default> {
    pub x: RefCell<T>,
    prefix: RefCell<usize>,
    child: [RefCell<Option<Rc<BTNode<T>>>>; 2], // 0 = left, 1 = right
    jump: RefCell<Option<Rc<BTNode<T>>>>,
    parent: RefCell<Option<Weak<BTNode<T>>>>,
    prev: RefCell<Option<Weak<BTNode<T>>>>,   // left
    pub next: RefCell<Option<Rc<BTNode<T>>>>, // right
}
impl<T: USizeV + Default> Hash for BTNode<T> {
    fn hash<H: Hasher>(&self, state: &mut H) {
        self.prefix.borrow().hash(state);
    }
}
pub struct XFastTrie<T: USizeV + Default> {
    n: usize,
    r: Rc<BTNode<T>>,
    head: Option<Rc<BTNode<T>>>,   // dummy1
    tail: Option<Weak<BTNode<T>>>, // dummy2
    t: Box<[LinearHashTable<Rc<BTNode<T>>>]>,
}
```

`YFastTrie`は `XFastTrie`に `Treap`を組み合わせた値を追加できるようにした形です。一見すると難しそうなのですが、面倒な部分はすでに `XFastTrie`, `Treap` 側で実装がすんでいるので、トライ木の中では一番シンプルな実装となりました。

```Rust
struct YPair<T: USizeV + Default> {
    ix: usize,
    t: Rc<RefCell<Treap<T>>>,
}
pub struct YFastTrie<T>
where
    T: USizeV + Default + PartialOrd + Clone,
{
    xft: XFastTrie<YPair<T>>,
    n: usize,
}
```

### 第１４章(B木)
B木はもともと On-disk なデータを対象にした木構造のようですが、二分木の一般化でかつブロック単位でノードを扱うこともあり、これまでの木構造のようなリンクリスト形式ではなく、どちらかというと `BinaryHeap` のような配列ベースのデータ構造を対象としているような感覚で実装できました。
実装しなければならない機能は多いですが、B木の性質をみたすように借用や併合などが発生するだけで、考え方も Rust での実装もそれほど難しくありませんでした（シフトなど添字の計算が発生する処理は考えるのは大変だった）。

外部メモリは `BlockStore`というデータ構造で抽象化されており(`read_block()`, `write_block()`, `free_block()`, `place_block()`)、B木はこれに対して処理を行います。

```Rust
#[derive(Clone, Debug, Default, Eq, Ord, PartialEq, PartialOrd)]
struct Node<T: Clone + PartialOrd> {
    id: usize,
    keys: Box<[Option<T>]>,
    children: Box<[i32]>,
}

#[allow(non_snake_case)]
#[derive(Clone, Debug, Default, Eq, Ord, PartialEq, PartialOrd)]
pub struct BTree<T: Clone + PartialOrd> {
    b: usize,  // the maximum number of children of a node (must be odd)
    B: usize,  // d div 2
    n: usize,  // number of elements stored in the tree
    ri: usize, // index of the root
    bs: BlockStore<Node<T>>,
}
```

今回 `BlockStore` は `ArrayStack` で実装しています。 

```Rust
pub struct BlockStore<T: Clone> {
    blocks: ArrayStack<T>,
    free: ArrayStack<usize>,
}
```

なお、あくまで操作対象はディスクを念頭においているので、ノードの内部を書き換えたあとに、読み込みが発生するまえに書き換えた先のノードを更新しておく必要がありました。

例:

```Rust
                    x = w.remove(0).unwrap();
                    u.add(x, w.id as i32);
                    self.bs.write_block(w.id, w);
                    self.bs.write_block(u.id, u.clone());
```

## つまずいたところ
以下では実装している際につまずいて実際に人に教えてもらったり、未解決のまま放置した箇所に限り触れることにします。

### `borrow()`と`loop`
以下は、`SkiplistList`からの抜粋ですが、下記のコードは `match` の終わりにセミコロンがないとコンパイルエラーになります。

```Rust
loop {
    let u = Rc::clone(&n);
    match u.borrow().next[r] {
        Some(ref u) if j + n.borrow().length[r] - 1 < i => {
            j += n.borrow().length[r];
            n = Rc::clone(u)
        }
        _ => break,
    }; // <= これがないとコンパイルエラー
}
```

```
error[E0597]: `u` does not live long enough
  --> chapter04/src/skiplistlist.rs:58:31
   |
58 |                         match u.borrow().next[r] {
   |                               ^---------
   |                               |
   |                               borrowed value does not live long enough
   |                               a temporary with access to the borrow is created here ...
...
65 |                     }
   |                     -
   |                     |
   |                     `u` dropped here while still borrowed
   |                     ... and the borrow might be used here, when that temporary is dropped and runs the destructor for type `std::cell::Ref<'_, skiplistlist::Node<T>>`
   |
   = note: The temporary is part of an expression at the end of a block. Consider adding semicolon after the expression so its temporaries are dropped sooner, before the local variables declared by the block are dropped.
```

セミコロンありだと、`u`を使う式は `match ... {...}` なので、「`match`式の評価（テンポラルの消費）」→「`u`のdrop」という順ですが、セミコロンなしだと`u`を使う式が`loop {...}` になってしまって、`loop`式の評価が終わるまで`u`がdropできずダメという感じのようです。そっくりそのままtwitterでうどん先生に教えていただきました。

### `default()`の罠1
構造体の初期化のときに、`..Default::default()`を使うと、たとえデフォルト値が必要ない場合でも、`Default`がトレイト境界にないとコンパイルエラーになるようです。

```Rust
impl<T: Default> RBTNode<T> {
    pub fn new(x: T) -> Self {
        Self {
            x: RefCell::new(x),
            ..Default::default()
        }
    }
}
```

下記のようにすれば、`Default`の境界は不要

```Rust
impl<T> RBTNode<T> {
    pub fn new(x: T) -> Self {
        Self {
            x: RefCell::new(x),
            left: Default::default(),
            right: Default::default(),
            parent: Default::default(),
            color: Default::default(),
        }
    }
}
```

### `default()`の罠2
`Default`を実装する処理の中で`..Default::default()`を使ってはいけません。言われてみると当たり前なきがしますが再帰でスタックオーバーフローしてしまいます。素直に derive しましょう。こちらもデバッグ手法も含めてtwitterでうどん先生に教えていただきました。

```Rust
// ダメ
impl Default for X {
    fn default() -> Self {
        Self {
            ..Default::default()
        }
    }
}
```

### `rotate_left()`を使おう
スライスで要素を決まった分シフトする際には、`swap()`で変にやらずに、素直に`rotate_left()`や`rotate_right()`を使いましょう。
間違った添字の計算とかで無駄な時間をすごしてしました。twitterでmonochrome先生に教えていただきました。

### `or`が便利
`Option`値で `A`が`Some`だったら`A`を、`A`が`None`で`B`が`Some`だったら`B`を変数に束縛したいなんてときがあると思いますが、`if`で場合分けをすると冗長で煩雑になります。`or`を使いましょう。twitterでドッグ先生に教えていただきました。

https://doc.rust-lang.org/std/option/enum.Option.html#method.or

```Rust
match (prev, parent, left, right) {
    (Some(p), Some(v), left, right) if Rc::ptr_eq(&p, &v) => {
        next = left.or(right).or(Some(p));
    }
  ...
}
```

### `rand::Rng`の`fill()`が便利
配列を乱数で初期化したいときがありますが、イテレータで頑張って処理しなくても`fill()`で一発でした。twitterでてらモス先生に教えていただきました。
https://docs.rs/rand/0.7.3/rand/trait.Rng.html#method.fill

### pretty printing
Debug 出力では`"{:#?}"`でpretty printingできます。小さめの木構造とか見たいときに便利です。
twitterであるごん先生におしえていただきました。

### `Rc`ベースのデータ構造の罠
`Rc`では、`Rc`のデストラクタ内部で再帰呼び出しが実施されます。このため、Linked List など`Rc`ベースのデータ構造では、連結が大きすぎるとリソースの破棄時にスタックオーバーフローを発生させてしまうようです。解決方法は Drop　を自分で実装して再帰呼び出しを防ぐことになります。
この問題点の指摘については[reddit: Finished implementing OpenDataStructures in Rust](https://www.reddit.com/r/rust/comments/hk2nbp/finished_implementing_opendatastructures_in_rust/)にて、encyclopedistさんに教えていただきました。

解決方法については、twitterでガラスボー先生に教えていただきました。ありがとうございました。

https://stackoverflow.com/questions/57781630/how-to-prevent-a-stack-overflow-from-a-recursive-deallocation-when-using-rc-in-r

雑ですが、すでに修正版をマージ済みです。

### `SkiplistSSet`
### `BTree`の`remove()`

## 感想
twitter で質問すると運が良ければたまにいろいろ教えてくれる方がいます。神か？
というのは一旦おいといて、本書を通してで実装してみて、データ構造に関する苦手意識を払拭できたと思います。

今回自分で実装してみたデータ構造を実際には自分で使用することはないのでしょうけど、実装しようと思えば簡単に実装できる力がついたし/それができることがわかったし、Rust の提供する既存のデータ構造をどんなときに使えばいいのかもイメージできるようになってきたのではないかなと期待しています。ドキュメントに書いてあることの意味がよくわかるようになったというのも大事で、どのデータ構造を使うべきか判断するための材料を自分の頭の中に手に入れたイメージがあります。

Rust 力もはじめたころより up した気がするので、「みんなのデータ構造」を Rust で実装してみるをやってみて本当に良かったなと思いました。

なお特別に Rust に詳しいわけでなく、ほとんどコードも書かない生活をしています。おそらく詳しい人がみれば改善できる部分がたくさんあるに違いないと思っています。もしそういう部分を見つけられたら、ぜひアドバイスやプルリクをいただければと思います。

https://github.com/o8vm/ods

## 宣伝
Linux と Rust が好きで他にも記事を書いてますよかったらみてってください。
[CPU Steal Time 入門](https://qiita.com/o8vm/items/fffbcd1dc009f9c7f930)
[Rust で vmlinux を起動できる x86 ブートローダーを作ってみた話](https://qiita.com/o8vm/items/cda42e0a55744b9ff253)
