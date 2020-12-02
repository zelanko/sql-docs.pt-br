---
description: '% (Módulo) (Transact-SQL)'
title: '% (Módulo) (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- modulo
- modulus
- '% (Modulo)'
- '% (Modulus)'
- MOD_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- '% (modulo operator)'
- '% (modulus operator)'
- remainder of division operation
- modulo operator (%)
- modulus operator (%)
ms.assetid: f93c662e-f405-486e-bf23-a2d03907b5bd
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 284d4110c4c0a2b8b4b7a1c26c4a4148fb5c50a6
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96124411"
---
# <a name="-modulus-transact-sql"></a>% (Módulo) (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Retorna o resto de um número dividido por outro.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
dividend % divisor  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *dividend*  
 É a expressão numérica a ser dividida. *dividend* deve ser uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) válida de um dos tipos de dados nas categorias de tipo de dados inteiros e monetários ou no tipo de dados **numeric**.  
  
 *divisor*  
 É a expressão numérica pela qual dividir o dividendo. *divisor* deve ser qualquer expressão válida de um dos tipos de dados nas categorias de tipos de dados inteiros e monetários ou no tipo de dados **numeric**.  
  
## <a name="result-types"></a>Tipos de resultado  
 Determinado por tipos de dados dos dois argumentos.  
  
## <a name="remarks"></a>Comentários  
 Use o operador aritmético de módulo na lista de seleção da instrução SELECT com qualquer combinação de nomes de coluna, constantes numéricas ou qualquer expressão válida das categorias de tipo de dados inteiros ou monetários ou o tipo de dados **numeric**.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-simple-example"></a>a. Exemplo simples  
 O exemplo a seguir divide o número 38 por 5. Isto resulta em 7 como a parte inteira do resultado e demonstra como o módulo retorna o resto de 3.  
  
```sql  
SELECT 38 / 5 AS Integer, 38 % 5 AS Remainder;
```  
  
### <a name="b-example-using-columns-in-a-table"></a>B. Exemplo com o uso de colunas em uma tabela  
 O exemplo a seguir retorna o número da ID de produto, o preço unitário do produto e o módulo (resto) da divisão do preço de cada produto, convertido em um valor inteiro, pelo número de produtos ordenados.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT TOP(100)ProductID, UnitPrice, OrderQty,  
   CAST((UnitPrice) AS INT) % OrderQty AS Modulo  
FROM Sales.SalesOrderDetail;  
GO  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Exemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-simple-example"></a>C: Exemplo simples  
 O exemplo a seguir mostra os resultados para o operador `%` durante a divisão de 3 por 2.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT TOP(1) 3%2 FROM dimEmployee;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
---------   
1         
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções internas &#40;Transact-SQL&#41;](~/t-sql/functions/functions.md)   
 [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md)   
 [Operadores &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)   
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)   
 [%= &#40;Atribuição de módulo&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/modulo-equals-transact-sql.md)   
 [Operadores compostos &#40;Transact-SQL&#41;](../../t-sql/language-elements/compound-operators-transact-sql.md)  
  
  


