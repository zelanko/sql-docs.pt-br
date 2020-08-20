---
description: sp_dbmmonitorhelpalert (Transact-SQL)
title: sp_dbmmonitorhelpalert (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorhelpalert_TSQL
- sp_dbmmonitorhelpalert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorhelpalert
- database mirroring [SQL Server], monitoring
ms.assetid: 43911660-b4e4-4934-8c02-35221160aaec
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 942696e1d05ac149780ca226d4a6ba500a3aa11c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489403"
---
# <a name="sp_dbmmonitorhelpalert-transact-sql"></a>sp_dbmmonitorhelpalert (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre limites de aviso em uma ou todas as várias métricas de desempenho do monitor de espelhamento de banco de dados principal.  
 
  ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dbmmonitorhelpalert database_name   
    [ , alert_id ]   
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Especifica o banco de dados.  
  
 [ *alert_id* ]  
 Um valor inteiro que identifica o aviso a ser retornado. Se esse argumento for omitido, todos os avisos serão retornados, mas não o período de retenção.  
  
 Para retornar um aviso específico, especifique um dos valores seguintes:  
  
|Valor|Métrica de desempenho|Limite de aviso|  
|-----------|------------------------|-----------------------|  
|1|Transação não enviada mais antiga|Especifica o número de minutos de transações que podem ser acumuladas na fila de envio, antes da geração de um aviso na instância do servidor principal. Esse aviso ajuda a medir o potencial de perda de dados em termos de tempo, e é particularmente relevante para o modo de alto desempenho. No entanto, o aviso também é relevante para o modo de segurança alta, quando o espelhamento é pausado ou suspenso devido à desconexão dos parceiros.|  
|2|Log não enviado|Especifica quantos quilobytes (KB) de log não enviado geram um aviso na instância do servidor principal. Esse aviso ajuda a medir o potencial de perda de dados em termos de KB e é particularmente relevante para o modo de alto desempenho. No entanto, o aviso também é relevante para o modo de segurança alta, quando o espelhamento é pausado ou suspenso devido à desconexão dos parceiros.|  
|3|Log não restaurado|Especifica quantos KB de log não restaurado geram um aviso na instância do servidor espelho. Esse aviso ajuda a medir o tempo de failover. *Tempo de failover* consiste, essencialmente, no tempo necessário para que o servidor espelho anterior efetue o roll-forward de quaisquer logs restantes em sua fila de restauração, mais um pequeno tempo adicional.|  
|4|Sobrecarga espelhada confirmada|Especifica o número de milissegundos de atraso médio por transação tolerado, antes que um aviso seja gerado no servidor principal. Esse atraso consiste na quantidade de sobrecarga incidente enquanto a instância do servidor principal aguarda que a instância do servidor espelho grave o registro do log da transação na fila de restauração. Esse valor é relevante somente no modo de alta segurança.|  
|5|Período de retenção|Metadados que controlam quanto tempo as linhas na tabela de status de espelhamento de banco de dados são preservadas.|  
  
 Para obter informações sobre as IDs de evento correspondentes aos avisos, consulte [usar limites de aviso e alertas sobre métricas de desempenho de espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Para cada alerta retornado, retorna uma fila que contém as colunas seguintes:  
  
|Coluna|Tipo de dados|Descrição|  
|------------|---------------|-----------------|  
|**alert_id**|**int**|A tabela a seguir lista o valor de **alert_id** para cada métrica de desempenho e a unidade de medida da métrica exibida no conjunto de resultados de **sp_dbmmonitorresults** :|  
|**threshold**|**int**|O valor do limite para o aviso. Se um valor acima desse limite for retornado quando o status de espelhamento for atualizado, uma entrada será inserida no log de eventos do Windows. Esse valor representa KB, minutos ou milissegundos, dependendo do aviso. Se o limite não estiver definido atualmente, o valor será NULL.<br /><br /> **Observação:** Para exibir os valores atuais, execute o procedimento armazenado [sp_dbmmonitorresults](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md) .|  
|**habilitado**|**bit**|0 = Evento desabilitado.<br /><br /> 1 = Evento habilitado.<br /><br /> **Observação:** O período de retenção está sempre habilitado.|  
  
|Valor|Métrica de desempenho|Unidade|  
|-----------|------------------------|----------|  
|1|Transação não enviada mais antiga|minutos|  
|2|Log não enviado|KB|  
|3|Log não restaurado|KB|  
|4|Sobrecarga espelhada confirmada|Milissegundos|  
|5|Período de retenção|Horas|  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna uma linha que indica se um aviso está habilitado para a métrica de desempenho da transação mais antiga não enviada do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
EXEC sp_dbmmonitorhelpalert AdventureWorks2012, 1 ;  
```  
  
 O exemplo a seguir retorna uma linha para cada métrica de desempenho que indica se ela está habilitada no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
```  
EXEC sp_dbmmonitorhelpalert AdventureWorks2012;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitorchangealert ](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitorchangemonitoring ](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitordropalert ](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitorupdate ](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitorhelpmonitoring ](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
