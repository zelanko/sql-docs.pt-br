---
title: '@@DBTS (Transact-SQL) | Microsoft Docs'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- '@@DBTS_TSQL'
- '@@DBTS'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@DBTS function'
- timestamp data type
ms.assetid: 91842ddd-91c0-4445-a03f-116f6bc991d0
caps.latest.revision: 35
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: c6ea46c5187f00190cb39ba9a502b3ecb6a28bc6
ms.openlocfilehash: 4a90150c55cdeb89788fdb86faf8aef8a1efdcd2
ms.contentlocale: pt-br
ms.lasthandoff: 09/19/2017

---
# <a name="x40x40dbts-transact-sql"></a>& #x 40; & #x 40; DBTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Retorna o valor do tipo de dados **timestamp** atual para o banco de dados atual. Este carimbo de data e hora é garantido como exclusivo no banco de dados.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```
@@DBTS  
```  
  
## <a name="return-types"></a>Tipos de retorno
**varbinary**
  
## <a name="remarks"></a>Comentários  
@@DBTS retorna o valor usado por último carimbo de hora do banco de dados atual. Um novo valor de carimbo de data e hora é gerado quando uma linha com uma coluna **timestamp** é inserida ou atualizada.
  
O @@DBTS função não é afetada pelas alterações nos níveis de isolamento da transação.
  
## <a name="examples"></a>Exemplos  
O exemplo a seguir retorna atual **timestamp** do [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] banco de dados.
  
```sql
USE AdventureWorks2012;  
GO  
SELECT @@DBTS;  
```  
  
## <a name="see-also"></a>Consulte também
[Funções de configuração &#40; Transact-SQL &#41;](../../t-sql/functions/configuration-functions-transact-sql.md)  
[Simultaneidade de cursor &#40; ODBC &#41;](../../relational-databases/native-client-odbc-cursors/properties/cursor-concurrency-odbc.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION &#40; Transact-SQL &#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)
  
  

