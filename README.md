# imiv-parser

>IMI共通語彙基盤ライブラリ　バージョン1.0.0 (2018年9月7日 公開, MIT ライセンス)に対応

ここにあるファイルをすべてダウンロードしてください

## 動作環境について　

以下の環境では動作確認済み

- macOS v14.1
- ubuntu v22.04
- Node.js v21.4.0

# imiv-parser-masterに移動

# 実行するためにnodeバージョン

最新版を使用


## npm

```
npm install imiv-parser
```

## 実行するTXTファイルの作成
imivparserを利用するにはIMIV形式に沿ったテキストファイルを作成してくだい
```
touch index.txt
```
例
```
#name "競馬"
#"競馬を表す単語"
class ic:競馬型;

#name "重賞"
#"レースを表す単語"
set ic:競馬型>ic:重賞型;

#name "レース名"
#"レース名を表す単語"
set ic:競馬型>ic:レース名型;
```



## 実行するためのJSファイルの作成


```
touch index.js
```

作成したindex.jsに下記コードをコピペしてください
```
const fs = require('fs');
const IMIVParser = require('imiv-parser');

// IMI形式のテキストファイルのパス
const filePath = 'ここにファイルのパス';

// ファイルを読み込んでIMIVパーサーに渡す
fs.readFile(filePath, 'utf8', (err, data) => {
    if (err) {
        console.error("ファイルの読み込みに失敗しました:", err);
    } else {
        let result;

        try {
            // IMIVパーサーを実行
            result = IMIVParser.parse(data);
        } catch (parseErr) {
            console.error("データのパースに失敗しました:", parseErr);
        }

        const resultFilePath = '出力したい名前.json';

        try {
            // ファイルに結果を書き込む
            fs.writeFileSync(resultFilePath, JSON.stringify(result, null, 2));
            console.log("結果が保存されました。");
        } catch (writeErr) {
            console.error("データの書き込みに失敗しました:", writeErr);
        }
    }
});


```
IMIVParser

```
IMIVParser.parse()で機能呼び出し

parse()の中にIMIテキストを引数にする
```

## 実行結果を保存するためのJSONファイルを作成

```
touch parsedResult.json
```

## 実行

```
node index.js
```

実行するとターミナルとparsedResult.jsonに結果が表示されます





