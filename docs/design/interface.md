# Packageのインターフェース

## ユースケース

### 1. Getting Started Usecase

```python
# simple local usecase
import fino-eidnet-collector as fec

# decide wheare to collect filings. it's depending on your usecase and environmnet
collection = fec.Collection(root_path="~/.edinet_file")

edinet = fec.Edinet(api_key="hogehgoehogheohoge", collection=collection)
edinet.sync_catalog()

result = edinet.collect(form_type=FormatType.ANNUAL)
result.filings[0] # Filing Class with file path
filing = filings[0]
filing_name = filing.name
filing_path = filing.path # easy to access file from result
file = filing.open()


collection.search(sec_code="1111")
collection.get(docd="hgoehgeo")

result.collection # provide same collection object from collect func result
```

```python
# custom collection partition
import fino-eidnet-collector as fec, SpecField, CustomField

fun ticker_generate(filing: FilingMetadata) -> str:
    ticker = mapping_ticker_from_sec(filing.sec_code)

    return ticker


# customize directory partitions as user want to mangage
collection_spec = fec.CollectionSpec(
    partition=[
        SpecFiled.SEC_CODE,
        SpecFiled.DOCUMENT_TYPE,
        SpecFiled.PERIOD_START,
        CustomSpecField("ticker", ticker_generate)
    ],
    file_name=[
        SpecFiled.DOCUMENT_ID,
        SpecFiled.FORMAT_TYPE
    ]
)

collection = fec.Collection(type="s3", spec=collection_spec)

edinet = fec.Edinet(api_key="hogehgoehogheohoge", collection=collection)
```

\*\*

- file pathの衝突はdoc_idをfile_nameに必須にすることで回避する
- format typeによる衝突はdocument idで回避できない（単一doc idで複数のformatが存在する）ため、ファイルの拡張子prefixとして自動挿入する
- \*\*
