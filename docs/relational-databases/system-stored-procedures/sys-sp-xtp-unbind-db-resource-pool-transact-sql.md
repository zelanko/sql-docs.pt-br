---
title: sys. sp_xtp_unbind_db_resource_pool (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_xtp_unbind_db_resource_pool_TSQL
- sp_xtp_unbind_db_resource_pool
- sys.sp_xtp_unbind_db_resource_pool_TSQL
- sys.sp_xtp_unbind_db_resource_pool
dev_langs:
- TSQL
helpviewer_keywords:
- sp_xtp_unbind_db_resource_pool
- sys.sp_xtp_unbind_db_resource_pool
ms.assetid: 695a796d-087e-4bc8-99d0-ddc342604c75
author: stevestein
ms.author: sstein
ms.openlocfilehash: be0f8e7b410abb2e9027ce0b773d1a1ad5a14465
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68041000"
---
# <a name="syssp_xtp_unbind_db_resource_pool-transact-sql"></a>sys.sp_xtp_unbind_db_resource_pool (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Este procedimento do sistema remove uma associação existente entre um banco de dados e um pool de recursos para fins de controlar o uso de memória do [!INCLUDE[hek_2](../../includes/hek-2-md.md)].  Se não houver um pool associado no momento ao banco de dados especificado, o sucesso será retornado. Quando o banco de dados não está associado, a memória alocada anteriormente para objetos com otimização de memória permanece alocada para o pool de recursos anterior. Você precisa reiniciar o banco de dados para liberar a memória alocada. Quando um banco de dados é desassociado do pool de recursos, a associação recorre ao pool de recursos DEFAULT.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
sys.sp_xtp_unbind_db_resource_pool 'database_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 database_name  
 O nome de um banco de dados habilitado para [!INCLUDE[hek_2](../../includes/hek-2-md.md)] existente.  
  
#### <a name="parameters"></a>Parâmetros  
  
## <a name="messages"></a>Mensagens  
 Se o banco de dados foi associado a um pool de recursos nomeado, o procedimento retornará com êxito. No entanto, você deve reiniciar o banco de dados para a desassociação entrar em vigor.  
 Se não houver nenhuma associação para o banco de dados especificado, o `sp_xtp_unbind_db_resource_pool` retornará o êxito, mas dará a mensagem informativa:  
  
```  
Msg 41374, Level 16, State 1, Procedure sp_xtp_unbind_db_resource_pool_internal, Line 140.  
Database 'Hekaton_DB' does not have a binding to a resource pool.  
  
```  
  
## <a name="example"></a>Exemplo  
 O código de exemplo desassocia o banco de dados Hekaton_DB do pool de recursos do [!INCLUDE[hek_2](../../includes/hek-2-md.md)] ao qual está associado.  Se Hekaton_DB não estiver associado no momento a um pool de recursos do [!INCLUDE[hek_2](../../includes/hek-2-md.md)], uma mensagem será emitida. O banco de dados deve ser reiniciado para a desassociação entrar em vigor.  
  
```sql  
sys.sp_xtp_unbind_db_resource_pool 'Hekaton_DB'  
```  
  
## <a name="requirements"></a>Requisitos  
  
-   O banco de dados especificado por `database_name` deve ter uma associação para um pool de recursos do [!INCLUDE[hek_2](../../includes/hek-2-md.md)].  
  
-   Requer a permissão CONTROL SERVER.  
  
## <a name="see-also"></a>Consulte Também  
 [Associar um banco de dados com tabelas com otimização de memória a um pool de recursos](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [sys.sp_xtp_bind_db_resource_pool &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sys-sp-xtp-bind-db-resource-pool-transact-sql.md)  
  
  
