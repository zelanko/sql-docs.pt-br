---
title: "Quais são as funções de banco de dados do Microsoft SQL? | Microsoft Docs"
ms.custom: 
ms.date: 06/28/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, database-engine, pdw, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- built-in functions [SQL Server]
- function [SQL Server] See functions [SQL Server]
- functions [Transact-SQL]
- functions [SQL Server], about functions
- scalar functions
- functions [SQL Server]
ms.assetid: 17186213-5ab5-40b0-b470-b660af1ec44c
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: fa55a0b066db617ef0d6f2f0471ad6866cac2d73
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="what-are-the-sql-database-functions"></a>Quais são as funções de banco de dados SQL?
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

Saiba mais sobre as categorias de funções internas que você pode usar com bancos de dados SQL. Você pode usar as funções internas ou criar suas próprias funções definidas pelo usuário.
  
## <a name="aggregate-functions"></a>Funções de agregação

As funções de agregação executam um cálculo em um conjunto de valores e retornam um único valor. Elas são permitidas na lista de seleção ou a cláusula HAVING de uma instrução SELECT. Você pode usar uma agregação em combinação com a cláusula GROUP BY para calcular a agregação em categorias de linhas. Use a cláusula OVER para calcular a agregação em um intervalo específico de valor. A cláusula OVER não pode seguir as agregações GROUPING ou GROUPING_ID.

Todas as funções de agregação são determinísticas, o que significa que elas sempre retornarem o mesmo valor ao serem executados nos mesmos valores de entrada. Para obter mais informações, consulte [determinísticas e funções não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md). |

## <a name="analytic-functions"></a>Funções analíticas
As funções analíticas computam um valor agregado com base em um grupo de linhas. No entanto, ao contrário das funções de agregação, funções analíticas podem retornar várias linhas para cada grupo. Você pode usar funções analíticas para computar médias móveis, somas acumuladas, porcentagens, ou os primeiros N resultados dentro de um grupo.

## <a name="ranking-functions"></a>Funções de classificação
As funções de classificação retornam um valor de classificação para cada linha em uma partição. Dependendo da função usada, algumas linhas podem receber o mesmo valor que outras. As funções de classificação são não determinísticas.

## <a name="rowset-functions"></a>Funções de conjunto de linhas
Funções de conjunto de linhas retornam um objeto que pode ser usado como referências de tabela em uma instrução SQL.

## <a name="scalar-functions"></a>Funções escalares
Funcionam em um valor único e retornam um valor único. As funções escalares podem ser usadas onde uma expressão é válida.

### <a name="categories-of-scalar-functions"></a>Categorias de funções escalares
  
|Categoria da função|Description|  
|-----------------------|-----------------|  
|[Funções de configuração](configuration-functions-transact-sql.md)|Retornam informações sobre a configuração atual.|  
|[Funções de conversão](conversion-functions-transact-sql.md)|Suporte para conversão de tipos de dados.|  
|[Funções de cursor](cursor-functions-transact-sql.md)|Retornam informações sobre cursores.|  
|[Dados de data e hora tipos e funções](date-and-time-data-types-and-functions-transact-sql.md)|Executam operações em uma data e valores de entrada de hora e retornam valores de cadeia de caracteres, numéricos ou de data e hora.|  
|[Funções JSON](json-functions-transact-sql.md)|Validar, consultar ou alterar dados JSON.|  
|[Funções lógicas](http://msdn.microsoft.com/library/5b2b4546-951b-462d-91d5-e41fc5acd6f9)|Executam operações lógicas.|  
|[Funções matemáticas](mathematical-functions-transact-sql.md)|Executam cálculos baseados em valores de entrada fornecidos como parâmetros às funções e retorna valores numéricos.|  
|[Funções de metadados](metadata-functions-transact-sql.md)|Retornam informações sobre o banco de dados e objetos de banco de dados.|  
|[Funções de segurança](security-functions-transact-sql.md)|Retornam informações sobre usuários e funções.|  
|[Funções de cadeia de caracteres](string-functions-transact-sql.md)|Executar operações em uma cadeia de caracteres (**char** ou **varchar**) valor de entrada e retorna um valor de cadeia de caracteres ou numérica.|  
|[Funções do Sistema](../../relational-databases/system-functions/system-functions-for-transact-sql.md)|Executam operações e informações de retorno sobre valores, objetos e configurações em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Funções estatísticas do sistema](system-statistical-functions-transact-sql.md)|Retornam informações estatísticas sobre o sistema.|  
|[Funções de texto e imagem](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)|Executam operações em valores de entrada de texto ou imagem ou colunas e retornam informações sobre o valor.|  
  
## <a name="function-determinism"></a>Determinismo de função  
 As funções internas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são determinísticas ou não determinísticas. As funções são determinísticas quando retornam sempre o mesmo resultado quando são chamadas com o uso de um conjunto específico de valores de entrada. As funções são não determinísticas quando podem retornar resultados diferentes sempre que são chamadas, mesmo com o mesmo conjunto específico de valores de entrada. Para obter mais informações, consulte [determinísticas e funções não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)  
  
## <a name="function-collation"></a>Agrupamento de funções  
 As funções que usam uma entrada de cadeia de caracteres e retornam uma saída de cadeia de caracteres usam o agrupamento da cadeia de caracteres de entrada para a saída.  
  
 As funções que usam entradas de não caracteres e retornam uma cadeia de caracteres usam o agrupamento padrão do banco de dados atual para a saída.  
  
 As funções que usam várias entradas de cadeia de caracteres e retornam uma cadeia de caracteres usam as regras de precedência de agrupamento para definir o agrupamento da cadeia de caracteres de saída. Para obter mais informações, consulte [precedência de agrupamento &#40; Transact-SQL &#41; ](../../t-sql/statements/collation-precedence-transact-sql.md).  
  
## <a name="see-also"></a>Consulte também  
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md)   
 [Usando procedimentos armazenados &#40; MDX &#41;](../../mdx/using-stored-procedures-mdx.md)  
  
  
