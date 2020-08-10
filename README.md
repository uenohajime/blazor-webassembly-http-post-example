# Blazor Webassembly HTTP Post Example

Blazor WebAssembly で HTTP POST でデータを送るサンプルプロジェクトと、そのデータを受け取る Azure Functions のサンプルです。


## フォルダ構成

| フォルダ名 | 概要 |
| ---------- | ---- |
| BlazorApp2 | Blazor WebAssembly プロジェクトのフォルダ |
| FunctionApp2 | Azure Functions プロジェクトのフォルダ |


## 起動手順

1. FunctionApp2/FunctionApp2.sln をダブルクリックして、 Azure Functions プロジェクトの起動
2. "F5" キーを押して、ソリューションのデバッグを開始
3. BlazorApp2/BlazorApp2.sln をダブルクリックして、 Blazor WebAssembly プロジェクトの起動
4. "F5" キーを押して、ソリューションのデバッグを開始
5. 開いたブラウザで "Function" メニューを選択
6. "Send Data" ボタンを押す

## 参考サイト

* [Azure Function のローカル開発環境で CORS 設定する方法](https://github.com/dotnet/aspnetcore/issues/21321)
