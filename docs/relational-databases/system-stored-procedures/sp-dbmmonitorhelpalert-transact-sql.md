---
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4639f548ec75844e72c19cb34ec29fc21933e31a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47851604"
---
# <a name="spdbmmonitorhelpalert-transact-sql"></a>sp_dbmmonitorhelpalert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre limites de aviso em uma ou todas as várias métricas de desempenho do monitor de espelhamento de banco de dados principal.  
 
  ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
  
 Para obter informações sobre as IDs de eventos que correspondem aos avisos, consulte [alertas em métricas de desempenho de espelhamento e os limites de aviso de uso &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md).  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 None  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Para cada alerta retornado, retorna uma fila que contém as colunas seguintes:  
  
|coluna|Data type|Description|  
|------------|---------------|-----------------|  
|**alert_id**|**int**|A tabela abaixo lista os **alert_id** valor para cada métrica de desempenho e a unidade de medida da métrica exibida na **sp_dbmmonitorresults** conjunto de resultados:|  
|**threshold**|**int**|O valor do limite para o aviso. Se um valor acima desse limite for retornado quando o status de espelhamento for atualizado, uma entrada será inserida no log de eventos do Windows. Esse valor representa KB, minutos ou milissegundos, dependendo do aviso. Se o limite não estiver definido atualmente, o valor será NULL.<br /><br /> **Observação:** para exibir os valores atuais, execute o [sp_dbmmonitorresults](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md) procedimento armazenado.|  
|**habilitado**|**bit**|0 = Evento desabilitado.<br /><br /> 1 = Evento habilitado.<br /><br /> **Observação:** período de retenção está sempre habilitado.|  
  
|Valor|Métrica de desempenho|Unidade|  
|-----------|------------------------|----------|  
|1|Transação não enviada mais antiga|Minutes (minutos)|  
|2|Log não enviado|KB|  
|3|Log não restaurado|KB|  
|4|Sobrecarga espelhada confirmada|milissegundos|  
|5|Período de retenção|Hours (horas)|  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangealert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangealert-transact-sql.md)   
 [sp_dbmmonitorchangemonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitordropalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)   
 [sp_dbmmonitorupdate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
