---
title: Como criar um procedimento armazenado usando sqlrutils
description: Use o pacote R sqlrutils em SQL Server para agrupar o código de linguagem R em uma única função que pode ser passada como um argumento para um procedimento armazenado.
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 0713a126a237f20b2de4e3b16225bb9e5ae26307
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345574"
---
# <a name="create-a-stored-pprocedure-using-sqlrutils"></a>Criar um pProcedure armazenado usando sqlrutils
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artigo descreve as etapas para converter seu código R para executar como um procedimento armazenado T-SQL. Para obter os melhores resultados possíveis, seu código poderá precisar ser um pouco modificado, para garantir que todas as entradas possam ser parametrizadas.

## <a name="bkmk_rewrite"></a>Etapa 1. Reescrever script R

Para obter os melhores resultados, você deve reescrever o código R para encapsulá-lo como uma única função.

Todas as variáveis usadas pela função devem ser definidas dentro da função ou devem ser definidas como parâmetros de entrada. Consulte o [código de exemplo](#samples) neste artigo.

Além disso, como os parâmetros de entrada para a função R se tornarão os parâmetros de entrada do procedimento armazenado do SQL, você deve garantir que suas entradas e saídas estejam em conformidade com os seguintes requisitos de tipo:

### <a name="inputs"></a>Entradas

Entre os parâmetros de entrada pode haver no máximo um quadro de dados.

Os objetos dentro do quadro de dados, bem como todos os outros parâmetros de entrada da função, devem ser dos seguintes tipos de dados R:
- POSIXct
- numeric
- character
- integer
- logical
- raw

Se um tipo de entrada não é de um dos tipos acima, ele precisa ser serializado e transmitido para a função como *raw*. Nesse caso, a função também deve incluir o código para desserializar a entrada.

### <a name="outputs"></a>Saídas

A função pode produzir uma das seguintes opções:

- Um quadro de dados que contém os tipos de dados com suporte. Todos os objetos no quadro de dados devem usar um dos tipos de dados com suporte.
- Uma lista nomeada, contendo no máximo um quadro de dados. Todos os membros da lista devem usar um dos tipos de dados com suporte.
- Um valor NULO, se sua função não retornar nenhum resultado

## <a name="step-2-generate-required-objects"></a>Etapa 2. Gerar objetos necessários

Depois que o código R tiver sido limpo e puder ser chamado como uma única função, você usará as funções no pacote **sqlrutils** para preparar as entradas e saídas em um formulário que pode ser passado para o construtor que, na verdade, cria o procedimento armazenado.

o **sqlrutils** fornece funções que definem o tipo e o esquema de dados de entrada e definem o tipo e o esquema de dados de saída. Ele também inclui funções que podem converter objetos R para o tipo de saída necessário. Você pode fazer várias chamadas de função para criar os objetos necessários, dependendo dos tipos de dados usados pelo seu código.

### <a name="inputs"></a>Entradas

Se sua função usa entradas, para cada entrada, chame as seguintes funções:

- `setInputData`se a entrada for um quadro de dados
- `setInputParameter`para todos os outros tipos de entrada

Quando você faz cada chamada de função, é criado um objeto R que será passado posteriormente como um argumento para `StoredProcedure`, para criar o procedimento armazenado completo.

### <a name="outputs"></a>Saídas

o **sqlrutils** fornece várias funções para converter objetos R, como listas, para o Data. frame exigido pelo SQL Server.
Se sua função gera diretamente um quadro de dados, sem primeiro encapsulá-lo em uma lista, você pode ignorar esta etapa.
Você também pode ignorar a conversão desta etapa se sua função retornar NULL.

Ao converter uma lista ou obter um item específico de uma lista, escolha uma destas funções:

- `setOutputData`se a variável a ser obtida da lista for um quadro de dados
- `setOutputParameter`para todos os outros membros da lista

Quando você faz cada chamada de função, é criado um objeto R que será passado posteriormente como um argumento para `StoredProcedure`, para criar o procedimento armazenado completo.

## <a name="step-3-generate-the-stored-procedure"></a>Etapa 3. Gerar o procedimento armazenado

Quando todos os parâmetros de entrada e saída estiverem prontos, faça uma chamada `StoredProcedure` para o construtor.

**Usage**

`StoredProcedure (func, spName, ..., filePath = NULL ,dbName = NULL, connectionString = NULL, batchSeparator = "GO")`

Para ilustrar, suponha que você deseja criar um procedimento armazenado chamado **sp_rsample** com estes parâmetros:

- Usa uma função **foosql**existente. A função era baseada em código existente na função de R **foo**, mas você reescreveu a função para estar de acordo com os requisitos, conforme descrito nesta [seção](#bkmk_rewrite), e denominada a função updated como **foosql**.
- Usa o quadro de dados **queryinput** como entrada
- Gera como saída um quadro de dados com o nome da variável  R, sqloutput
- Você deseja criar o código T-SQL como um arquivo na `C:\Temp` pasta, para que você possa executá-lo usando SQL Server Management Studio mais tarde

```R
StoredProcedure (foosql, sp_rsample, queryinput, sqloutput, filePath = "C:\\Temp")
```

> [!NOTE]
> Como você está gravando o arquivo no sistema de arquivos, você pode omitir os argumentos que definem a conexão de banco de dados.

A saída da função é um procedimento armazenado T-SQL que pode ser executado em uma instância do SQL Server 2016 (requer R Services) ou SQL Server 2017 (requer Serviços de Machine Learning com R). 

Para obter exemplos adicionais, consulte a ajuda do pacote, `help(StoredProcedure)` chamando de um ambiente de R.

## <a name="step-4-register-and-run-the-stored-procedure"></a>Etapa 4. Registrar e executar o procedimento armazenado

Há duas maneiras de executar o procedimento armazenado:

- Usando o T-SQL, de qualquer cliente que dá suporte a conexões com a instância do SQL Server 2016 ou SQL Server 2017
- De um ambiente de R

Os dois métodos exigem que o procedimento armazenado seja registrado no banco de dados em que você pretende usar o procedimento armazenado.

### <a name="register-the-stored-procedure"></a>Registrar o procedimento armazenado

Você pode registrar o procedimento armazenado usando o R, ou pode executar a instrução CREATE PROCEDURE no T-SQL.

- Usando o T-SQL.  Se você for mais confortável com o T-SQL, abra o SQL Server Management Studio (ou qualquer outro cliente que possa executar comandos DDL do `StoredProcedure` SQL) e execute a instrução CREATE PROCEDURE usando o código preparado pela função.
- Usando o R. Enquanto você ainda estiver em seu ambiente de R, poderá usar a `registerStoredProcedure` função no **sqlrutils** para registrar o procedimento armazenado no banco de dados.

  Por exemplo, você pode registrar o procedimento armazenado **sp_rsample** na instância e no banco de dados definido em *sqlConnStr*, fazendo essa chamada R:

  ```R
  registerStoredProcedure(sp_rsample, sqlConnStr)
  ```


> [!IMPORTANT]
> Independentemente de você usar R ou SQL, você deve executar a instrução usando uma conta que tenha permissões para criar novos objetos de banco de dados.

### <a name="run-using-sql"></a>Executar usando SQL

Depois que o procedimento armazenado tiver sido criado, abra uma conexão com o banco de dados SQL usando qualquer cliente que ofereça suporte a T-SQL e passe valores para quaisquer parâmetros exigidos pelo procedimento armazenado.

### <a name="run-using-r"></a>Executar usando o R

Será necessária alguma preparação adicional se você quiser executar o procedimento armazenado do código R, em vez de SQL Server. Por exemplo, se o procedimento armazenado exigir valores de entrada, você deverá definir esses parâmetros de entrada antes que a função possa ser executada e, em seguida, passar esses objetos para o procedimento armazenado em seu código R.

O processo geral de chamar o procedimento armazenado SQL preparado é o seguinte:

1. Chamar `getInputParameters` para obter uma lista de objetos de parâmetro de entrada.
2. Definir um `$query` ou definir um `$value` para cada parâmetro de entrada.
3. Use `executeStoredProcedure` para executar o procedimento armazenado no ambiente de desenvolvimento R, transmitindo a lista de objetos de parâmetro de entrada que você definiu.

## <a name = "samples"></a>Exemplo

Este exemplo mostra as versões anteriores e posteriores de um script R que obtém dados de um banco de SQL Server, realiza algumas transformações nos dados e salva-os em um banco de dado diferente.

Esse exemplo simples é usado apenas para demonstrar como você pode reorganizar seu código R para facilitar a conversão em um procedimento armazenado.

### <a name="before-code-preparation"></a>Antes da preparação do código


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
> Ao usar uma conexão ODBC em vez de invocar a função *RxSqlServerData* , você deve abrir a conexão usando *rxOpen* antes de executar operações no banco de dados.


### <a name="after-code-preparation"></a>Após a preparação do código

Na versão atualizada, a primeira linha define o nome da função. Todos os outros códigos da solução R original se tornam parte dessa função.

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


