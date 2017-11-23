---
title: Criar Objetos de Dados do SQL Server usando RxSqlServerData | Microsoft Docs
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: bcf5f7ff-795b-4815-b163-bcddd496efce
caps.latest.revision: "18"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7eecfb2ce8a6cfe525b07aa8c6636c7dd77b0d30
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata"></a>Criar Objetos de Dados do SQL Server usando RxSqlServerData

Agora que você criou o banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e tem as permissões necessárias para trabalhar com os dados, você criará objetos no R que permitem trabalhar com os dados – no servidor e na estação de trabalho.

## <a name="create-the-sql-server-data-objects"></a>Criar os Objetos de Dados do SQL Server

Nesta etapa, você usará o R para criar e preencher duas tabelas. Ambas as tabelas contêm dados de fraude de cartão de crédito simulados. Uma tabela é usada para treinar os modelos e a outra é usada para pontuá-los.

Para criar tabelas no computador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] remoto, você usará a função **RxSqlServerData** fornecida no pacote **RevoScaleR** .

> [!TIP]
> Se você estiver usando as ferramentas de R para o Visual Studio, selecione **Ferramentas de R** na barra de ferramentas e clique em **Windows** para ver as opções de depuração e exibir as variáveis do R.

### <a name="create-the-training-data-table"></a>Criar a tabela de dados de treinamento

1. Forneça a cadeia de conexão do banco de dados em uma variável do R. Aqui, fornecemos dois exemplos de cadeias de caracteres de conexão ODBC válidas para o SQL Server: um que usa um logon do SQL e outro para a autenticação integrada do Windows (recomendada).

    **Usando um logon do SQL**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name; Database=DeepDive;Uid=user_name;Pwd=password"
    ```

    **Usando a autenticação do Windows**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name;Database=DeepDive;Trusted_Connection=True"
    ```

    Lembre-se de modificar o nome da instância, o nome do banco de dados, o nome de usuário e a senha, conforme apropriado.
  
2. Especifique o nome da tabela que você quer criar e salve-o em uma variável do R.
  
    ```R
    sqlFraudTable <- "ccFraudSmall"
    ```
  
    Como a instância e o nome do banco de dados já foram especificados como parte da cadeia de conexão, quando você combina as duas variáveis, o nome *totalmente qualificado* da nova tabela se transforma em _instance.database.schema.ccFraudSmall_.
  
3.  Antes de criar uma instância do objeto da fonte de dados, adicione uma linha especificando um parâmetro adicional, *rowsPerRead*.  O parâmetro *rowsPerRead* controla quantas linhas de dados são lidas em cada lote.
  
    ```R
    sqlRowsPerRead = 5000
    ```
  
    Embora esse parâmetro seja opcional, ele é importante para lidar com o uso de memória e cálculos eficientes.  A maioria das funções analíticas avançadas do [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] processa dados em partes e acumula resultados intermediários, retornando os cálculos finais depois que todos os dados foram lidos.
  
    Caso o valor desse parâmetro seja muito grande, o acesso aos dados pode ser lento, pois você não tem memória suficiente para processar com eficiência um bloco de dados grande.  Em alguns sistemas, se o valor de *rowsPerRead* for muito pequeno, o desempenho poderá ser mais lento.
  
    Para este passo a passo, você usará o tamanho do processo em lote definido pela instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para controlar o número de linhas em cada parte e salvará esse valor na variável *sqlRowsPerRead*.  Recomendamos testar essa configuração em seu sistema quando você estiver trabalhando com um conjunto de dados grande.
  
4.  Finalmente, defina uma variável para o novo objeto de fonte de dados e passar os argumentos definidos anteriormente para o construtor RxSqlServerData. Observe que isso só cria o objeto da fonte de dados, mas não o preenche.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

#### <a name="to-create-the-scoring-data-table"></a>Para criar a tabela de dados de pontuação

Você criará a tabela que contém os dados de pontuação usando o mesmo processo.

1. Crie uma nova variável do R, *sqlScoreTable*, para armazenar o nome da tabela usada para pontuação.
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. Fornecer essa variável como um argumento para a função RxSqlServerData para definir um segundo objeto de fonte de dados, *sqlScoreDS*.
  
    ```R
    sqlScoreDS \<- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

Como você já definiu a cadeia de conexão e outros parâmetros como variáveis no espaço de trabalho do R, é fácil criar novas fontes de dados para diferentes tabelas, exibições ou consultas: basta especificar um nome de tabela diferente.

Mais adiante neste tutorial, você aprenderá a criar um objeto da fonte de dados com base em uma consulta SQL.

## <a name="load-data-into-sql-tables-using-r"></a>Carregar dados em tabelas SQL usando o R

Agora que você criou as tabelas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , é possível carregar dados nelas usando a função **Rx** apropriada.

O **RevoScaleR** pacote contém funções que oferecem suporte a várias fontes de dados: dados de texto, você usará RxTextData para gerar o objeto de fonte de dados. Há outras funções para criar objetos da fonte de dados com base em dados do Hadoop, dados ODBC e assim por diante.

> [!NOTE]
> Para esta seção, você deve ter permissões Executar DDL no banco de dados.

### <a name="load-data-into-the-training-table"></a>Carregar dados na tabela de treinamento

1. Crie uma variável de R, *ccFraudCsv*e atribuir à variável de caminho do arquivo para o arquivo CSV que contém os dados de exemplo.
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    Observe a função de utilitário, **rxGetOption**. Essa função é fornecida no pacote **RevoScaleR** para ajudá-lo a definir e gerenciar opções relacionadas aos contextos de computação local e remota, como o diretório compartilhado padrão, o número de processadores (núcleos) a serem usados em cálculos, etc.  Esta chamada é útil porque ele obtém os exemplos da biblioteca correta, independentemente de onde você está executando seu código. Por exemplo, experimente executar a função no SQL Server e no seu computador de desenvolvimento e veja como os caminhos diferem.
  
2. Definir uma variável para armazenar os novos dados e use a função RxTextData para especificar a fonte de dados de texto.
  
    ```R
    inTextData <- RxTextData(file = ccFraudCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer",
        "fraudRisk" = "integer"))
    ```
  
    O argumento *colClasses* é importante. Você pode usá-lo para indicar o tipo de dados que será atribuído a cada coluna de dados carregados do arquivo de texto. Neste exemplo, todas as colunas são tratadas como texto, exceto pelas colunas nomeadas, que são tratadas como inteiros.
  
3. Neste ponto, talvez você queira pausar um instante e exibir o banco de dados em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  Atualize a lista de tabelas no banco de dados.
  
    Você verá que, embora os objetos de dados do R tenham sido criados no espaço de trabalho local, as tabelas ainda não foram criadas no banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Além disso, nenhum dado foi carregado do arquivo de texto para a variável de R.
  
4. Agora, chame a função **rxDataStep** para inserir os dados na tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
  
    Após uma pequena pausa, supondo que não haja nenhum problema com a cadeia de conexão, você deve ver resultados como estes:
  
      *Total de linhas gravadas: 10000, Tempo total: 0,466*

      *Linhas lidas: 10000, Total de linhas processadas: 10000, Tempo total da parte: 0,577 segundo*
  
5. Usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], atualize a lista de tabelas. Para verificar se cada variável tem os tipos de dados correto e se foi importado com êxito, você pode também clique a tabela em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e selecione **selecionar 1000 linhas superiores**.

### <a name="load-data-into-the-scoring-table"></a>Carregar dados na tabela de pontuação

1. Você seguirá as mesmas etapas para carregar o conjunto de dados usado para pontuação no banco de dados.
  
    Comece fornecendo o caminho para o arquivo de origem.
  
    ```R
    ccScoreCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudScoreSmall.csv")
    ```
  
2. Use a função RxTextData para obter os dados e salve-o na variável, *inTextData*.
  
    ```R
    inTextData <- RxTextData(file = ccScoreCsv,      colClasses = c(
        "custID" = "integer", "gender" = "integer", "state" = "integer",
        "cardholder" = "integer", "balance" = "integer",
        "numTrans" = "integer",
        "numIntlTrans" = "integer", "creditLine" = "integer"))
    ```
  
3.  Chame a função rxDataStep para substituir a tabela atual com o novo esquema e dados.
  
    ```R
    rxDataStep(inData = inTextData, sqlScoreDS, overwrite = TRUE)
    ```
  
    - O argumento *inData* define a fonte de dados que será usada.
  
    - O argumento *outFile* especifica a tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em que você quer salvar os dados.
  
    - Se a tabela já existir e você não usar a opção *substituir* , os resultados serão inseridos sem truncamento.
  
Novamente, se a conexão foi bem-sucedida, você verá uma mensagem indicando a conclusão e o tempo necessário para gravar os dados na tabela:

*Total de linhas gravadas: 10000, Tempo total: 0,384*

*Linhas lidas: 10000, Total de linhas processadas: 10000, Tempo total da parte: 0,456 segundo*

## <a name="more-about-rxdatastep"></a>Mais sobre rxDataStep

O **rxDataStep** é uma função avançada que pode executar várias transformações em um quadro de dados de R, para converter os dados para a representação exigida pelo destino. Nesse caso, o destino é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Você também pode especificar transformações nos dados, usando funções R nos argumentos para rxDataStep. Você verá exemplos dessas operações mais tarde.

## <a name="next-step"></a>Próxima etapa

[Consultar e modificar os dados do SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)

## <a name="previous-step"></a>Etapa anterior

[Trabalhar com dados do SQL Server usando o R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)

