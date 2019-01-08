---
title: Como criar um procedimento armazenado usando sqlrutils - serviços do SQL Server Machine Learning
description: Use o pacote sqlrutils R no SQL Server para agrupar o código de idioma R em uma única função que pode ser passada como um argumento para um procedimento armazenado.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e347deb0a0f05da12a4281e77223a0492f04f13f
ms.sourcegitcommit: 85bfaa5bac737253a6740f1f402be87788d691ef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2018
ms.locfileid: "53432709"
---
# <a name="create-a-stored-pprocedure-using-sqlrutils"></a>Criar um pProcedure armazenado usando sqlrutils
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve as etapas para converter seu código R para ser executado como um procedimento armazenado T-SQL. Para obter os melhores resultados possíveis, seu código poderá precisar ser um pouco modificado, para garantir que todas as entradas possam ser parametrizadas.

## <a name="bkmk_rewrite"></a>Etapa 1. Reescreva o Script R

Para obter melhores resultados, você deve reescrever seu código R para encapsulá-la como uma única função.

Todas as variáveis usadas pela função devem ser definidas dentro da função, ou devem ser definidas como parâmetros de entrada. Consulte a [código de exemplo](#samples) neste artigo.

Além disso, como os parâmetros de entrada para a função R se tornará os parâmetros de entrada do SQL do procedimento de armazenado, você deve garantir que suas entradas e saídas em conformidade com os seguintes requisitos de tipo:

### <a name="inputs"></a>Entradas

Entre os parâmetros de entrada pode haver no máximo um quadro de dados.

Os objetos dentro do quadro de dados, bem como todos os outros parâmetros de entrada da função, devem ser dos seguintes tipos de dados R:
- POSIXct
- NUMERIC
- character
- inteiro
- logical
- raw

Se um tipo de entrada não é de um dos tipos acima, ele precisa ser serializado e transmitido para a função como *raw*. Nesse caso, a função também deve incluir o código para desserializar a entrada.

### <a name="outputs"></a>Saídas

A função pode produzir uma das seguintes opções:

- Um quadro de dados que contém os tipos de dados com suporte. Todos os objetos no quadro de dados devem usar um dos tipos de dados com suporte.
- Uma lista nomeada, contendo no máximo um quadro de dados. Todos os membros da lista devem usar um dos tipos de dados com suporte.
- Um valor NULO, se sua função não retornar nenhum resultado

## <a name="step-2-generate-required-objects"></a>Etapa 2. Gerar objetos necessários

Depois que seu código R foi limpo e pode ser chamado como uma única função, você usará as funções na **sqlrutils** pacote para preparar as entradas e saídas em um formulário que pode ser passado para o construtor que cria, na verdade, o procedimento armazenado.

**sqlrutils** fornece funções que definem o esquema de dados de entrada e o tipo e definem o esquema de dados de saída e o tipo. Ele também inclui funções que podem converter objetos de R para o tipo de saída necessária. Você pode fazer várias chamadas de função para criar os objetos necessários, dependendo do seu código usa os tipos de dados.

### <a name="inputs"></a>Entradas

Se sua função receber entradas, para cada entrada, chame as funções a seguir:

- `setInputData` Se a entrada for um quadro de dados
- `setInputParameter` para todos os outros tipos de entrada

Quando você faz com que cada função de chamada, um objeto de R é criado que você passará mais tarde como um argumento para `StoredProcedure`, para criar o procedimento armazenado concluído.

### <a name="outputs"></a>Saídas

**sqlrutils** fornece várias funções para converter R objetos, como listas para o Frame requerida pelo SQL Server.
Se sua função gera diretamente um quadro de dados, sem primeiro encapsulá-lo em uma lista, você pode ignorar esta etapa.
Você também pode ignorar a conversão esta etapa se a função retornará NULL.

Quando a conversão de uma lista ou obtendo um item específico de uma lista, escolha essas funções:

- `setOutputData` Se a variável para obter a lista é um quadro de dados
- `setOutputParameter` para todos os outros membros da lista

Quando você faz com que cada função de chamada, um objeto de R é criado que você passará mais tarde como um argumento para `StoredProcedure`, para criar o procedimento armazenado concluído.

## <a name="step-3-generate-the-stored-procedure"></a>Etapa 3. Gerar o procedimento armazenado

Quando todos os parâmetros de entrada e saídos estiverem prontos, fazer uma chamada para o `StoredProcedure` construtor.

**Usage**

`StoredProcedure (func, spName, ..., filePath = NULL ,dbName = NULL, connectionString = NULL, batchSeparator = "GO")`

Para ilustrar, suponha que você deseja criar um procedimento armazenado denominado **sp_rsample** com estes parâmetros:

- Usa uma função existente **foosql**. A função foi baseada em função do R de código existente **foo**, mas você reescreveu a função para estar em conformidade com os requisitos conforme descrito em [nesta seção](#bkmk_rewrite)e a chamada a função atualizada como  **foosql**.
- Usa o quadro de dados **queryinput** como entrada
- Gera como saída de um quadro de dados com o nome da variável R **sqloutput**
- Você deseja criar o código T-SQL como um arquivo no `C:\Temp` pasta, para que você pode executá-lo mais tarde usando o SQL Server Management Studio

```R
StoredProcedure (foosql, sp_rsample, queryinput, sqloutput, filePath = "C:\\Temp")
```

> [!NOTE]
> Porque você está escrevendo o arquivo ao sistema de arquivos, você pode omitir os argumentos que definem a conexão de banco de dados.

A saída da função é um procedimento armazenado T-SQL que pode ser executado em uma instância do SQL Server 2016 (requer o R Services) ou SQL Server 2017 (requer serviços de Machine Learning com R). 

Para obter exemplos adicionais, consulte a Ajuda do pacote, chamando `help(StoredProcedure)` em um ambiente de R.

## <a name="step-4-register-and-run-the-stored-procedure"></a>Etapa 4. Registrar e executar o procedimento armazenado

Há duas maneiras que você pode executar o procedimento armazenado:

- Usando o T-SQL, de qualquer cliente que dá suporte a conexões com a instância do SQL Server 2016 ou SQL Server 2017
- Em um ambiente de R

Ambos os métodos requerem que o procedimento armazenado ser registrado no banco de dados no qual você pretende usar o procedimento armazenado.

### <a name="register-the-stored-procedure"></a>Registrar o procedimento armazenado

Você pode registrar o procedimento armazenado usando o R, ou você pode executar a instrução CREATE PROCEDURE no T-SQL.

- Usando o T-SQL.  Se você estiver mais confortável com o T-SQL, abra o SQl Server Management Studio (ou qualquer outro cliente que pode executar comandos de DDL de SQL) e execute a instrução CREATE PROCEDURE usando o código preparado pelo `StoredProcedure` função.
- Usando o R. Enquanto você ainda estiver em seu ambiente de R, você pode usar o `registerStoredProcedure` funcionar **sqlrutils** para registrar o procedimento armazenado com o banco de dados.

  Por exemplo, você poderia registrar o procedimento armazenado **sp_rsample** na instância e banco de dados definidos no *sqlConnStr*, ao fazer essa chamada de R:

  ```R
  registerStoredProcedure(sp_rsample, sqlConnStr)
  ```


> [!IMPORTANT]
> Independentemente de você usar R ou do SQL, você deve executar a instrução usando uma conta que tenha permissões para criar novos objetos de banco de dados.

### <a name="run-using-sql"></a>Executar usando o SQL

Depois que o procedimento armazenado foi criado, abra uma conexão ao banco de dados SQL usando qualquer cliente compatível com o T-SQL e passar valores para os parâmetros necessários para o procedimento armazenado.

### <a name="run-using-r"></a>Executar usando o R

Alguma preparação adicional é necessária se você quiser executar o procedimento armazenado a partir do código R, em vez do SQL Server. Por exemplo, se o procedimento armazenado requer valores de entrada, você deve definir esses parâmetros de entrada antes da função pode ser executado e, em seguida, passar esses objetos para o procedimento armazenado em seu código R.

O processo geral de chamar o procedimento armazenado SQL preparado é da seguinte maneira:

1. Chamar `getInputParameters` para obter uma lista de objetos de parâmetro de entrada.
2. Definir um `$query` ou definir um `$value` para cada parâmetro de entrada.
3. Use `executeStoredProcedure` para executar o procedimento armazenado no ambiente de desenvolvimento R, transmitindo a lista de objetos de parâmetro de entrada que você definiu.

## <a name = "samples"></a>Exemplo

Este exemplo mostra o antes e depois de versões de um script de R que obtém dados de um banco de dados do SQL Server, executa algumas transformações nos dados e salva-o em outro banco de dados.

Esse exemplo simples é usado somente para demonstrar como você pode reorganizar seu código R para tornar mais fácil converter em um procedimento armazenado.

### <a name="before-code-preparation"></a>Antes de preparação de código


```R
sqlConnFrom <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=AirlineSrc;Trusted_Connection=Yes;"
  
sqlConnTo <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=AirlineTest;Trusted_Connection=Yes;"
  
sqlQueryAirline <- "SELECT TOP 10000 ArrDelay, CRSDepTime, DayOfWeek FROM [AirlineDemoSmall]"
  
dsSqlFrom <- RxSqlServerData(sqlQuery = sqlQueryAirline, connectionString = sqlConnFrom)
  
dsSqlTo <- RxSqlServerData(table = "cleanData", connectionString = sqlConnTo)
  
xFunc <- function(data) {
    data$CRSDepHour <- as.integer(trunc(data$CRSDepTime))
    return(data)
    }
  
xVars <- c("CRSDepTime")
  
sqlCompute <- RxInSqlServer(numTasks = 4, connectionString = sqlConnTo)
  
rxOpen(dsSqlFrom)
rxOpen(dsSqlTo)
  
if (rxSqlServerTableExists("cleanData", connectionString = sqlConnTo))   {
    rxSqlServerDropTable("cleanData")}
  
rxDataStep(inData = dsSqlFrom, 
     outFile = dsSqlTo,
     transformFunc = xFunc,
     transformVars = xVars,
     overwrite = TRUE)
```

> [!NOTE]
> 
> Quando você usa uma conexão ODBC em vez de invocar o *RxSqlServerData* função, você deve abrir a conexão usando *rxOpen* antes de executar operações no banco de dados.


### <a name="after-code-preparation"></a>Após a preparação de código

Na versão atualizada, a primeira linha define o nome da função. Todos os outros códigos de solução de R original se torna parte dessa função.

```R
myetl1function <- function() { 
   sqlConnFrom <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer01;Database=Airline01;Trusted_Connection=Yes;"
   sqlConnTo <- "Driver={ODBC Driver 13 for SQL Server};Server=MyServer02;Database=Airline02;Trusted_Connection=Yes;"
    
   sqlQueryAirline <- "SELECT TOP 10000 ArrDelay, CRSDepTime, DayOfWeek FROM [AirlineDemoSmall]"

   dsSqlFrom <- RxSqlServerData(sqlQuery = sqlQueryAirline, connectionString = sqlConnFrom)
  
   dsSqlTo <- RxSqlServerData(table = "cleanData", connectionString = sqlConnTo)
  
   xFunc <- function(data) {
     data$CRSDepHour <- as.integer(trunc(data$CRSDepTime))
     return(data)}
  
   xVars <- c("CRSDepTime")
  
   sqlCompute <- RxInSqlServer(numTasks = 4, connectionString = sqlConnTo)
  
   if (rxSqlServerTableExists("cleanData", connectionString = sqlConnTo)) {rxSqlServerDropTable("cleanData")}
  
   rxDataStep(inData = dsSqlFrom, 
        outFile = dsSqlTo,
        transformFunc = xFunc,
        transformVars = xVars,
        overwrite = TRUE)
   return(NULL)
}
```

> [!NOTE]
> 
> Embora você não precise explicitamente abrir a conexão ODBC como parte do seu código, uma conexão ODBC ainda é necessária para usar o **sqlrutils**.

## <a name="see-also"></a>Consulte também

[sqlrutils (SQL)](ref-r-sqlrutils.md)


