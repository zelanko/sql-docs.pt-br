---
title: DATALENGTH (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DATALENGTH_TSQL
- DATALENGTH
dev_langs:
- TSQL
helpviewer_keywords:
- number of bytes representing expression
- data types [SQL Server], length
- DATALENGTH function
- expressions [SQL Server], length
- lengths [SQL Server], data
ms.assetid: 00f377f1-cc3e-4eac-be47-b3e3f80267c9
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 77c7eb1fcde9b073b3c08f412ac0e46519763c74
ms.openlocfilehash: d8887c50cb482e27bce63e08aa18b8ca54616faa
ms.contentlocale: pt-br
ms.lasthandoff: 10/17/2017

---
# <a name="datalength-transact-sql"></a>DATALENGTH (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

Retorna o número de bytes usado para representar qualquer expressão.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```sql
DATALENGTH ( expression )   
```  
  
## <a name="arguments"></a>Argumentos  
*expressão*  
É um [expressão](../../t-sql/language-elements/expressions-transact-sql.md) de qualquer tipo de dados.
  
## <a name="return-types"></a>Tipos de retorno
**bigint** se *expressão* é o **varchar (max)**, **nvarchar (max)** ou **varbinary (max)** tipos de dados. Caso contrário, **int**.
  
## <a name="remarks"></a>Comentários  
DATALENGTH é especialmente útil com **varchar**, **varbinary**, **texto**, **imagem**, **nvarchar**, e **ntext** tipos de dados, pois esses tipos de dados podem armazenar dados de comprimento variável.
  
O DATALENGTH de NULL é NULL.
  
> [!NOTE]  
>  Os níveis de compatibilidade podem afetar os valores de retorno. Para obter mais informações sobre níveis de compatibilidade, veja [Nível de compatibilidade de ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir localiza o comprimento da coluna `Name` na tabela `Product`.
  
```sql
-- Uses AdventureWorks  
  
SELECT length = DATALENGTH(EnglishProductName), EnglishProductName  
FROM dbo.DimProduct  
ORDER BY EnglishProductName;  
GO  
```  
  
## <a name="see-also"></a>Consulte também
[LEN &#40; Transact-SQL &#41;](../../t-sql/functions/len-transact-sql.md)  
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[Funções do sistema &#40; Transact-SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)
  
  


