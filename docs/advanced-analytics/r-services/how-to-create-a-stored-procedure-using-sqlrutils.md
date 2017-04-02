---
title: "Como criar um procedimento armazenado usando sqlrutils | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 5ba99b49-481e-4b30-967a-a429b855b1bd
caps.latest.revision: 10
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# Como criar um procedimento armazenado usando sqlrutils
Este tópico descreve as etapas para converter seu código R para ser executado como um procedimento armazenado T-SQL. Para obter os melhores resultados possíveis, seu código poderá precisar ser um pouco modificado, para garantir que todas as entradas possam ser parametrizadas.

## <a name="step-1-format-your-r-script"></a>Etapa 1. Formatar seu script R

1. Encapsule todo o código em uma única função.

   Isso significa que todas as variáveis usadas pela função devem ser definidas dentro da função ou definidas como parâmetros de entrada. Consulte o [código de exemplo](#samples) neste tópico.

## <a name="step-2-standardize-the-inputs-and-outputs"></a>Etapa 2. Padronizar as entradas e saídas

Os parâmetros de entrada da função vão se tornar os parâmetros de entrada do procedimento armazenado SQL e, portanto, devem estar em conformidade com os seguintes requisitos de tipo:
- Entre os parâmetros de entrada pode haver no máximo um quadro de dados.
- Os objetos dentro do quadro de dados, bem como todos os outros parâmetros de entrada da função, devem ser dos seguintes tipos de dados R:
    - POSIXct
    - numeric
    - character
    - inteiro
    - logical
    - raw

- Se um tipo de entrada não é de um dos tipos acima, ele precisa ser serializado e transmitido para a função como *raw*. Nesse caso, a função também deve incluir o código para desserializar a entrada.

A função pode produzir uma das seguintes opções:

- Um quadro de dados que contém os tipos de dados com suporte. Todos os objetos no quadro de dados devem usar um dos tipos de dados com suporte.
- Uma lista nomeada, contendo no máximo um quadro de dados. Todos os membros da lista devem usar um dos tipos de dados com suporte. 
- Um valor NULO, se sua função não retornar nenhum resultado

## <a name="step-3-make-calls-to-the-sqlrutils-package-to-generate-the-stored-procedure"></a>Etapa 3. Fazer chamadas ao pacote de sqlrutils para gerar o procedimento armazenado

Depois que o código R foi limpo e pode ser chamado como uma única função, você pode começar o processo de usar as funções no **sqlrutils** para converter seu código em um procedimento armazenado.

Dependendo dos tipos de dados dos parâmetros, você usará funções diferentes para capturar os dados e criar um objeto de parâmetro.

1. Se sua função utiliza parâmetros de entrada, para cada parâmetro, crie um dos seguintes objetos: 
    - Se o parâmetro de entrada for um quadro de dados, use `setInputData`.
    - Para todos os outros parâmetros de entrada, use `setInputParameter`.

2. Se sua função gera uma lista, crie um objeto para manipular os dados desejados da lista da seguinte maneira: 
    - Se a variável na lista é um quadro de dados, use `setOutputData`.
    - Para todos os outros membros da lista, use `setOutputParameter`.
    - Se sua função gera diretamente um quadro de dados, sem primeiro encapsulá-lo em uma lista, você pode ignorar esta etapa. 
    - Ignore esta etapa se a função retornar um valor NULO.

3. Quando todos os parâmetros de entrada e saída estiverem prontos, faça uma chamada para o construtor `StoredProcedure` para gerar o procedimento armazenado contendo a função R.
4. Para registrar imediatamente o procedimento armazenado com o banco de dados, use `registerStoredProcedure`.

## <a name="step-4-execute-the-stored-procedure"></a>Etapa 4. Executar o procedimento armazenado

1. Se você deseja executar o procedimento armazenado no código R, em vez de executar no SQL Server, e o procedimento armazenado requer uma entrada, você deve definir esses parâmetros de entrada antes que a função possa ser executada: 
    - Chamar `getInputParameters` para obter uma lista de objetos de parâmetro de entrada.
    - Definir um `$query` ou definir um `$value` para cada parâmetro de entrada. 

2. Use `executeStoredProcedure` para executar o procedimento armazenado no ambiente de desenvolvimento R, transmitindo a lista de objetos de parâmetro de entrada que você definiu.

## <a name="a-name-samplesaexamples-prepare-your-code"></a><a name = "samples"></a>Exemplos: prepare seu código 

Neste exemplo, o código R lê de um banco de dados, executa algumas transformações nos dados e salva-os em outro banco de dados. Esse exemplo simples é usado somente para demonstrar como você pode reorganizar seu código R para fornecer uma interface mais simples para conversão do procedimento armazenado.

**Antes da formatação**


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
Observe que quando você usa uma conexão ODBC em vez de chamar a função *RxSqlServerData*, você deve abrir a conexão usando *rxOpen* antes de executar operações no banco de dados.



**Após a formatação**

Na versão reformatada, a primeira linha define o nome da função.

Todos os outros códigos de sua solução de R original se tornam parte dessa função. 

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
Embora você não precise explicitamente abrir a conexão ODBC como parte do seu código, uma conexão ODBC ainda é necessária para usar o **sqlrutils**. 


## <a name="see-also"></a>Consulte também

[Gerando um procedimento armazenado usando sqlrutils](../../advanced-analytics/r-services/generating-an-r-stored-procedure-for-r-code-using-the-sqlrutils-package.md)

