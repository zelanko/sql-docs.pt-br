---
title: CHECKSUM_AGG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f74f05dcb91885bf6f95571242699672f10fb871
ms.sourcegitcommit: 032273bfbc240fe22ac6c1f6601a14a6d99573f7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2019
ms.locfileid: "55513806"
---
# <a name="checksumagg-transact-sql"></a>CHECKSUM_AGG (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Essa função retorna a soma de verificação dos valores em um grupo. `CHECKSUM_AGG` ignora valores nulos. A [cláusula OVER](../../t-sql/queries/select-over-clause-transact-sql.md) pode seguir `CHECKSUM_AGG`.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
CHECKSUM_AGG ( [ ALL | DISTINCT ] expression )  
```  
  
## <a name="arguments"></a>Argumentos  
**ALL**  
Aplica a função de agregação a todos os valores. ALL é o argumento padrão.
  
DISTINCT  
Especifica que `CHECKSUM_AGG` retorna a soma de verificação de valores exclusivos.
  
*expressão*  
Uma [expression](../../t-sql/language-elements/expressions-transact-sql.md) de inteiro. `CHECKSUM_AGG` não permite o uso de funções de agregação nem de subconsultas.
  
## <a name="return-types"></a>Tipos de retorno
Retorna a soma de verificação de todos os valores de *expression* como **int**.
  
## <a name="remarks"></a>Remarks  
`CHECKSUM_AGG` pode detectar alterações em uma tabela.
  
O resultado de `CHECKSUM_AGG` não depende da ordem das linhas na tabela. Além disso, as funções de `CHECKSUM_AGG` permitem o uso da palavra-chave `DISTINCT` e da cláusula `GROUP BY`.
  
Se o valor de lista de uma expressão for alterado, a lista de valores da soma de verificação de lista provavelmente também será alterada. No entanto, há uma pequena possibilidade de que a soma de verificação calculada não seja alterada.
  
O `CHECKSUM_AGG` tem uma funcionalidade semelhante à de outras funções de agregação. Para obter mais informações, consulte [Funções de agregação &#40;Transact-SQL&#41;](../../t-sql/functions/aggregate-functions-transact-sql.md).
  
## <a name="examples"></a>Exemplos  
Estes exemplos usam `CHECKSUM_AGG` para detectar alterações na coluna `Quantity` da tabela `ProductInventory` no banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].
  
```sql
--Get the checksum value before the column value is changed.  

SELECT CHECKSUM_AGG(CAST(Quantity AS int))  
FROM Production.ProductInventory;  
GO  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
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
  
```
------------------------  
287  
```  
  
## <a name="see-also"></a>Confira também
[CHECKSUM &#40;Transact-SQL&#41;](../../t-sql/functions/checksum-transact-sql.md)  
[HASHBYTES &#40;Transact-SQL&#41;](../../t-sql/functions/hashbytes-transact-sql.md)  
[BINARY_CHECKSUM  &#40;Transact-SQL&#41;](../../t-sql/functions/binary-checksum-transact-sql.md)
[cláusula OVER &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md)
  
