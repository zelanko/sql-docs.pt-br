---
title: Criar objetos RxSqlServerData
description: 'Tutorial 2 do RevoScaleR: Como criar objetos de dados usando a linguagem R no SQL Server.'
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 7869fc3fc67cb24542223c2300cd7b6ebcf1eb41
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76922567"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-server-and-revoscaler-tutorial"></a>Criar objetos de dados do SQL Server usando RxSqlServerData (tutorial do SQL Server e do RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Este é o tutorial 2 da [série de tutoriais do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Este tutorial é uma continuação da criação do banco de dados: adição de tabelas e carregamento de dados. Caso um DBA tenha criado o banco de dados e feito logon no [Tutorial 2](deepdive-work-with-sql-server-data-using-r.md), será possível adicionar tabelas usando um IDE R como o RStudio ou uma ferramenta interna como o **Rgui**.

No R, conecte-se ao SQL Server e use as funções do **RevoScaleR** para executar as seguintes tarefas:

> [!div class="checklist"]
> * Criar tabelas para dados de treinamento e previsões
> * Carregar tabelas com os dados de um arquivo .csv local

Os dados de exemplo são dados simulados de fraudes de cartão de crédito (o conjunto de dados ccFraud), particionados em conjuntos de dados de treinamento e pontuação. O arquivo de dados está incluído em **RevoScaleR**.

Use um IDE do R ou **Rgui** para concluir essas tarefas. Use os executáveis do R encontrados nesta localização: C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 (Rgui.exe se você estivar usando essa ferramenta ou um IDE do R que está apontando para C:\Program Files\Microsoft\R Client\R_SERVER). Ter uma [estação de trabalho cliente R](../r/set-up-a-data-science-client.md) com esses executáveis é considerado um pré-requisito deste tutorial.

## <a name="create-the-training-data-table"></a>Criar a tabela de dados de treinamento

1. Armazene a cadeia de conexão de banco de dados em uma variável do R. Abaixo há dois exemplos de cadeias de conexão ODBC válidas para SQL Server: uma que usa um logon do SQL e outra para autenticação integrada do Windows. 

   Lembre-se de modificar o nome do servidor, nome de usuário e senha, conforme adequado.

    **Logon do SQL**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=<server-name>; Database=RevoDeepDive;Uid=<user_name>;Pwd=<password>"
    ```

    **Autenticação do Windows**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=<server-name>;Database=RevoDeepDive;Trusted_Connection=True"
    ```

2. Especifique o nome da tabela que você quer criar e salve-o em uma variável do R.
  
    ```R
    sqlFraudTable <- "ccFraudSmall"
    ```
  
    Como a instância do servidor e o nome do banco de dados já foram especificados como parte da cadeia de conexão, quando você combina as duas variáveis, o nome *totalmente qualificado* da nova tabela se torna em *instance.database.schema.ccFraudSmall*.
  
3.  Opcionalmente, especifique *rowsPerRead* para controlar quantas linhas de dados são lidas em cada lote.
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    Embora esse parâmetro seja opcional, configurá-lo pode resultar em cálculos mais eficientes. A maioria das funções analíticas aprimoradas no **RevoScaleR** e **MicrosoftML** processam dados em partes. O parâmetro *rowsPerRead* determina o número de linhas em cada parte.
  
    Talvez seja necessário experimentar essa configuração para encontrar o equilíbrio certo. Se o valor for muito grande, o acesso a dados poderá ser lento se não houver memória suficiente para processar os dados em partes desse tamanho. Por outro lado, em alguns sistemas, se o valor de *rowsPerRead* for muito pequeno, o desempenho poderá desacelerar também.
  
    Como um valor inicial, use o tamanho do processo em lote padrão definido pela instância do mecanismo de banco de dados para controlar o número de linhas em cada parte (5 mil linhas). Salve esse valor na variável *sqlRowsPerRead*.
  
4.  Defina uma variável para o novo objeto de fonte de dados e passe os argumentos definidos anteriormente para o construtor **RxSqlServerData**. Observe que isso só cria o objeto da fonte de dados, mas não o preenche. O carregamento de dados é uma etapa separada.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

## <a name="create-the-scoring-data-table"></a>Criar a tabela de dados de pontuação

Usando as mesmas etapas, crie a tabela que armazena os dados de pontuação usando o mesmo processo.

1. Crie uma nova variável do R, *sqlScoreTable*, para armazenar o nome da tabela usada para pontuação.
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. Forneça essa variável como um argumento para a função **RxSqlServerData** para definir um segundo objeto da fonte de dados, *sqlScoreDS*.
  
    ```R
    sqlScoreDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

Como você já definiu a cadeia de conexão e outros parâmetros como variáveis no workspace do R, pode usá-la novamente para novas fontes de dados que representam diferentes tabelas, exibições ou consultas.

> [!NOTE]
> A função usa argumentos diferentes para definir uma fonte de dados com base em uma tabela inteira do que para uma fonte de dados com base em uma consulta. Isso ocorre porque o mecanismo de banco de dados do SQL Server deve preparar as consultas de forma diferente. Mais adiante neste tutorial, você aprenderá a criar um objeto de fonte de dados com base em uma consulta SQL.

## <a name="load-data-into-sql-tables-using-r"></a>Carregar dados em tabelas SQL usando o R

Agora que você criou as tabelas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , é possível carregar dados nelas usando a função **Rx** apropriada.

O pacote **RevoScaleR** contém funções específicas para os tipos de fonte de dados. Para dados de texto, use [RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata) para gerar o objeto de fonte de dados. Há outras funções para criar objetos da fonte de dados com base em dados do Hadoop, dados ODBC e assim por diante.

> [!NOTE]
> Para esta seção, você deve ter permissões **Executar DDL** no banco de dados.

### <a name="load-data-into-the-training-table"></a>Carregar dados na tabela de treinamento

1. Crie uma variável do R, *ccFraudCsv*, e atribua à variável o caminho para o arquivo CSV que contém os dados de exemplo. Esse conjunto de dados é fornecido no **RevoScaleR**. O "sampleDataDir" é uma palavra-chave na função **rxGetOption**.
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    Observe a chamada a **rxGetOption**, que é o método GET associado a [rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions) no **RevoScaleR**. Use este utilitário para definir e listar opções relacionadas aos contextos de computação local e remota, como o diretório compartilhado padrão, ou o número de processadores (núcleos) a serem usados em cálculos.
    
    Essa chamada específica obtém os exemplos da biblioteca correta, independentemente do local em que seu código está em execução. Por exemplo, experimente executar a função no SQL Server e no seu computador de desenvolvimento e veja como os caminhos diferem.
  
2. Defina uma variável para armazenar os novos dados e use a função **RxTextData** para especificar a fonte de dados de texto.
  
    ```R
    inTextData <- RxTextData(file = ccFraudCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer",
        "fraudRisk" = "integer"))
    ```
  
    O argumento *colClasses* é importante. Você pode usá-lo para indicar o tipo de dados que será atribuído a cada coluna de dados carregados do arquivo de texto. Neste exemplo, todas as colunas são tratadas como texto, exceto pelas colunas nomeadas, que são tratadas como inteiros.
  
3. Neste ponto, talvez você queira pausar um momento e exibir seu banco de dados no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Atualize a lista de tabelas no banco de dados.
  
    Você pode ver que, embora os objetos de dados do R tenham sido criados no workspace local, as tabelas não foram criadas no banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Além disso, nenhum dado foi carregado do arquivo de texto para a variável do R.
  
4. Insira os dados chamando a função [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep).
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
    
    Após uma pequena pausa, supondo que não haja nenhum problema com a cadeia de conexão, você deve ver resultados como estes:
  
    *Total de linhas gravadas: 10000, Tempo total: 0,466* *linhas lidas: 10000, Total de linhas processadas: 10000, Tempo total da parte: 0,577 segundo*
  
5. Atualize a lista de tabelas. Para verificar se cada variável tem os tipos de dados corretos e se foi importada com êxito, você também pode clicar com o botão direito do mouse na tabela em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e selecione **Selecionar as Primeiras 1000 Linhas**.

### <a name="load-data-into-the-scoring-table"></a>Carregar dados para a tabela de pontuação

1. Repita essas etapas para carregar o conjunto de dados usado para pontuação no banco de dados.
  
    Comece fornecendo o caminho para o arquivo de origem.
  
    ```R
    ccScoreCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudScoreSmall.csv")
    ```
  
2. Use a função **RxTextData** para obter os dados e salvá-los na variável, *inTextData*.
  
    ```R
    inTextData <- RxTextData(file = ccScoreCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer"))
    ```
  
3.  Chame a função **rxDataStep** para substituir a tabela atual pelo novo esquema e pelos novos dados.
  
    ```R
    rxDataStep(inData = inTextData, sqlScoreDS, overwrite = TRUE)
    ```
  
    - O argumento *inData* define a fonte de dados que será usada.
  
    - O argumento *outFile* especifica a tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que você quer salvar os dados.
  
    - Se a tabela já existir e você não usar a opção *substituir*, os resultados serão inseridos sem truncamento.
  
Novamente, se a conexão foi bem-sucedida, você verá uma mensagem indicando a conclusão e o tempo necessário para gravar os dados na tabela:

*Total de linhas gravadas: 10000, Tempo total: 0,384*
*Linhas lidas: 10000, Total de linhas processadas: 10000, Tempo total da parte: 0,456 segundo*

## <a name="more-about-rxdatastep"></a>Mais sobre rxDataStep

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) é uma função avançada que pode executar várias transformações em um quadro de dados do R. Você também pode usar rxDataStep para converter na representação exigida pelo destino: neste caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Opcionalmente, você pode especificar transformações nos dados usando funções do R nos argumentos para **rxDataStep**. Exemplos dessas operações são fornecidos posteriormente neste tutorial.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Consultar e modificar os dados do SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)