# Packageのインターフェース

## 公開クラス

### EdinetCollector

#### メソッド

- sync_catalog
- search_catalog
- collect
- list_collection

```python
class EdinetCollector:

    def sync_catalog(self) -> None:
        """EDINETの書類一覧をローカルDBに同期する"""

    def search_catalog(
        self,
        *,
        company: str | None = None,
        date_from: date | None = None,
        date_to: date | None = None,
        doc_type: str | None = None,
    ) -> list[Document]:
        """条件に基づいて書類一覧を検索する"""

    def collect(
        self,
        documents: list[Document],
        output_dir: str | None = None,
    ) -> list[CollectedDocument]:
        """指定された書類をダウンロードして保存する"""

    def list_collection(self) -> list[CollectedDocument]:
        """これまでに収集した書類一覧を返す"""
```

#### ユースケース

##### 書類収集のながれ(メイン機能)

```python
from fino_edinet_collector import EdinetCollector

collector = EdinetCollector(api_key="YOUR_API_KEY")

# 一覧を同期
collector.sync_catalog()

# トヨタの有価証券報告書を検索
docs = collector.search(
    company="トヨタ",
    doc_type="有価証券報告書"
)

# ダウンロード
collector.collect(docs, output_dir="./data")
```
