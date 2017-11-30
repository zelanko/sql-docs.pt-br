---
title: sys. fn_translate_permissions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.fn_translate_permissions
- sys.fn_translate_permissions_TSQL
- fn_translate_permissions
- fn_translate_permissions_TSQL
dev_langs: TSQL
helpviewer_keywords:
- permissions bitmask [SQL Server]
- sys.fn_translate_permissions function
- fn_translate_permissions function
ms.assetid: ac97121f-2bd0-4f71-8e45-42c8584edbc5
caps.latest.revision: "18"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ed217e60301c2ee877381a3aebc7b9f3d6fcf7bc
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2017
---
# <a name="sysfntranslatepermissions-transact-sql"></a>sys.fn_translate_permissions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Traduz o bitmask de permissões retornado pelo Rastreamento do SQL em uma tabela de nomes de permissões.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_translate_permissions ( level , perms )  
```  
  
## <a name="arguments"></a>Argumentos  
 *nível*  
 É o tipo de protegível ao qual a permissão é aplicada. *nível de* é **nvarchar (60)**.  
  
 *permissões*  
 É um bitmask retornado na coluna de permissões. *permissões* é **varbinary (16)**.  
  
## <a name="returns"></a>Retorna  
 **table**  
  
## <a name="remarks"></a>Comentários  
 O valor retornado no **permissões** coluna de rastreamento do SQL é uma representação de inteiro de um bitmask usada pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao calcular permissões efetivas. Cada um dos 25 tipos de protegíveis tem seu próprio conjunto de permissões com valores numéricos correspondentes. **sys. fn_translate_permissions** converte esse bitmask em uma tabela de nomes de permissões.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="example"></a>Exemplo  
 A consulta a seguir usa `sys.fn_builtin_permissions` para exibir as permissões que se aplicam a certificados e, em seguida, usa `sys.fn_translate_permissions` para retornar os resultados de bitmask de permissões.  
  
```  
SELECT * FROM sys.fn_builtin_permissions('CERTIFICATE');  
SELECT '0001' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0001);  
SELECT '0010' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0010);  
SELECT '0011' AS Input, * FROM sys.fn_translate_permissions('CERTIFICATE', 0011);  
```  
  
## <a name="see-also"></a>Consulte também  
 [Permissões &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/security/permissions-database-engine.md)   
 [sys.server_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)   
 [sys.database_permissions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)  
  
  
