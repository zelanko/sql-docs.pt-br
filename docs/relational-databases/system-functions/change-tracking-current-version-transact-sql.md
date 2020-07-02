---
title: CHANGE_TRACKING_CURRENT_VERSION (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_CURRENT_VERSION_TSQL
- CHANGE_TRACKING_CURRENT_VERSION
dev_langs:
- TSQL
helpviewer_keywords:
- change tracking [SQL Server], CHANGE_TRACKING_CURRENT_VERSION
- CHANGE_TRACKING_CURRENT_VERSION
ms.assetid: 3027c4f7-6b4d-4089-a369-5926e8a8da1c
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3b3b32313c296af2d7e08e9797a991171a4be40d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85738616"
---
# <a name="change_tracking_current_version-transact-sql"></a>CHANGE_TRACKING_CURRENT_VERSION (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Retorna uma versão que está associada à última transação confirmada. Essa versão pode ser usada quando você enumera as alterações usando [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CHANGE_TRACKING_CURRENT_VERSION ( )  
```  
  
## <a name="return-type"></a>Tipo de retorno  
 **bigint**  
  
## <a name="remarks"></a>Comentários  
 Retorna NULL quando o controle de alterações não está habilitado para o banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir declara a variável local `@next_baseline` para o armazenamento da versão atual das alterações rastreadas e, em seguida, usa a função `CHANGE_TRACKING_CURRENT_VERSION()` para obter o valor da variável.  
  
```sql  
DECLARE @next_baseline bigint;  
SET @next_baseline = CHANGE_TRACKING_CURRENT_VERSION();  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções de Controle de Alterações &#40;&#41;de Transact-SQL](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [&#41;CHANGEtable &#40;Transact-SQL](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [&#41;&#40;Transact-SQL de CHANGE_TRACKING_MIN_VALID_VERSION](../../relational-databases/system-functions/change-tracking-min-valid-version-transact-sql.md)   
 [Controle de alterações de dados &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
