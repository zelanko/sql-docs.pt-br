---
title: sp_delete_log_shipping_primary_secondary (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_log_shipping_primary_secondary_TSQL
- sp_delete_log_shipping_primary_secondary
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_log_shipping_primary_secondary
ms.assetid: d6f71a12-f7b1-4a1c-9639-a533b8287b0c
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8276a23224495b7bcc69721fd5317d0b2b87821a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68009173"
---
# <a name="spdeletelogshippingprimarysecondary-transact-sql"></a>sp_delete_log_shipping_primary_secondary (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove a entrada de um banco de dados secundário no servidor primário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_log_shipping_primary_secondary  
    [ @primary_database = ] 'primary_database',   
    [ @secondary_server = ] 'secondary_server',   
    [ @secondary_database = ] 'secondary_database'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @primary_database = ] 'primary_database'` É o nome do banco de dados no servidor primário. *primary_database* está **sysname**, sem padrão.  
  
`[ @secondary_server = ] 'secondary_server'` É o nome do servidor secundário. *secondary_server* está **sysname**, sem padrão.  
  
`[ @secondary_database = ] 'secondary_database'` É o nome do banco de dados secundário. *secondary_database* está **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 nenhuma.  
  
## <a name="remarks"></a>Comentários  
 **sp_delete_log_shipping_primary_secondary** deve ser executado a partir de **mestre** banco de dados no servidor primário. Esse procedimento armazenado remove a entrada para um banco de dados secundário **log_shipping_primary_secondaries** no servidor primário.  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 No seguinte exemplo, `sp_delete_log_shipping_primary_secondary` é usado para excluir o banco de dados secundário `LogShipAdventureWorks` do servidor secundário `FLATIRON`.  
  
```  
EXEC master.dbo.sp_delete_log_shipping_primary_secondary  
@primary_database = N'AdventureWorks'  
,@secondary_server = N'FLATIRON'  
,@secondary_database = N'LogShipAdventureWorks';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
