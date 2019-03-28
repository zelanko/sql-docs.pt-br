---
title: Criar objetos de dados do SQL Server usando RevoScaleR RxSqlServerData - aprendizagem de máquina do SQL Server
description: Tutorial passo a passo sobre como criar objetos de dados usando a linguagem R no SQL Server.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/26/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 45643dbcdc2876fe0794ddb731abe6334537169c
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510353"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-server-and-revoscaler-tutorial"></a>Criar objetos de dados do SQL Server usando RxSqlServerData (tutorial do SQL Server e o RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lição é parte do [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre como usar [funções RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Lição dois é uma continuação da criação do banco de dados: adição de tabelas e carregamento de dados. Se um DBA criado o banco de dados e o logon no [lição uma](deepdive-work-with-sql-server-data-using-r.md), você pode adicionar tabelas usando um IDE R, como RStudio ou como uma ferramenta interna **Rgui**.

A partir do R, conecte-se ao SQL Server e use **RevoScaleR** funções para executar as tarefas a seguir:

> [!div class="checklist"]
> * Criar tabelas de dados de treinamento e previsões
> * Carregar tabelas com dados de um arquivo. csv local

Dados de exemplo são dados de fraude de cartão de crédito simulados (ccFraud conjunto de dados), particionados em treinamento e conjuntos de dados de pontuação. O arquivo de dados está incluído no **RevoScaleR**.

Usar um IDE R ou **Rgui** para concluir esses leva. Certifique-se de usar os executáveis do R encontrados neste local: C:\Program Files\Microsoft\R Client\R_SERVER\bin\x64 (ambos Rgui.exe se você estiver usando essa ferramenta, ou um IDE R apontando para C:\Program Files\Microsoft\R Client\R_SERVER). Ter uma [estação de trabalho de cliente R](../r/set-up-a-data-science-client.md) com esses executáveis é considerado um pré-requisito deste tutorial.

## <a name="create-the-training-data-table"></a>Criar a tabela de dados de treinamento

1. Store a cadeia de caracteres de conexão de banco de dados em uma variável do R. Abaixo estão dois exemplos de cadeias de caracteres de conexão ODBC válidas para o SQL Server: um usando um logon SQL e outro para a autenticação integrada do Windows. 

   Certifique-se de modificar o nome do servidor, nome de usuário e senha, conforme apropriado.

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
  
    Como a instância do servidor e o nome do banco de dados já foram especificados como parte da cadeia de conexão, quando você combina as duas variáveis, o *totalmente qualificado* torna-se do nome da nova tabela  *ccfraudsmall*.
  
3.  Opcionalmente, especifique *rowsPerRead* para controlar quantas linhas de dados são lidas em cada lote.
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    Embora esse parâmetro é opcional, defini-lo pode resultar em cálculos mais eficientes. A maioria das funções analíticas avançadas no **RevoScaleR** e **MicrosoftML** processa dados em partes. O *rowsPerRead* parâmetro determina o número de linhas em cada parte.
  
    Talvez você precise fazer experiências com essa configuração para encontrar o equilíbrio certo. Se o valor for muito grande, acesso a dados pode ser lento se não houver memória suficiente para processar dados em partes desse tamanho. Por outro lado, em alguns sistemas, se o valor de *rowsPerRead* for muito pequeno, o desempenho pode também reduzir.
  
    Como um valor inicial, use o tamanho padrão do processo em lote definido pela instância do mecanismo de banco de dados para controlar o número de linhas em cada parte (5.000 linhas). Salve esse valor na variável *sqlRowsPerRead*.
  
4.  Defina uma variável para o novo objeto de fonte de dados e passe os argumentos definidos anteriormente para o **RxSqlServerData** construtor. Observe que isso só cria o objeto da fonte de dados, mas não o preenche. Carregamento de dados é uma etapa separada.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

## <a name="create-the-scoring-data-table"></a>Criar tabela de dados de pontuação

Usando as mesmas etapas, crie a tabela que contém os dados de pontuação usando o mesmo processo.

1. Crie uma nova variável do R, *sqlScoreTable*, para armazenar o nome da tabela usada para pontuação.
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. Forneça essa variável como um argumento para a função **RxSqlServerData** para definir um segundo objeto da fonte de dados, *sqlScoreDS*.
  
    ```R
    sqlScoreDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

Como você já definiu a cadeia de caracteres de conexão e outros parâmetros como variáveis no espaço de trabalho do R, você pode reutilizá-lo para novas fontes de dados que representam diferentes tabelas, exibições ou consultas.

> [!NOTE]
> A função usa argumentos diferentes para definir uma fonte de dados com base em uma tabela inteira que para uma fonte de dados com base em uma consulta. Isso ocorre porque o mecanismo de banco de dados do SQL Server deve preparar as consultas de forma diferente. Mais tarde neste tutorial, você aprenderá como criar um objeto de fonte de dados com base em uma consulta SQL.

## <a name="load-data-into-sql-tables-using-r"></a>Carregar dados em tabelas SQL usando o R

Agora que você criou as tabelas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , é possível carregar dados nelas usando a função **Rx** apropriada.

O **RevoScaleR** pacote contém funções específicas para os tipos de fonte de dados. Para dados de texto, use [RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata) para gerar o objeto de fonte de dados. Há outras funções para criar objetos da fonte de dados com base em dados do Hadoop, dados ODBC e assim por diante.

> [!NOTE]
> Para essa seção, você deve ter **execução de DDL** permissões no banco de dados.

### <a name="load-data-into-the-training-table"></a>Carregar dados na tabela de treinamento

1. Criar uma variável do R *ccFraudCsv*e atribua à variável o caminho do arquivo para o arquivo CSV que contém os dados de exemplo. Esse conjunto de dados é fornecido em **RevoScaleR**. "sampleDataDir" é uma palavra-chave sobre o **rxGetOption** função.
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    Observe a chamada para **rxGetOption**, que é o método GET associado [rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions) na **RevoScaleR**. Use esse utilitário para definir e listam as opções relacionam aos contextos de computação local e remota, como o diretório compartilhado padrão ou o número de processadores (núcleos) a serem usados em cálculos.
    
    Essa chamada específica obtém os exemplos da biblioteca correta, independentemente de onde você está executando seu código. Por exemplo, experimente executar a função no SQL Server e no seu computador de desenvolvimento e veja como os caminhos diferem.
  
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
  
3. Neste ponto, talvez você queira pausar um instante e exibir seu banco de dados em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Atualize a lista de tabelas no banco de dados.
  
    Você pode ver que, embora os objetos de dados de R criou seu espaço de trabalho local, as tabelas não foram criadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados. Além disso, nenhum dado foi carregado do arquivo de texto para a variável de R.
  
4. Inserir os dados, chamando a função [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) função.
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
    
    Após uma pequena pausa, supondo que não haja nenhum problema com a cadeia de conexão, você deve ver resultados como estes:
  
    *Total de linhas gravadas: 10000, tempo total: 0,466* *linhas lidas: 10000, total de linhas processadas: 10000, tempo total de bloco: 0,577 segundo*
  
5. Atualize a lista de tabelas. Para verificar se cada variável tem os tipos de dados correto e se foi importado com êxito, você pode também botão direito do mouse em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e selecione **selecionar 1000 linhas superiores**.

### <a name="load-data-into-the-scoring-table"></a>Carregar dados na tabela de pontuação

1. Repita as etapas para carregar o conjunto de dados usado para pontuação no banco de dados.
  
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
  
    - Se a tabela já existir e você não usa o *substituir* opção, os resultados são inseridos sem truncamento.
  
Novamente, se a conexão foi bem-sucedida, você verá uma mensagem indicando a conclusão e o tempo necessário para gravar os dados na tabela:

*Total de linhas gravadas: 10000, tempo total: 0,384*
*linhas lidas: 10000, total de linhas processadas: 10000, tempo total de bloco: 0,456 segundo*

## <a name="more-about-rxdatastep"></a>Mais sobre rxDataStep

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) é uma função avançada que pode executar várias transformações em um quadro de dados de R. Você também pode usar o rxDataStep para converter os dados na representação exigida pelo destino: nesse caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Opcionalmente, você pode especificar transformações nos dados, usando funções do R nos argumentos para **rxDataStep**. Exemplos dessas operações são fornecidos posteriormente neste tutorial.

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Consultar e modificar os dados do SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)