---
title: Criar SQL Server objetos de dados usando RevoScaleR RxSqlServerData
description: Tutorial explicativo sobre como criar objetos de dados usando a linguagem R no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 423a90fe66749a3192c6f03c0efee314b4ceef37
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469757"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-server-and-revoscaler-tutorial"></a>Criar SQL Server objetos de dados usando o RxSqlServerData (tutorial SQL Server e RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Esta lição faz parte do [tutorial do RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar as [funções do RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com SQL Server.

A lição dois é uma continuação da criação do banco de dados: adição de tabelas e carregamento. Se um DBA criou o banco de dados e fizer logon na [lição um](deepdive-work-with-sql-server-data-using-r.md), você poderá adicionar tabelas usando um IDE R como RStudio ou uma ferramenta interna como **Rgui**.

No R, conecte-se a SQL Server e use as funções **RevoScaleR** para executar as tarefas seguir:

> [!div class="checklist"]
> * Criar tabelas para dados de treinamento e previsões
> * Carregar tabelas com dados de um arquivo. csv local

Os dados de exemplo são dados simulados de fraudes de cartão de crédito (o DataSet ccFraud), particionados em conjuntos de dado de treinamento e pontuação. O arquivo de dados está incluído no **RevoScaleR**.

Use um R IDE ou **Rgui** para concluir esses demora. Certifique-se de usar os executáveis do R encontrados neste local: C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 (Rgui. exe se você estiver usando essa ferramenta ou um IDE do R apontando para C:\Program Files\Microsoft\R Client\R_SERVER). Ter uma [estação de trabalho cliente R](../r/set-up-a-data-science-client.md) com esses executáveis é considerada um pré-requisito deste tutorial.

## <a name="create-the-training-data-table"></a>Criar a tabela de dados de treinamento

1. Armazene a cadeia de conexão do banco de dados em uma variável do R. Abaixo estão dois exemplos de cadeias de conexão ODBC válidas para SQL Server: uma usando um logon do SQL e outra para a autenticação integrada do Windows. 

   Certifique-se de modificar o nome do servidor, o nome de usuário e a senha conforme apropriado.

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
  
    Como a instância de servidor e o nome do banco de dados já estão especificados como parte da cadeia de conexão, quando você combina as duas variáveis, o nome *totalmente qualificado* da nova tabela torna-se *instance. Database. Schema. ccFraudSmall*.
  
3.  Opcionalmente, especifique *rowsPerRead* para controlar quantas linhas de dados são lidas em cada lote.
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    Embora esse parâmetro seja opcional, configurá-lo pode resultar em cálculos mais eficientes. A maioria das funções analíticas aprimoradas nos dados de processo **RevoScaleR** e **MicrosoftML** em partes. O parâmetro *rowsPerRead* determina o número de linhas em cada parte.
  
    Talvez seja necessário experimentar essa configuração para encontrar o equilíbrio certo. Se o valor for muito grande, o acesso aos dados poderá ser lento se não houver memória suficiente para processar dados em partes desse tamanho. Por outro lado, em alguns sistemas, se o valor de *rowsPerRead* for muito pequeno, o desempenho também poderá ficar lento.
  
    Como um valor inicial, use o tamanho do processo em lote padrão definido pela instância do mecanismo de banco de dados para controlar o número de linhas em cada parte (5.000 linhas). Salve esse valor na variável *sqlRowsPerRead*.
  
4.  Defina uma variável para o novo objeto de fonte de dados e passe os argumentos definidos anteriormente para o construtor **RxSqlServerData** . Observe que isso só cria o objeto da fonte de dados, mas não o preenche. O carregamento de dados é uma etapa separada.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

## <a name="create-the-scoring-data-table"></a>Criar a tabela de dados de Pontuação

Usando as mesmas etapas, crie a tabela que contém os dados de Pontuação usando o mesmo processo.

1. Crie uma nova variável do R, *sqlScoreTable*, para armazenar o nome da tabela usada para pontuação.
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. Forneça essa variável como um argumento para a função **RxSqlServerData** para definir um segundo objeto da fonte de dados, *sqlScoreDS*.
  
    ```R
    sqlScoreDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

Como você já definiu a cadeia de conexão e outros parâmetros como variáveis no espaço de trabalho do R, você pode reutilizá-la para novas fontes de dados que representam diferentes tabelas, exibições ou consultas.

> [!NOTE]
> A função usa argumentos diferentes para definir uma fonte de dados com base em uma tabela inteira do que para uma fonte de dados com base em uma consulta. Isso ocorre porque o mecanismo de banco de dados SQL Server deve preparar as consultas de forma diferente. Posteriormente neste tutorial, você aprenderá a criar um objeto de fonte de dados com base em uma consulta SQL.

## <a name="load-data-into-sql-tables-using-r"></a>Carregar dados em tabelas SQL usando o R

Agora que você criou as tabelas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , é possível carregar dados nelas usando a função **Rx** apropriada.

O pacote **RevoScaleR** contém funções específicas para tipos de fonte de dados. Para dados de texto, use [RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata) para gerar o objeto de fonte de dados. Há outras funções para criar objetos da fonte de dados com base em dados do Hadoop, dados ODBC e assim por diante.

> [!NOTE]
> Para esta seção, você deve ter permissões **Executar DDL** no banco de dados.

### <a name="load-data-into-the-training-table"></a>Carregar dados na tabela de treinamento

1. Crie uma variável de R, *ccFraudCsv*, e atribua à variável o caminho do arquivo CSV que contém os dados de exemplo. Esse DataSet é fornecido em **RevoScaleR**. O "sampleDataDir" é uma palavra-chave na função **rxGetOption** .
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    Observe a chamada para **rxGetOption**, que é o método Get associado a [rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions) em **RevoScaleR**. Use este utilitário para definir e listar opções relacionadas a contextos de computação locais e remotos, como o diretório compartilhado padrão ou o número de processadores (núcleos) a serem usados em cálculos.
    
    Essa chamada em particular Obtém os exemplos da biblioteca correta, independentemente de onde você está executando seu código. Por exemplo, experimente executar a função no SQL Server e no seu computador de desenvolvimento e veja como os caminhos diferem.
  
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
  
    Você pode ver que, embora os objetos de dados do R tenham sido criados no seu espaço de trabalho local, as tabelas não foram [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criadas no banco de dado. Além disso, nenhum dado foi carregado do arquivo de texto para a variável de R.
  
4. Insira os dados chamando a função [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) function.
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
    
    Após uma pequena pausa, supondo que não haja nenhum problema com a cadeia de conexão, você deve ver resultados como estes:
  
    *Total de linhas gravadas: 10000, tempo total:*  0,466*linhas lidas: 10000, total de linhas processadas: 10000, tempo total da parte: 0,577 segundos*
  
5. Atualize a lista de tabelas. Para verificar se cada variável tem os tipos de dados corretos e foi importada com êxito, você também pode clicar com [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o botão direito do mouse na tabela no e selecionar **selecionar as 1000 linhas superiores**.

### <a name="load-data-into-the-scoring-table"></a>Carregar dados na tabela de Pontuação

1. Repita as etapas para carregar o conjunto de dados usado para pontuação no banco de dado.
  
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
  
    - Se a tabela já existir e você não usar a opção de *substituição* , os resultados serão inseridos sem truncamento.
  
Novamente, se a conexão foi bem-sucedida, você verá uma mensagem indicando a conclusão e o tempo necessário para gravar os dados na tabela:

*Total de linhas gravadas: 10000, tempo total: 0,384*linhaslidas *:
 10000, total de linhas processadas: 10000, tempo total da parte: 0,456 segundos*

## <a name="more-about-rxdatastep"></a>Mais sobre rxDataStep

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) é uma função poderosa que pode executar várias transformações em um quadro de dados do R. Você também pode usar rxDataStep para converter dados na representação exigida pelo destino: nesse caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Opcionalmente, você pode especificar transformações nos dados, usando as funções do R nos argumentos para **rxDataStep**. Exemplos dessas operações são fornecidos posteriormente neste tutorial.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Consultar e modificar os dados do SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)