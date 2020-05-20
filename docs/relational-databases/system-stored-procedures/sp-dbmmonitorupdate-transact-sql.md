---
title: sp_dbmmonitorupdate (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8f847881fa57735a09945d47d446949db3443b3e
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826148"
---
# <a name="sp_dbmmonitorupdate-transact-sql"></a>sp_dbmmonitorupdate (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Atualiza a tabela de status do monitor de espelhamento de banco de dados ao inserir uma nova linha na tabela para cada banco de dados espelho, e trunca linhas anteriores ao período de retenção atual. O período de retenção padrão é de 7 dias (168 horas). Ao atualizar a tabela, **sp_dbmmonitorupdate** avalia as métricas de desempenho.  
  
> [!NOTE]  
>  Na primeira vez que o **sp_dbmmonitorupdate** é executado, ele cria a tabela de status de espelhamento de banco de dados e a função de banco de dados fixa **dbm_monitor** no banco de dados **msdb** .  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dbmmonitorupdate [ database_name ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 O nome do banco de dados para o qual atualizar o status de espelhamento. Se *database_name* não for especificado, o procedimento atualizará a tabela de status para cada banco de dados espelhado na instância do servidor.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Não  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 **sp_dbmmonitorupdate** pode ser executado somente no contexto do banco de dados **msdb** .  
  
 Se uma coluna da tabela de status não se aplicar ao papel de um parceiro, o valor será NULL nesse parceiro. Uma coluna também deveria ter um valor NULL se as informações relevantes não estiverem disponíveis, como durante um failover ou reinicialização de servidor.  
  
 Depois que **sp_dbmmonitorupdate** cria a função de banco de dados fixa **dbm_monitor** no banco de dados **msdb** , os membros da função de servidor fixa **sysadmin** podem adicionar qualquer usuário à função de banco de dados fixa **dbm_monitor** . A função **dbm_monitor** permite que seus membros exibam o status de espelhamento de banco de dados, mas não os atualize, mas não exiba nem configure eventos de espelhamento de banco de dados.  
  
 Ao atualizar o status de espelhamento de um banco de dados, **sp_dbmmonitorupdate** inspeciona o valor mais recente de qualquer métrica de desempenho de espelhamento para a qual um limite de aviso foi especificado. Se o valor exceder o limiar, o procedimento adicionará um evento de informação ao log de evento. Todas as taxas são médias desde a última atualização. Para obter mais informações, veja [Usar os limites de aviso e alertas em métricas de desempenho de espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md).  
  
## <a name="permissions"></a>Permissões  
 Requer a associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir atualiza o status de espelhamento apenas para o banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
USE msdb;  
EXEC sp_dbmmonitorupdate AdventureWorks2012 ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitorchangealert](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitorchangemonitoring](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitordropalert](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitorhelpalert](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitorhelpmonitoring](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
