---
title: Salvar e carregar objetos de R do SQL Server usando o ODBC - serviços do SQL Server Machine Learning
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 6556602e080587b9be1ff8c02fafb378b4497606
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962463"
---
# <a name="save-and-load-r-objects-from-sql-server-using-odbc"></a>Salvar e carregar objetos de R do SQL Server usando o ODBC
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Os serviços de R do SQL Server podem armazenar objetos de R serializados em uma tabela e, em seguida, carregar o objeto da tabela conforme necessário, sem a necessidade de executar novamente o código de R ou readaptar o modelo. Essa capacidade de salvar objetos de R em um banco de dados é essencial para cenários como treinar e salvar um modelo para depois usá-lo para análise ou pontuação.

Para melhorar o desempenho desta etapa crítica, o pacote **RevoScaleR** agora inclui novas funções de serialização e desserialização, que melhoram significativamente o desempenho e armazenam o objeto de forma mais compacta. Este artigo descreve essas funções e como usá-los.

## <a name="overview"></a>Visão geral

O pacote **RevoScaleR** agora inclui novas funções que facilitam a salvar objetos de R no SQL Server e, em seguida, ler os objetos da tabela do SQL Server. Em geral, cada chamada de função usa um armazenamento de valor de chave simples, no qual a chave é o nome do objeto, e o valor associado com a chave é o objeto varbinary de R para ser movido para dentro ou fora de uma tabela.

Para salvar objetos de R do SQL Server diretamente em um ambiente de R, faça o seguinte:

+ estabelecer uma conexão ao SQL Server usando o *RxOdbcData* fonte de dados.
+ Chamar as novas funções ao longo de conexão ODBC
+ Opcionalmente, você pode especificar que o objeto não ser serializado. Em seguida, escolha um novo algoritmo de compactação para usar em vez do algoritmo de compactação padrão.

Por padrão, qualquer objeto que é chamado do R para ser movido para o SQL Server é serializado e compactado. Por outro lado, quando você carrega um objeto de uma tabela do SQL Server para usar em seu código de R, o objeto é desserializado e descompactado.

## <a name="list-of-new-functions"></a>Lista de novas funções

- A`rxWriteObject` grava um objeto de R no SQL Server usando a fonte de dados ODBC.

- A`rxReadObject` lê um objeto de R de um banco de dados do SQL Server, usando uma fonte de dados ODBC

- A`rxDeleteObject` exclui um objeto R do banco de dados do SQL Server especificado na fonte de dados ODBC. Se houver vários objetos identificados pela combinação de chave/versão, todos são excluídos.

- A`rxListKeys` lista todos os objetos disponíveis como pares chave-valor. Isso ajuda a determinar os nomes e as versões dos objetos de R.

Para obter ajuda detalhada sobre a sintaxe de cada função, use a Ajuda de R. Detalhes também estão disponíveis na [referência do ScaleR](https://docs.microsoft.com/r-server/r-reference/revoscaler/revoscaler).

## <a name="how-to-store-r-objects-in-sql-server-using-odbc"></a>Como armazenar objetos de R no SQL Server usando o ODBC

Este procedimento demonstra como você pode usar as novas funções para criar um modelo e salvá-lo no SQL Server.

1. Configure a cadeia de conexão para o SQL Server.
   ```R
   conStr <- 'Driver={SQL Server};Server=localhost;Database=storedb;Trusted_Connection=true'
   ```
2. Crie um objeto de fonte de dados *rxOdbcData* em R usando a cadeia de conexão.
   ```R
   ds <- RxOdbcData(table="robjects", connectionString=conStr)
   ```

3. Exclua a tabela, se ela já existir e você não desejar controlar as versões antigas dos objetos.

   ```R
   if(rxSqlServerTableExists(ds@table, ds@connectionString)) {
       rxSqlServerDropTable(ds@table, ds@connectionString)
       }
   ```
   
4. Defina uma tabela que pode ser usada para armazenar objetos binários.

   ```R
   ddl <- paste(" CREATE TABLE [", ds@table, "] 
      (","  [id] varchar(200) NOT NULL,
       "," [value] varbinary(max),
       "," CONSTRAINT unique_id UNIQUE (id))", 
       sep = "") 
   ```
5. Abra a conexão ODBC para criar a tabela e, quando a instrução DDL for concluída, feche a conexão.

   ```R
    rxOpen(ds, "w") 
    rxExecuteSQLDDL(ds, ddl) 
    rxClose(ds)
    ```
6. Gere os objetos de R que você deseja armazenar.

   ```R
   infertLogit <- rxLogit(case ~ age + parity + education + spontaneous + induced, 
     data = infert)
   ```
6. Use o objeto *RxOdbcData* criado anteriormente, para salvar o modelo no banco de dados.

   ```R
   rxWriteObject(ds, "logit.model", infertLogit)
   ```

## <a name="how-to-read-r-objects-from-sql-server-using-odbc"></a>Como ler objetos de R do SQL Server usando o ODBC

Este procedimento demonstra como você pode usar as novas funções para carregar um modelo do SQL Server.

1. Configure a cadeia de conexão para o SQL Server.

   ```R
   conStr2 <- 'Driver={SQL Server};Server=localhost;Database=storedb;Trusted_Connection=true'
   ```
2. Crie um objeto de fonte de dados *rxOdbcData* em R usando a cadeia de conexão.

   ```R
   ds <- RxOdbcData(table="robjects", connectionString=conStr2)
   ```
3. Leia o modelo da tabela especificando seu nome de objeto R.

   ```R
    infertLogit2 <- rxReadObject(ds, "logit.model")
   ```
