---
description: Cálculos de aplicação no PolyBase
title: Cálculos de aplicação no PolyBase | Microsoft Docs
dexcription: Enable pushdown computation to improve performance of queries on your Hadoop cluster. You can select a subset of rows/columns in an external table for pushdown.
ms.date: 11/17/2020
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016'
ms.openlocfilehash: 844ab3f2a13e2bd5a9e3ea26d41012a51e7329a4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97416484"
---
# <a name="pushdown-computations-in-polybase"></a>Cálculos de aplicação no PolyBase

[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

A computação de aplicação aprimora o desempenho de consultas em fontes de dados externas. Do SQL Server 2016 em diante, os cálculos de aplicação estavam disponíveis para fontes de dados externas do Hadoop. O SQL Server 2019 introduz os cálculos de aplicação para outros tipos de fontes de dados externas.

## <a name="enable-pushdown-computation"></a> Habilitar cálculo de aplicação

Os seguintes artigos incluem informações sobre como configurar a computação de aplicação para tipos específicos de fontes de dados externas:

- [Habilitar cálculo de aplicação no Hadoop](polybase-configure-hadoop.md#pushdown)
- [Configurar o PolyBase para acessar dados externos no Oracle](polybase-configure-oracle.md)
- [Configurar o PolyBase para acessar dados externos no Teradata](polybase-configure-teradata.md)
- [Configurar o PolyBase para acessar dados externos no MongoDB](polybase-configure-mongodb.md)
- [Configurar o PolyBase para acessar dados externos com tipos genéricos ODBC](polybase-configure-odbc-generic.md)
- [Configurar o PolyBase para acessar dados externos no SQL Server](polybase-configure-sql-server.md)

## <a name="select-a-subset-of-rows"></a>Selecionar um subconjunto de linhas

Use aplicação de predicado para melhorar o desempenho de uma consulta que seleciona um subconjunto de linhas de uma tabela externa.

Neste exemplo, o SQL Server 2016 inicia um trabalho de map-reduce para recuperar as linhas que correspondem ao predicado `customer.account_balance < 200000` no Hadoop. Como a consulta pode ser concluída com êxito sem examinar todas as linhas na tabela, somente as linhas que atendem aos critérios de predicado são copiadas para o SQL Server. Isso economiza bastante tempo e exige menos espaço de armazenamento temporário quando o número de saldos do cliente < 200000 é pequeno em comparação com o número de clientes com saldos o cliente >= 200000.

```sql
SELECT * FROM customer WHERE customer.account_balance < 200000
SELECT * FROM SensorData WHERE Speed > 65;  
```

### <a name="select-a-subset-of-columns"></a>Selecionar um subconjunto de colunas

Use aplicação de predicado para melhorar o desempenho de uma consulta que seleciona um subconjunto de colunas de uma tabela externa.

Nesta consulta, o SQL Server inicia um trabalho map-reduce para pré-processar o arquivo de texto delimitado por Hadoop para que somente os dados de duas colunas, customer.name e customer.zip_code, sejam copiados para o SQL Server.

```sql
SELECT customer.name, customer.zip_code
FROM customer
WHERE customer.account_balance < 200000
```

### <a name="pushdown-for-basic-expressions-and-operators"></a>Aplicação de operadores e expressões básicas

O SQL Server permite os seguintes operadores e expressões básicas para a aplicação de predicado.

- Operadores de comparação binária (`<`, `>`, `=`, `!=`, `<>`, `>=`, `<=`) para valores temporais, de data e numéricos.
- Operadores aritméticos (`+`, `-`, `*`, `/`, `%`).
- Operadores lógicos (`AND`, `OR`).
- Operadores unários (`NOT`, `IS NULL`, `IS NOT NULL`).

Os operadores `BETWEEN`, `NOT`, `IN` e `LIKE` podem ser propagados. O comportamento real depende de como o otimizador de consulta reescreve as expressões do operador como uma série de instruções que usam operadores relacionais básicos.

A consulta neste exemplo tem vários predicados que podem ser propagados para o Hadoop. O SQL Server pode enviar por push trabalhos map-reduce para o Hadoop para executar o predicado `customer.account_balance <= 200000`. A expressão `BETWEEN 92656 AND 92677` também é composta por operações binárias e lógicas que podem ser enviadas por push para Hadoop. A lógica **E** no `customer.account_balance AND customer.zipcode` é uma expressão final.

Dada essa combinação de predicados, os trabalhos map-reduce podem executar tudo da cláusula WHERE. Somente os dados que atendem aos critérios `SELECT` são copiados de volta para o SQL Server.

```sql
SELECT * FROM customer 
WHERE customer.account_balance <= 200000 
    AND customer.zipcode BETWEEN 92656 AND 92677
```

## <a name="examples"></a>Exemplos

### <a name="force-pushdown"></a>Forçar aplicação

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (FORCE EXTERNALPUSHDOWN);
```

### <a name="disable-pushdown"></a>Desabilitar aplicação

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (DISABLE EXTERNALPUSHDOWN);
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o PolyBase, consulte [What is PolyBase](polybase-guide.md) (O que é o PolyBase?).
