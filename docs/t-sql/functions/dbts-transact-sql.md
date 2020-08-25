---
description: '&#x40;&#x40;DBTS (Transact-SQL)'
title: DBTS (Transact-SQL)
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1f11adca5f8a3fe72a0365e84a746cdec2d5e049
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88417402"
---
# <a name="x40x40dbts-transact-sql"></a>&#x40;&#x40;DBTS (Transact-SQL)

[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

Esta função retorna o valor do tipo de dados **timestamp** atual para o banco de dados atual. O banco de dados atual terá um valor de carimbo do carimbo de data/hora exclusivo garantido.
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
@@DBTS  
```  

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="return-types"></a>Tipos de retorno
**varbinary**
  
## <a name="remarks"></a>Comentários  
@@DBTS retorna o valor do carimbo de data/hora do banco de dados atual usado pela última vez. Uma inserção ou atualização de uma linha com uma coluna **timestamp** gera um novo valor de carimbo de data/hora.
  
Alterações nos níveis de isolamento não afetam a função @@DBTS.
  
## <a name="examples"></a>Exemplos  
Este exemplo retorna o **timestamp** atual do banco de dados [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].
  
```sql
USE AdventureWorks2012;  
GO  
SELECT @@DBTS;  
```  
  
## <a name="see-also"></a>Confira também
[Funções de configuração &#40;Transact-SQL&#41;](../../t-sql/functions/configuration-functions-transact-sql.md)  
[Simultaneidade do cursor &#40;ODBC&#41;](../../relational-databases/native-client-odbc-cursors/properties/cursor-concurrency-odbc.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[MIN_ACTIVE_ROWVERSION &#40;Transact-SQL&#41;](../../t-sql/functions/min-active-rowversion-transact-sql.md)
  
  
