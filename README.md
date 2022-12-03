# 数独ソルバー

世界最速（多分）の TypeScript製 数独ソルバーです。  
下記ページから、実際に動いているところを見ることができます。  
https://sudoku-svelte.vercel.app/

## インストール

```
npm i sudoku-solver-ts
```

or

```
yarn add sudoku-solver-ts
```

## 使い方

```js
import { solve, SolveStatus } from "sudoku-solver-ts"

const result = solve([
  8, 0, 0, 0, 0, 0, 0, 0, 0,
  0, 0, 3, 6, 0, 0, 0, 0, 0,
  0, 7, 0, 0, 9, 0, 2, 0, 0,
  0, 5, 0, 0, 0, 7, 0, 0, 0,
  0, 0, 0, 0, 4, 5, 7, 0, 0,
  0, 0, 0, 1, 0, 0, 0, 3, 0,
  0, 0, 1, 0, 0, 0, 0, 6, 8,
  0, 0, 8, 5, 0, 0, 0, 1, 0,
  0, 9, 0, 0, 0, 0, 4, 0, 0,
])

if (result.success) {
  console.log(result.solution)
} else {
  switch (result.status) {
    case SolveStatus.invalidLength:
      console.error("配列の要素数が81ではありません。")
      break
    case SolveStatus.duplicated:
      console.error("重複があります。")
      break
    case SolveStatus.noEmpty:
      console.error("空白のマスがありません。")
      break
    case SolveStatus.unsolvable:
      console.error("解けませんでした。")
      break
  }
}
```

- 数独の盤面を表す81個の number 配列を solve に渡してください。空白のマスは 0 で表してください。
- 返り値は success プロパティをもつオブジェクトです。 success が true なら解けた、 false なら解けなかったことを表します。
- success が ture の場合は、 solution プロパティにソルブ済の配列が入っています。
- success が false の場合は、 status プロパティに失敗した原因を表すコード (number) が入っています。
  - SolveStatus.invalidLength (1)
    - 配列の要素数が81ではない（数独は全部で81マスなので）
  - SolveStatus.duplicated (2)
    - 重複がある（同じ列に同じ数字が2つ以上ある場合など）
  - SolveStatus.noEmpty (3)
    - 空白のマスが1つもない場合（解く必要がない）
  - SolveStatus.unsolvable (4)
    - 解けなかった（解なし）
  - SolveStatus.outOfRange (5)
    - 配列の要素に 0-9 の整数以外の値が含まれる
