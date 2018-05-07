---
title: sp_dbmmonitorupdate (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorupdate
- sp_dbmmonitorupdate_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorupdate
- database mirroring [SQL Server], monitoring
ms.assetid: 9ceb9611-4929-44ee-a406-c39ba2720fd5
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0882644bb3cef95694cee44e308b21fc627cd489
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="spdbmmonitorupdate-transact-sql"></a>sp_dbmmonitorupdate (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Atualiza a tabela de status do monitor de espelhamento de banco de dados ao inserir uma nova linha na tabela para cada banco de dados espelho, e trunca linhas anteriores ao período de retenção atual. O período de retenção padrão é de 7 dias (168 horas). Ao atualizar a tabela **sp_dbmmonitorupdate** avalia a métrica de desempenho.  
  
> [!NOTE]  
>  Na primeira vez **sp_dbmmonitorupdate** é executado, ele cria o tabela de status de espelhamento de banco de dados e o **dbm_monitor** função de banco de dados fixa no **msdb** banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dbmmonitorupdate [ database_name ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 O nome do banco de dados para o qual atualizar o status de espelhamento. Se *database_name* não for especificado, o procedimento atualiza a tabela de status para cada banco de dados espelho na instância do servidor.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhuma  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="remarks"></a>Remarks  
 **sp_dbmmonitorupdate** pode ser executado somente no contexto da **msdb** banco de dados.  
  
 Se uma coluna da tabela de status não se aplicar ao papel de um parceiro, o valor será NULL nesse parceiro. Uma coluna também deveria ter um valor NULL se as informações relevantes não estiverem disponíveis, como durante um failover ou reinicialização de servidor.  
  
 Depois de **sp_dbmmonitorupdate** cria o **dbm_monitor** função de banco de dados fixa no **msdb** banco de dados, membros do **sysadmin** função de servidor fixa pode adicionar qualquer usuário para o **dbm_monitor** função fixa de banco de dados. O **dbm_monitor** função permite que seus membros exibir o status de espelhamento de banco de dados, mas não atualizá-lo, mas não exibir ou configurar eventos de espelhamento de banco de dados.  
  
 Ao atualizar o status de espelhamento de banco de dados, **sp_dbmmonitorupdate** inspeciona o último valor de qualquer métrica de desempenho de espelhamento para o qual foi especificado um limite de aviso. Se o valor exceder o limiar, o procedimento adicionará um evento de informação ao log de evento. Todas as taxas são médias desde a última atualização. Para obter mais informações, veja [Usar os limites de aviso e alertas em métricas de desempenho de espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md).  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir atualiza o status de espelhamento apenas para o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE msdb;  
EXEC sp_dbmmonitorupdate AdventureWorks2012 ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangealert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)   
 [sp_dbmmonitorchangemonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitordropalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)   
 [sp_dbmmonitorhelpalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
