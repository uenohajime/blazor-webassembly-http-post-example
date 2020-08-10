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

## Blazor で JSON オブジェクトを送る 2 つの方法

### テキストから JSON を作成してデータを送る場合

```
@page "/function"
@inject HttpClient Http

<h1>Test HTTP POST</h1>

<p>Received Data: @body</p>

<input @bind="modelName" />
<button class="btn btn-primary" @onclick="OnClickAsyncWithString">Send Data</button>

@code {
    private string functionUrl = @"http://localhost:7071/api/Function1";
    private string modelName;
    private string body = "";

    private async Task OnClickAsyncWithString(MouseEventArgs e)
    {
        var json = @"{""name"":""" + modelName + @"""}";
        var content = new StringContent(json, Encoding.UTF8);

        var receivedMessage = await Http.PostAsync(functionUrl, content);
        Console.WriteLine(await receivedMessage.Content.ReadAsStringAsync());
        body = await receivedMessage.Content.ReadAsStringAsync();
    }
}
```

### クラスから JSON を作成してデータを送る場合

```
@page "/function"
@inject HttpClient Http

<h1>Test HTTP POST</h1>

<p>Received Data: @body</p>

<input @bind="modelName" />
<button class="btn btn-primary" @onclick="OnClickAsyncWithClass">Send Data</button>

@code {
    private string functionUrl = @"http://localhost:7071/api/Function1";

    private class PostDataModel
    {
        [Required]
        public string name { get; set; }
    }

    private string modelName;
    private string body = "";

    private async Task OnClickAsyncWithClass(MouseEventArgs e)
    {
        PostDataModel postDataModel = new PostDataModel { name = modelName };

        var receivedMessage = await Http.PostAsJsonAsync(functionUrl, postDataModel);
        Console.WriteLine(await receivedMessage.Content.ReadAsStringAsync());
        body = await receivedMessage.Content.ReadAsStringAsync();
    }
```


## 参考サイト

* [Azure Function のローカル開発環境で CORS 設定する方法](https://github.com/dotnet/aspnetcore/issues/21321)
