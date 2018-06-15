---
title: Criar objetos de dados do SQL Server usando RxSqlServerData (SQL e R mergulho profundo) | Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e15c3e7c13c1be4f524c25bb1cec6da3c8e20c7e
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
ms.locfileid: "31203458"
---
# <a name="create-sql-server-data-objects-using-rxsqlserverdata-sql-and-r-deep-dive"></a>Criar objetos de dados do SQL Server usando RxSqlServerData (SQL e R mergulho profundo)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo faz parte do tutorial mergulho profundo de ciência de dados, como usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) com o SQL Server.

Agora que você criou o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de banco de dados e ter as permissões necessárias para trabalhar com os dados. Nesta etapa, você deve criar alguns objetos em R que permitem que você trabalhe com os dados.

## <a name="create-the-sql-server-data-objects"></a>Criar os objetos de dados do SQL Server

Nesta etapa, você pode usar funções pelo **RevoScaleR** pacote para criar e popular duas tabelas. Uma tabela é usada para treinar os modelos e a outra é usada para pontuá-los. Ambas as tabelas contêm dados de fraude de cartão de crédito simulados.

Para criar tabelas no controle remoto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] computador, chame o **RxSqlServerData** função.

> [!TIP]
> Se você estiver usando as ferramentas de R para o Visual Studio, selecione **Ferramentas de R** na barra de ferramentas e clique em **Windows** para ver as opções de depuração e exibir as variáveis do R.

### <a name="create-the-training-data-table"></a>Criar a tabela de dados de treinamento

1. Salve a cadeia de caracteres de conexão do banco de dados em uma variável de R. Aqui estão dois exemplos de cadeias de conexão ODBC válidas para o SQL Server: usando um logon SQL e uma para a autenticação integrada do Windows.

    **Logon do SQL**
    ```R
    sqlConnString <- "Driver=SQL Server;Server=instance_name; Database=DeepDive;Uid=user_name;Pwd=password"
    ```

    **Autenticação do Windows**
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
  
    Embora esse parâmetro seja opcional, ele é importante para lidar com o uso de memória e cálculos eficientes.  A maioria das funções analíticas aprimoradas na [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] processar dados em partes e armazenar resultados intermediários, retornando as computações finais depois que todos os dados foram lidos.
  
    Caso o valor desse parâmetro seja muito grande, o acesso aos dados pode ser lento, pois você não tem memória suficiente para processar com eficiência um bloco de dados grande.  Em alguns sistemas, se o valor de *rowsPerRead* for muito pequeno, o desempenho poderá ser mais lento. Portanto, é recomendável fazer experiências com essa configuração em seu sistema quando você estiver trabalhando com um grande conjunto de dados.
  
    Para este passo a passo, use o tamanho do processo de lote padrão definido pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instância para controlar o número de linhas em cada bloco. Salvar esse valor na variável `sqlRowsPerRead`.
  
4.  Finalmente, defina uma variável para o novo objeto de fonte de dados e passar os argumentos definidos anteriormente para o construtor RxSqlServerData. Observe que isso só cria o objeto da fonte de dados, mas não o preenche.
  
    ```R
    sqlFraudDS <- RxSqlServerData(connectionString = sqlConnString,
       table = sqlFraudTable,
       rowsPerRead = sqlRowsPerRead)
    ```

#### <a name="to-create-the-scoring-data-table"></a>Para criar a tabela de dados de pontuação

Usando as mesmas etapas, crie a tabela que contém os dados de pontuação usando o mesmo processo.

1. Crie uma nova variável do R, *sqlScoreTable*, para armazenar o nome da tabela usada para pontuação.
  
    ```R
    sqlScoreTable <- "ccFraudScoreSmall"
    ```
  
2. Fornecer essa variável como um argumento para a função RxSqlServerData para definir um segundo objeto de fonte de dados, *sqlScoreDS*.
  
    ```R
    sqlScoreDS \<- RxSqlServerData(connectionString = sqlConnString,
       table = sqlScoreTable, rowsPerRead = sqlRowsPerRead)
    ```

Porque o que você já definiu a cadeia de caracteres de conexão e outros parâmetros como variáveis no espaço de trabalho de R, é fácil criar novas fontes de dados de diferentes tabelas, exibições ou consultas.

> [!NOTE]
> A função usa argumentos diferentes para definir uma fonte de dados com base em uma tabela inteira que para uma fonte de dados com base em uma consulta. Isso ocorre porque o mecanismo de banco de dados do SQL Server deve preparar as consultas diferente. Posteriormente neste tutorial, você aprenderá como criar um objeto de fonte de dados com base em uma consulta SQL.

## <a name="load-data-into-sql-tables-using-r"></a>Carregar dados em tabelas do SQL usando o R

Agora que você criou as tabelas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , é possível carregar dados nelas usando a função **Rx** apropriada.

O **RevoScaleR** pacote contém funções que oferecem suporte a várias fontes de dados: dados de texto, use [RxTextData](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxtextdata) para gerar o objeto de fonte de dados. Há outras funções para criar objetos da fonte de dados com base em dados do Hadoop, dados ODBC e assim por diante.

> [!NOTE]
> Para essa seção, você deve ter **executar DDL** permissões no banco de dados.

### <a name="load-data-into-the-training-table"></a>Carregar dados na tabela de treinamento

1. Crie uma variável de R, *ccFraudCsv*e atribuir à variável de caminho do arquivo para o arquivo CSV que contém os dados de exemplo.
  
    ```R
    ccFraudCsv <- file.path(rxGetOption("sampleDataDir"), "ccFraudSmall.csv")
    ```
  
    Observe a chamada para **rxGetOption**, que é o método GET associado [rxOptions](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxoptions) na **RevoScaleR**. Use esse utilitário para definir e opções da lista relacionam contextos de computação local e remota, como o diretório compartilhado padrão ou o número de processadores (núcleos) a serem usados em cálculos.
    
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
  
3. Neste ponto, talvez você queira pausar um instante e exibir o banco de dados em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  Atualize a lista de tabelas no banco de dados.
  
    Você pode ver que, embora os objetos de dados R foram criados no seu espaço de trabalho local, as tabelas não foram criadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] banco de dados. Além disso, nenhum dado foi carregado do arquivo de texto para a variável de R.
  
4. Agora, chame a função [rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) para inserir os dados na tabela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
    ```R
    rxDataStep(inData = inTextData, outFile = sqlFraudDS, overwrite = TRUE)
    ```
  
    Após uma pequena pausa, supondo que não haja nenhum problema com a cadeia de conexão, você deve ver resultados como estes:
  
      *Total de linhas gravadas: 10000, Tempo total: 0,466*

      *Linhas lidas: 10000, Total de linhas processadas: 10000, Tempo total da parte: 0,577 segundo*
  
5. Usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], atualize a lista de tabelas. Para verificar se cada variável tem os tipos de dados correto e se foi importado com êxito, você pode também clique a tabela em [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e selecione **selecionar 1000 linhas superiores**.

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
  
    - Se a tabela já existir e você não usa o *substituir* opção resultados são inseridos sem truncamento.
  
Novamente, se a conexão foi bem-sucedida, você verá uma mensagem indicando a conclusão e o tempo necessário para gravar os dados na tabela:

*Total de linhas gravadas: 10000, Tempo total: 0,384*

*Linhas lidas: 10000, Total de linhas processadas: 10000, Tempo total da parte: 0,456 segundo*

## <a name="more-about-rxdatastep"></a>Mais sobre rxDataStep

[rxDataStep](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxdatastep) é uma função avançada que pode executar várias transformações em um quadro de dados R. Você também pode usar rxDataStep para converter dados para a representação exigida pelo destino: nesse caso, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

Opcionalmente, você pode especificar transformações nos dados, usando funções R nos argumentos para **rxDataStep**. Exemplos dessas operações são fornecidos posteriormente neste tutorial.

## <a name="next-step"></a>Próxima etapa

[Consultar e modificar os dados do SQL Server](../../advanced-analytics/tutorials/deepdive-query-and-modify-the-sql-server-data.md)

## <a name="previous-step"></a>Etapa anterior

[Trabalhar com dados do SQL Server usando o R](../../advanced-analytics/tutorials/deepdive-work-with-sql-server-data-using-r.md)
