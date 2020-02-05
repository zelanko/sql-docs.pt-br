---
title: Cálculos de aplicação no PolyBase | Microsoft Docs
ms.date: 04/23/2019
ms.prod: sql
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.reviewer: ''
monikerRange: '>= sql-server-2016 || =sqlallproducts-allversions'
ms.openlocfilehash: 94e360c19c4f734b891701a4ec40c82cdb57927d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71710480"
---
# <a name="pushdown-computations-in-polybase"></a>Cálculos de aplicação no PolyBase

## <a name="dmv"></a>DMV

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

A computação de aplicação melhora o desempenho de consultas em seu cluster do Hadoop.

## <a name="enable-pushdown"></a>Habilitar aplicação

As etapas para habilitar a aplicação são abordadas no artigo a seguir:

[Habilitar cálculo de aplicação no Hadoop](polybase-configure-hadoop.md#pushdown)

## <a name="select-a-subset-of-rows"></a>Selecionar um subconjunto de linhas

Use aplicação de predicado para melhorar o desempenho de uma consulta que seleciona um subconjunto de linhas de uma tabela externa.

Neste exemplo, o SQL Server 2016 inicia um trabalho de map-reduce para recuperar as linhas que correspondem ao predicado `customer.account_balance < 200000` no Hadoop. Como a consulta pode ser concluída com êxito sem examinar todas as linhas na tabela, somente as linhas que atendem aos critérios de predicado são copiadas para o SQL Server. Isso economiza bastante tempo e exige menos espaço de armazenamento temporário quando o número de saldos do cliente < 200000 é pequeno em comparação com o número de clientes com saldos o cliente >= 200000.

```sql
SELECT * FROM customer WHERE customer.account_balance < 200000
SELECT * FROM SensorData WHERE Speed > 65;  
```

### <a name="select-a-subset-of-columns"></a>Selecionar um subconjunto de colunas

Use aplicação de predicado para melhorar o desempenho de uma consulta que seleciona um subconjunto de colunas de uma tabela externa.

Nesta consulta, o SQL Server inicia um trabalho map-reduce para pré-processar o arquivo de texto delimitado por Hadoop para que somente os dados de duas colunas, customer.name e customer.zip_code, serão copiados para o SQL Server PDW.

```sql
SELECT customer.name, customer.zip_code FROM customer WHERE customer.account_balance < 200000
```

### <a name="pushdown-for-basic-expressions-and-operators"></a>Aplicação de operadores e expressões básicas

O SQL Server permite os seguintes operadores e expressões básicas para a aplicação de predicado.

+ Operadores de comparação binária ( \<, >, =, !=, <>, >=, <= ) para valores de hora, data e numéricos.

+ Operadores aritméticos ( +, -, *, /, % ).

+ Operadores lógicos (AND, OR).

+ Operadores unários (NOT, IS NULL, IS NOT NULL).

Os operadores BETWEEN, NOT, IN e LIKE podem ser propagados. O comportamento real depende de como o otimizador de consulta reescreve as expressões do operador como uma série de instruções que usam operadores relacionais básicos.

A consulta neste exemplo tem vários predicados que podem ser propagados para o Hadoop. O SQL Server pode enviar por push trabalhos map-reduce para o Hadoop para executar o predicado `customer.account_balance <= 200000`. A expressão `BETWEEN 92656 and 92677` também é composta por operações binárias e lógicas que podem ser enviadas por push para Hadoop. A lógica **E** no `customer.account_balance and customer.zipcode` é uma expressão final.

Dada essa combinação de predicados, os trabalhos map-reduce podem executar tudo da cláusula WHERE. Apenas os dados que atendem aos critérios de SELECT serão copiados para o SQL Server PDW.

```sql
SELECT * FROM customer WHERE customer.account_balance <= 200000 AND customer.zipcode BETWEEN 92656 AND 92677
```

## <a name="force-pushdown"></a>Forçar aplicação

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (FORCE EXTERNALPUSHDOWN);
```

## <a name="disable-pushdown"></a>Desabilitar aplicação

```sql
SELECT * FROM [dbo].[SensorData]
WHERE Speed > 65
OPTION (DISABLE EXTERNALPUSHDOWN);
```

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre o PolyBase, consulte [What is PolyBase](polybase-guide.md) (O que é o PolyBase?).
