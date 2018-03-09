---
title: CHECKSUM_AGG (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CHECKSUM_AGG
- CHECKSUM_AGG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- checksum values
- CHECKSUM_AGG function
- groups [SQL Server], checksum values
ms.assetid: cdede70c-4eb5-4c92-98ab-b07787ab7222
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 3499cd8fb118d12fdbf450c23f2919fd0003cee7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="checksumagg-transact-sql"></a>CHECKSUM_AGG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna a soma de verificação dos valores em um grupo. Valores nulos são ignorados. Pode ser seguido de [cláusula OVER](../../t-sql/queries/select-over-clause-transact-sql.md).
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CHECKSUM_AGG ( [ ALL | DISTINCT ] expression )  
```  
  
## <a name="arguments"></a>Argumentos  
**ALL**  
Aplica a função de agregação a todos os valores. ALL é o padrão.
  
DISTINCT  
Especifica que CHECKSUM_AGG retorna a soma de verificação de valores exclusivos.
  
*expressão*  
É um número inteiro [expressão](../../t-sql/language-elements/expressions-transact-sql.md). Funções de agregação e subconsultas não são permitidas.
  
## <a name="return-types"></a>Tipos de retorno
Retorna a soma de verificação de todos os *expressão* valores como **int**.
  
## <a name="remarks"></a>Comentários  
CHECKSUM_AGG pode ser usado para detectar alterações em uma tabela.
  
A ordem das linhas na tabela não afeta o resultado de CHECKSUM_AGG. Além disso, as funções de CHECKSUM_AGG podem ser usadas com a palavra-chave DISTINCT e a cláusula GROUP BY.
  
Se um dos valores da lista de expressão for alterado, em geral, a soma de verificação da lista também será alterada. Entretanto, há uma pequena chance de que a soma de verificação não seja alterada.
  
CHECKSUM_AGG tem uma funcionalidade semelhante a outras funções de agregação. Para obter mais informações, consulte [funções de agregação &#40; Transact-SQL &#41; ](../../t-sql/functions/aggregate-functions-transact-sql.md).
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir usa a função `CHECKSUM_AGG` para detectar as alterações na coluna `Quantity` da tabela `ProductInventory` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].
  
```sql
--Get the checksum value before the column value is changed.  
SELECT CHECKSUM_AGG(CAST(Quantity AS int))  
FROM Production.ProductInventory;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
------------------------  
262  
```  
  
```sql
UPDATE Production.ProductInventory   
SET Quantity=125  
WHERE Quantity=100;  
GO  
--Get the checksum of the modified column.  
SELECT CHECKSUM_AGG(CAST(Quantity AS int))  
FROM Production.ProductInventory;  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
------------------------  
287  
```  
  
## <a name="see-also"></a>Consulte também
[Soma de verificação &#40; Transact-SQL &#41;](../../t-sql/functions/checksum-transact-sql.md)  
[SOBRE cláusula &#40; Transact-SQL &#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
  
