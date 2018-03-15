---
title: cursor (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|data-types
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- cursor data type
ms.assetid: fbea16ef-f2cc-4734-9149-ec2598fd3cca
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b9fa1c8e8fea6aabf8fe8a0e6e84f82f7220facf
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="cursor-transact-sql"></a>cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Um tipo de dados para parâmetros OUTPUT de variáveis ou procedimento armazenado que contém uma referência a um cursor.
  
## <a name="remarks"></a>Remarks  
As operações que podem fazer referência a variáveis e parâmetros que têm o tipo de dados **cursor** são:
-   As instruções DECLARE *@local_variable* e SET *@local_variable*.  
-   As instruções de cursor OPEN, FETCH, CLOSE e DEALLOCATE.  
-   Parâmetros de saída de procedimento armazenado.  
-   A função CURSOR_STATUS.  
-   Os procedimentos armazenados do sistema **sp_cursor_list**, **sp_describe_cursor**, **sp_describe_cursor_tables** e **sp_describe_cursor_columns**.  
  
A coluna de saída **cursor_name** de **sp_cursor_list** e de **sp_describe_cursor** retorna o nome da variável de cursor.
  
Qualquer variável criada com o tipo de dados **cursor** é anulável.
  
O tipo de dados **cursor** não pode ser usado para uma coluna em uma instrução CREATE TABLE.
  
## <a name="see-also"></a>Consulte também
[CAST e CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CURSOR_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-status-transact-sql.md)  
[Conversão de tipo de dados &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  
