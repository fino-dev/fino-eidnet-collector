# コーディングルール

## 型ヒント
- 全関数・全メソッドに型ヒントを必須とする
- public APIは特に厳密に型を記述する

---

## テスト
- pytest を前提とする
- 新しいユースケースを追加する場合、対応するテストを追加すること
- adapters層のテストは統合テスト寄りでも可

---

## ロギング
- logging モジュールを使用する
- printは禁止
- loggerは各モジュールで以下の形式で定義する

```python
import logging
logger = logging.getLogger(__name__)
```

Agent駆動開発ルール

Agentによる開発では以下を厳守する。

実装単位
	•	クラス単位
	•	ユースケース単位

開発フロー
	1.	設計を文章で明確化
	2.	実装
	3.	テスト

この順序を必ず守る。

⸻

クラス設計ルール
	•	各クラスには「責務を示すコメント」を必ず記述する
	•	publicメソッドには簡潔なdocstringを書く
    •   parameterやresponseの説明はコメントに含めない


⸻

依存ルール
	•	adapters層 → domain/application への依存は許可
	•	domain/application層 → adapters層への依存は禁止
	•	循環importは禁止

⸻

公開範囲ルール
	•	Facadeクラスのみを正式な公開APIとする
	•	その他クラスは内部利用前提とする
	•	__all__ を用いて公開対象を明示する