---
title: .NET for Apache Spark の概要
description: Windows、macOS、Ubuntu で .NET Core を使用して .NET for Apache Spark アプリを実行する方法について説明します。
ms.date: 09/17/2020
ms.topic: tutorial
ms.custom: mvc
ms.author: luquinta
author: luisquintanilla
ms.openlocfilehash: 7afb35c9d02db1d1ee2bf04d565f79588b00695e
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/22/2020
ms.locfileid: "90866043"
---
# <a name="tutorial-get-started-with-net-for-apache-spark"></a>チュートリアル: .NET for Apache Spark の概要

このチュートリアルでは、Windows、macOS、Ubuntu で .NET Core を使用して .NET for Apache Spark アプリを実行する方法について説明します。

このチュートリアルでは、次の作業を行う方法について説明します。

> [!div class="checklist"]
>
> * .NET for Apache Spark の環境を準備する
> * 最初の .NET for Apache Spark アプリケーションを作成する
> * .NET for Apache Spark アプリケーションをビルドして実行する

[!INCLUDE [spark-preview-note](../../../includes/spark-preview-note.md)]

## <a name="prepare-your-environment"></a>環境を準備する

アプリの作成を開始する前に、いくつかの前提条件となる依存関係を設定する必要があります。 コマンド ライン環境から `dotnet`、`java`、`spark-shell` を実行できる場合は、環境が既に準備されているため、次のセクションに進むことができます。 コマンドのいずれかまたはすべてを実行できない場合は、次の手順を行います。

### <a name="1-install-net"></a>1..NET のインストール

.NET アプリのビルドを開始するには、.NET SDK (ソフトウェア開発キット) をダウンロードしてインストールする必要があります。

[.NET Core SDK](https://dotnet.microsoft.com/download/dotnet-core/3.1) をダウンロードしてインストールします。 SDK をインストールすると、`dotnet` ツールチェーンが PATH に追加されます。

.NET Core SDK をインストールしたら、新しいコマンド プロンプトまたはターミナルを開き、`dotnet` を実行します。

コマンドが実行され、dotnet の使用方法に関する情報が出力された場合は、次の手順に進むことができます。 `'dotnet' is not recognized as an internal or external command` エラーが発生した場合は、コマンドを実行する前に**新しい**コマンド プロンプトまたはターミナルを開いたことを確認してください。

### <a name="2-install-java"></a>2.Java のインストール

Windows および macOS の場合は [Java 8.1](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)、Ubuntu の場合は [OpenJDK 8](https://openjdk.java.net/install/) をインストールします。

ご使用のオペレーティング システムに適したバージョンを選択します。 たとえば、(次のように) Windows x64 マシンの場合は **jdk-8u201-windows-x64.exe**、macOS の場合は **jdk-8u231-macosx-x64.dmg** を選択します。 次に、コマンド `java` を使用してインストールを確認します。

![Java のダウンロード](https://dotnet.microsoft.com/static/images/java-jdk-downloads-windows.png?v=6BbJHoNyDO-PyYVciImr5wzh2AW_YHNcyb3p093AwPA)

### <a name="3-install-compression-software"></a>3.圧縮ソフトウェアのインストール

Apache Spark は、圧縮された .tgz ファイルとしてダウンロードされます。 [7-Zip](https://www.7-zip.org/)、[WinZip](https://www.winzip.com/) などの抽出プログラムを使用してファイルを抽出します。

### <a name="4-install-apache-spark"></a>4.Apache Spark のインストール

[Apache Spark をダウンロードしてインストールします](https://spark.apache.org/downloads.html)。 バージョン 2.3.*、2.4.0、2.4.1、2.4.3、または 2.4.4 から選択する必要があります (.NET for Apache Spark は、他のバージョンの Apache Spark と互換性がありません)。

次の手順で使用するコマンドは、[Apache Spark 2.4.1 をダウンロードしてインストールしていること](https://archive.apache.org/dist/spark/spark-2.4.1/spark-2.4.1-bin-hadoop2.7.tgz)を前提としています。 別のバージョンを使用する場合は、**2.4.1** を適切なバージョン番号に置き換えます。 その後、 **.tar** ファイルと Apache Spark ファイルを抽出します。

入れ子になった **.tar** ファイルを抽出するには、次のようにします。

* ダウンロードした **spark-2.4.1-bin-hadoop2.7.tgz** ファイルを見つけます。
* ファイルを右クリックし、 **[7-Zip] -> [ここに展開]** の順に選択します。
* ダウンロードした **.tgz** ファイルの横に **spark-2.4.1-bin-hadoop2.7.tar** が作成されます。

Apache Spark ファイルを抽出するには、次のようにします。

* **spark-2.4.1-bin-hadoop2.7.tar** を右クリックし、 **[7-Zip] -> [ここに展開]** の順に選択します
* **[展開先]** フィールドに「**C:\bin**」と入力します。
* **[展開先]** フィールドの下のチェックボックスをオフにします。
* **[OK]** を選択します。
* Apache Spark ファイルが C:\bin\spark-2.4.1-bin-hadoop2.7\ に抽出されます。

![Spark のインストール](https://dotnet.microsoft.com/static/images/spark-extract-with-7-zip.png?v=YvjUv54LIxI9FbALPC3h8zSQdyMtK2-NKbFOliG-f8M)

次のコマンドを実行して、Apache Spark を検索するために使用する環境変数を設定します。 Windows の場合は、管理者モードでコマンド プロンプトを実行してください。

#### <a name="windows"></a>[Windows](#tab/windows)

```console
setx /M HADOOP_HOME C:\bin\spark-2.4.1-bin-hadoop2.7\
setx /M SPARK_HOME C:\bin\spark-2.4.1-bin-hadoop2.7\
setx /M PATH "%PATH%;%HADOOP_HOME%;%SPARK_HOME%\bin"
```

#### <a name="maclinux"></a>[Mac/Linux](#tab/linux)

```bash
export SPARK_HOME=~/bin/spark-2.4.1-bin-hadoop2.7/
export PATH="$SPARK_HOME/bin:$PATH"
source ~/.bashrc
```

---

すべてをインストールし、環境変数を設定したら、**新しい**コマンド プロンプトまたはターミナルを開き、次のコマンドを実行します。

```text
spark-submit --version
```

コマンドが実行され、バージョン情報が出力された場合は、次の手順に進むことができます。

`'spark-submit' is not recognized as an internal or external command` エラーが発生した場合は、**新しい**コマンド プロンプトを開いたことを確認してください。

### <a name="5-install-net-for-apache-spark"></a>5..NET for Apache Spark のインストール

.NET for Apache Spark GitHub から、[Microsoft.Spark.Worker](https://github.com/dotnet/spark/releases) リリースをダウンロードします。 たとえば、Windows マシンを使用していて、.NET Core の使用を計画している場合は、[Windows x64 netcoreapp3.1 リリースをダウンロード](https://github.com/dotnet/spark/releases)します。

Microsoft.Spark.Worker を抽出するには、次のようにします。

* ダウンロードした **Microsoft.Spark.Worker.netcoreapp3.1.win-x64-0.8.0.zip** ファイルを見つけます。
* 右クリックし、 **[7-Zip] -> [ここに展開]** の順に選択します。
* **[展開先]** フィールドに「**C:\bin**」と入力します。
* **[展開先]** フィールドの下のチェックボックスをオフにします。
* **[OK]** を選択します。

![.NET Spark のインストール](https://dotnet.microsoft.com/static/images/dotnet-for-spark-extract-with-7-zip.png?v=jwCyum9mL0mGIi4V5zC7yuvLfcj1_nL-QFFD8TClhZk)

### <a name="6-install-winutils-windows-only"></a>6.WinUtils のインストール (Windows のみ)

.NET for Apache Spark では、Apache Spark と共に WinUtils をインストールする必要があります。 [winutils.exe をダウンロード](https://github.com/steveloughran/winutils/blob/master/hadoop-2.7.1/bin/winutils.exe)します。 次に、WinUtils を **C:\bin\spark-2.4.1-bin-hadoop2.7\bin** にコピーします。

> [!NOTE]
> Spark インストール フォルダー名の末尾に注釈が付けられている別のバージョンの Hadoop を使用している場合は、使用している Hadoop のバージョンと互換性のある[バージョンの WinUtils を選択](https://github.com/steveloughran/winutils)します。

### <a name="7-set-dotnet_worker_dir-and-check-dependencies"></a>7.DOTNET_WORKER_DIR の設定と依存関係の確認

次のコマンドのいずれかを実行して `DOTNET_WORKER_DIR` 環境変数を設定します。これは .NET アプリで .NET for Apache Spark を検索するために使用されます。 `<PATH-DOTNET_WORKER_DIR>` は、`Microsoft.Spark.Worker` をダウンロードして抽出したディレクトリに置き換えるようにしてください。 Windows の場合は、管理者モードでコマンド プロンプトを実行してください。

#### <a name="windows"></a>[Windows](#tab/windows)

```console
setx /M DOTNET_WORKER_DIR <PATH-DOTNET-WORKER-DIR>
```

#### <a name="maclinux"></a>[Mac/Linux](#tab/linux)

```bash
export DOTNET_WORKER_DIR=<PATH-DOTNET-WORKER-DIR>
```

---

最後に、次のセクションに進む前に、コマンド ラインから `dotnet`、`java`、`spark-shell` を実行できることを再度確認します。

## <a name="write-a-net-for-apache-spark-app"></a>.NET for Apache Spark アプリを作成する

### <a name="1-create-a-console-app"></a>1.コンソール アプリを作成する

コマンド プロンプトまたはターミナルで、次のコマンドを実行して、新しいコンソール アプリケーションを作成します。

```dotnetcli
dotnet new console -o MySparkApp
cd MySparkApp
```

`dotnet` コマンドで、種類が `console` の `new` アプリケーションを作成します。 `-o` パラメーターを指定すると、アプリを格納する *MySparkApp* という名前のディレクトリが作成され、必要なファイルが生成されます。 `cd MySparkApp` コマンドにより、作成したアプリ ディレクトリにディレクトリを変更できます。

### <a name="2-install-nuget-package"></a>2.NuGet パッケージのインストール

アプリで .NET for Apache Spark を使用するには、Microsoft.Spark パッケージをインストールします。 コマンド プロンプトまたはターミナルで、次のコマンドを実行します。

```dotnetcli
dotnet add package Microsoft.Spark
```

> [!NOTE]
> このチュートリアルでは、特に指定がない限り、最新バージョンの `Microsoft.Spark` NuGet パッケージを使用します。

### <a name="3-write-your-app"></a>3.アプリを作成する

Visual Studio Code または任意のテキスト エディターで *Program.cs* を開き、すべてのコードを次のコードで置き換えます。

```csharp
using Microsoft.Spark.Sql;
using static Microsoft.Spark.Sql.Functions;

namespace MySparkApp
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create Spark session
            SparkSession spark =
                SparkSession
                    .Builder()
                    .AppName("word_count_sample")
                    .GetOrCreate();

            // Create initial DataFrame
            string filePath = args[0];
            DataFrame dataFrame = spark.Read().Text(filePath);

            //Count words
            DataFrame words =
                dataFrame
                    .Select(Split(Col("value")," ").Alias("words"))
                    .Select(Explode(Col("words")).Alias("word"))
                    .GroupBy("word")
                    .Count()
                    .OrderBy(Col("count").Desc());

            // Display results
            words.Show();

            // Stop Spark session
            spark.Stop();
        }
    }
}
```

[SparkSession](xref:Microsoft.Spark.Sql.SparkSession) は Apache Spark アプリケーションのエントリ ポイントです。アプリケーションのコンテキストと情報を管理します。 [Text](xref:Microsoft.Spark.Sql.DataFrameReader.Text%2A) メソッドを使用し、`filePath` で指定したファイルから [DataFrame](xref:Microsoft.Spark.Sql.DataFrame) にテキスト データを読み取ります。 DataFrame は、データを一連の名前付き列に整理する方法です。 次に、一連の変換を適用してファイル内の文を分割し、各単語をグループ化して、カウントし、降順に並べ替えます。 これらの操作の結果は、別の DataFrame に格納されます。 この時点では、.NET for Apache Spark によるデータの遅延評価のため、操作が実行されていないことに注意してください。 `words` の変換された DataFrame の内容をコンソールに表示する [Show](xref:Microsoft.Spark.Sql.DataFrame.Show%2A) メソッドが呼び出されるまで、その上の行で定義されている操作は実行されません。 Spark セッションが不要になったら、[Stop](xref:Microsoft.Spark.Sql.SparkSession.Stop%2A) メソッドを使用してセッションを停止します。

### <a name="4-create-data-file"></a>4.データ ファイルを作成する

アプリでは、テキスト行を含むファイルが処理されます。 *MySparkApp* ディレクトリに、次のテキストを含む *input.txt* という名前のファイルを作成します。

```text
Hello World
This .NET app uses .NET for Apache Spark
This .NET app counts words with Apache Spark
```

変更を保存してファイルを閉じます。

## <a name="run-your-net-for-apache-spark-app"></a>.NET for Apache Spark アプリを実行する

次のコマンドを実行して、アプリケーションをビルドします。

```dotnetcli
dotnet build
```

ビルドの出力ディレクトリに移動し、`spark-submit` コマンドを使用して、Apache Spark 上で実行するアプリケーションを送信します。 `<version>` を使用する .NET ワーカーのバージョンに、`<path-of-input.txt>` を *input.txt* ファイルが格納されているパスに置き換えてください。

### <a name="windows"></a>[Windows](#tab/windows)

```console
spark-submit ^
--class org.apache.spark.deploy.dotnet.DotnetRunner ^
--master local ^
microsoft-spark-2.4.x-<version>.jar ^
dotnet MySparkApp.dll <path-of-input.txt>
```

### <a name="maclinux"></a>[Mac/Linux](#tab/linux)

```bash
spark-submit \
--class org.apache.spark.deploy.dotnet.DotnetRunner \
--master local \
microsoft-spark-2.4.x-<version>.jar \
dotnet MySparkApp.dll <path-of-input.txt>
```

---

> [!NOTE]
> このコマンドは、Apache Spark をダウンロードして PATH 環境変数に追加し、`spark-submit` を使用できる状態であることを前提としています。 そうでなければ、完全なパスを使用する必要があります (たとえば、*C:\bin\apache-spark\bin\spark-submit* や *~/spark/bin/spark-submit*)。

アプリを実行すると、*input.txt* ファイルのワード カウント データがコンソールに書き込まれます。

```console
+------+-----+
|  word|count|
+------+-----+
|  .NET|    3|
|Apache|    2|
|   app|    2|
|  This|    2|
| Spark|    2|
| World|    1|
|counts|    1|
|   for|    1|
| words|    1|
|  with|    1|
| Hello|    1|
|  uses|    1|
+------+-----+
```

おめでとうございます! .NET for Apache Spark アプリの作成と実行が正常に完了しました。

## <a name="next-steps"></a>次の手順

このチュートリアルでは、以下の内容を学習しました。
> [!div class="checklist"]
>
> * .NET for Apache Spark の環境を準備する
> * 最初の .NET for Apache Spark アプリケーションを作成する
> * .NET for Apache Spark アプリケーションをビルドして実行する

上記の手順を説明したビデオを見るには、[.NET for Apache Spark 101 ビデオ シリーズ](https://channel9.msdn.com/Series/NET-for-Apache-Spark-101/Run-Your-First-NET-for-Apache-Spark-App)を参照してください。

詳細については、リソースのページを参照してください。
> [!div class="nextstepaction"]
> [.NET for Apache Spark のリソース](../resources/index.md)
