---
title: sp_delete_log_shipping_primary_database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_delete_log_shipping_primary_database
- sp_delete_log_shipping_primary_database_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_log_shipping_primary_database
ms.assetid: cb1d5d00-2805-4d47-bd04-545232067345
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 76a1b1ac129d33866984eb7a0f428149e4e299a2
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33258711"
---
# <a name="spdeletelogshippingprimarydatabase-transact-sql"></a>sp_delete_log_shipping_primary_database (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Este procedimento armazenado remove o envio de logs do banco de dados primário, incluindo tarefas de backup, assim como o histórico local e remoto. Somente use esse procedimento armazenado depois de remover os bancos de dados secundários usando **sp_delete_log_shipping_primary_secondary**.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_log_shipping_primary_database  
[ @database = ] 'database'  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@database =** ] '*banco de dados*'  
 É o nome do banco de dados primário de envio de logs. *banco de dados* é **sysname**, sem padrão, e não pode ser NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma.  
  
## <a name="remarks"></a>Remarks  
 **sp_delete_log_shipping_primary_database** deve ser executado a partir de **mestre** banco de dados no servidor primário. Esse procedimento armazenado faz o seguinte:  
  
1.  Exclui o trabalho de backup do banco de dados primário especificado.  
  
2.  Remove o registro de monitor local em **log_shipping_monitor_primary** no servidor primário.  
  
3.  Remove entradas correspondentes em **log_shipping_monitor_history_detail** e **log_shipping_monitor_error_detail**.  
  
4.  Se o servidor monitor for diferente do servidor primário, remove o registro de monitor em **log_shipping_monitor_primary** no servidor monitor.  
  
5.  Remove entradas correspondentes em **log_shipping_monitor_history_detail** e **log_shipping_monitor_error_detail** no servidor monitor.  
  
6.  Remove a entrada em **log_shipping_primary_databases** para este banco de dados primário.  
  
7.  Chamadas **sp_delete_log_shipping_alert_job** no servidor monitor.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função fixa de servidor pode executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 Este exemplo ilustra o uso **sp_delete_log_shipping_primary_database** para excluir o banco de dados primário **AdventureWorks2012**.  
  
```  
EXEC master.dbo.sp_delete_log_shipping_primary_database @database = N'AdventureWorks2012';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Sobre o envio de logs & #40; SQL Server & #41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
