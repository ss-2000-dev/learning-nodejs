# Node.js, NPM 周りの知識をまとめたもの

### package.json の version 指定

#### そもそもバージョン（セマンティックバージョン）とは

- `major`: 前のバージョンと互換性を損なう変更をするときに上げる数字
- `minor`: 前のバージョンと互換性を持つ新機能追加の変更をするときに上げる数字
- `patch`: 前のバージョンと互換性を持つバグ修正の変更をするときに上げる数字

package.json は`major.minor.patch`で表現している

#### バージョン指定表現方法

バージョン固定

```
{
  "dependencies": {
    "foo": "1.0.0"
  }
}
```

指定した version より大きいバージョンのインストールを許可

- 1.0.0 より大きいバージョンインストールのインストールを許可
- <、>=、<=の比較演算子を使用した場合も、その比較演算子が持つ意味通りのバージョンがインストールされる

```
{
  "dependencies": {
    "foo": ">1.0.0"
  }
}
```

バージョンの範囲の指定

- ex. 1.1.0 以上、1.2.0 以下のバージョンがインストールされる

```
{
  "dependencies": {
    "foo": "1.0.1 - 1.2.0"
  }
}
```

ワイルドカード（X, \*）

```
{
  "dependencies": {
    "foo": "*",     // どんなバージョンでもOK
    "bar": "1.1.x", // >=1.1.0 and <1.2.0
    "hoge": "1.X",  // >=1.0.0 and <2.0.0
    "huga": ""      // "*"と同じことになる = どんなバージョンでもOK
  }
}
```

チルダ

- version のうち、minor バージョンが明記されている場合は patch バージョン部分の更新ができ、そうでない場合は minor バージョンの更新がされる、前のバージョンとの互換性を保ちながら、最新バージョンに保たれる可能性が高い

```
{
  "dependencies": {
    "foo": "~1.1.1",  // >=1.1.1 and <1.2.0
    "bar": "~1.1",    // >=1.1.0 and <1.2.0
    "hoge": "~1"      // >=1.1.0 and <2.0.0
  }
}
```

キャレット
― `major.minor.patch` のうち、一番左の 0 以外の数字のバージョンを更新しないような、更新が可能

```
{
  "dependencies": {
    "foo": "^1.1.1",  // >=1.1.1 and <2.0.0
    "bar": "^0.1.1",    // >=0.1.1 and <0.2.0
    "hoge": "^0.0.1"      // >=0.0.1 and <0.0.2
  }
}

```

参考

- [【いまさらですが】package.json の version 指定](https://qiita.com/chihiro/items/5826678bc9287fb57a28)
- [【package.json】 バージョンにつける「^」「~」は何を意味するのか？](https://zenn.dev/tm35/articles/778b9a260d43fc)
- [セマンティック バージョニング 2.0.0](https://semver.org/lang/ja/)
- [About semantic versioning | npm Docs](https://docs.npmjs.com/about-semantic-versioning)
