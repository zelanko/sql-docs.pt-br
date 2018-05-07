---
title: sp_dbmmonitorchangealert (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorchangealert_TSQL
- sp_dbmmonitorchangealert
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorchangealert
- database mirroring [SQL Server], monitoring
ms.assetid: 1b29f82b-9cf8-4539-8d5c-9a1024db8a50
caps.latest.revision: 42
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8eb29c4aba54f2db1421fcc4de83322c2f37c3d6
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
---
# <a name="spdbmmonitorchangealert-transact-sql"></a>sp_dbmmonitorchangealert (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona ou altera limites de aviso para uma métrica especificada de desempenho de espelhamento.  

  
 
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dbmmonitorchangealert database_name   
    , alert_id   
    , alert_threshold   
    , enabled   
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Especifica o banco de dados ao qual adicionar ou no qual alterar o limite de advertência especificado.  
  
 *alert_id*  
 Um valor inteiro que identifica o aviso a ser adicionado ou alterado. Especifique um dos seguintes valores:  
  
|Value|Métrica de desempenho|Limite de aviso|  
|-----------|------------------------|-----------------------|  
|1|Transação não enviada mais antiga|Especifica o número de minutos de transações que podem ser acumuladas na fila de envio, antes da geração de um aviso na instância do servidor principal. Esse aviso ajuda a medir o potencial de perda de dados em termos de tempo, e é particularmente relevante para o modo de alto desempenho. No entanto, o aviso também é relevante para o modo de segurança alta, quando o espelhamento é pausado ou suspenso devido à desconexão dos parceiros.|  
|2|Log não enviado|Especifica quantos quilobytes (KB) de log não enviado geram um aviso na instância do servidor principal. Esse aviso ajuda a medir o potencial de perda de dados em termos de KB e é particularmente relevante para o modo de alto desempenho. No entanto, o aviso também é relevante para o modo de segurança alta, quando o espelhamento é pausado ou suspenso devido à desconexão dos parceiros.|  
|3|Log não restaurado|Especifica quantos KB de log não restaurado geram um aviso na instância do servidor espelho. Esse aviso ajuda a medir o tempo de failover. *Tempo de failover* consiste, essencialmente, no tempo necessário para que o servidor espelho anterior efetue o roll-forward de quaisquer logs restantes em sua fila de restauração, mais um pequeno tempo adicional.|  
|4|Sobrecarga espelhada confirmada|Especifica o número de milissegundos de atraso médio por transação tolerado, antes que um aviso seja gerado no servidor principal. Esse atraso consiste na quantidade de sobrecarga incidente enquanto a instância do servidor principal aguarda que a instância do servidor espelho grave o registro do log da transação na fila de restauração. Esse valor é relevante somente no modo de alta segurança.|  
|5|Período de retenção|Metadados que controlam quanto tempo as linhas na tabela de status de espelhamento de banco de dados são preservadas.|  
  
 Para obter informações sobre as IDs de eventos que correspondem aos avisos, consulte [Use limites de aviso e alertas em métricas de desempenho de espelhamento &#40;SQL Server&#41;](../../database-engine/database-mirroring/use-warning-thresholds-and-alerts-on-mirroring-performance-metrics-sql-server.md).  
  
 *alert_threshold*  
 O valor do limite para o aviso. Se um valor acima desse limite for retornado quando o status de espelhamento for atualizado, uma entrada será inserida no log de eventos do Windows. Esse valor representa KB, minutos ou milissegundos, dependendo da métrica de desempenho.  
  
> [!NOTE]  
>  Para exibir os valores atuais, execute o [sp_dbmmonitorresults](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md) procedimento armazenado.  
  
 *Habilitado*  
 O aviso está habilitado?  
  
 0 = Aviso está desabilitado.  
  
 1 = Aviso está habilitado.  
  
> [!NOTE]  
>  O período de retenção está sempre habilitado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhuma  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhuma  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir define limites para todas as métricas de desempenho e para o período de retenção do banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]. A tabela a seguir exibe os valores usados no exemplo:  
  
|*alert_id*|Métrica de desempenho|Limite de aviso|O aviso está habilitado?|  
|-----------------|------------------------|-----------------------|-----------------------------|  
|1|Transação não enviada mais antiga|30 minutos|Sim|  
|2|Log não enviado|10.000 KB|Sim|  
|3|Log não restaurado|10.000 KB|Sim|  
|4|Sobrecarga espelhada confirmada|1.000 milissegundos|não|  
|5|Período de retenção|8 horas|Sim|  
  
```  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 1, 30, 1 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 2, 10000, 1 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 3, 10000, 1 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 4, 1000, 0 ;  
EXEC sp_dbmmonitorchangealert AdventureWorks2012, 5, 8, 1 ;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorhelpalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpalert-transact-sql.md)   
 [sp_dbmmonitordropalert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropalert-transact-sql.md)  
  
  
