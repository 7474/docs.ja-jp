### <a name="xsd-schema-validation-now-correctly-detects-violations-of-unique-constraints-if-compound-keys-are-used-and-one-key-is-empty"></a>XSD スキーマ検証は、複合キーが使用され、1 つのキーが空の場合に、一意制約の違反を正しく検出するようになりました

|   |   |
|---|---|
|説明|.NET Framework 4.6 より前のバージョンには、キーの 1 つが空であった場合、XSD 検証で複合キーの一意制約が検出されないというバグがありました。 .NET Framework 4.6 で、この問題は修正されました。 このため、より正しい検証が行われるようになりますが、以前は検証されていた XML の一部が検証されない可能性もあります。|
|提案される解決策|より緩やかな .NET Framework 4.0 の検証が必要な場合、検証アプリケーションはバージョン 4.5 (またはそれ以前) の .NET Framework をターゲットにできます。 ただし、.NET Framework 4.6 に再ターゲットするときには、コード レビューを行って、重複する複合キー (この問題の説明で述べられているように) の検証を予期していないことを確認する必要があります。|
|スコープ|エッジ|
|Version|4.6|
|型|再ターゲット中|

