---
title: sp_dbmmonitorresults (Transact-SQL) | Microsoft Docs
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
- sp_dbmmonitorresults
- sp_dbmmonitorresults_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorresults
- database mirroring [SQL Server], monitoring
ms.assetid: d575e624-7d30-4eae-b94f-5a7b9fa5427e
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 16061dc41994cd032a9e6124d38abf3acb2e6be5
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33256665"
---
# <a name="spdbmmonitorresults-transact-sql"></a>sp_dbmmonitorresults (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna as linhas de status de um banco de dados monitorado a partir da tabela de status na qual o monitoramento de espelhamento de banco de dados é armazenado e permite selecionar se o procedimento obtém o último status antes.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dbmmonitorresults database_name   
   , rows_to_return  
    , update_status   
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 Especifica qual banco de dados deve retornar o status de espelhamento.  
  
 *rows_to_return*  
 Especifica a quantidade de linhas retornadas:  
  
 0= Última linha  
  
 1 = Linhas das últimas duas horas  
  
 2 = Linhas das últimas quatro horas  
  
 3 = Linhas das últimas oito horas  
  
 4 = Linhas do último dia  
  
 5 = Linhas dos últimos dois dias  
  
 6 = últimas 100 linhas  
  
 7 = 500 última linhas  
  
 8 = última 1.000 linhas  
  
 9 = Últimas 1.000.000 linhas  
  
 *update_status*  
 Especifica que antes de retornar resultados, o procedimento:  
  
 0 = Não atualiza o status do banco de dados. Os resultados são computados utilizando somente as últimas duas linhas, a idade depende de quando a tabela de status foi atualizada.  
  
 1 = atualiza o status do banco de dados chamando **sp_dbmmonitorupdate** antes de calcular os resultados. No entanto, se a tabela de status tenha sido atualizada nos 15 segundos anteriores ou o usuário não é um membro do **sysadmin** função fixa de servidor **sp_dbmmonitorresults** é executado sem atualizar o status.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhuma  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Retorna o número solicitado de linhas de status de histórico do banco de dados especificado. Cada linha contém as seguintes informações:  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|Nome de um banco de dados espelho.|  
|**role**|**Int**|Função de espelhamento atual da instância do servidor:<br /><br /> 1 = Principal<br /><br /> 2 = Espelhamento|  
|**mirroring_state**|**Int**|Estado do banco de dados:<br /><br /> 0 = suspenso<br /><br /> 1 = desconectado<br /><br /> 2 = Sincronização<br /><br /> 3 = Failover pendente<br /><br /> 4 = Sincronizado|  
|**witness_status**|**Int**|O status da conexão da testemunha na sessão de espelhamento de banco de dados pode ser:<br /><br /> 0 = Desconhecido<br /><br /> 1 = conectado<br /><br /> 2 = Desconectado|  
|**log_generation_rate**|**Int**|Quantidade de log gerado desde a atualização anterior do status de espelhamento deste banco de dados em kilobytes/segundo.|  
|**unsent_log**|**Int**|Tamanho de log não enviado na fila de envio do principal em kilobytes.|  
|**send_rate**|**Int**|Taxa de envio de logs do principal para o espelhamento em kilobytes/segundo.|  
|**unrestored_log**|**Int**|Tamanho da fila de restauração do espelhamento em kilobytes.|  
|**recovery_rate**|**Int**|Taxa de restauração do espelhamento em kilobytes/segundo.|  
|**transaction_delay**|**Int**|Atraso total de todas as transações em milissegundos.|  
|**transactions_per_sec**|**Int**|Número de transações que estão ocorrendo por segundo na instância do servidor principal.|  
|**average_delay**|**Int**|Espera média na instância de servidor principal para cada transação devido ao espelhamento de banco de dados. Em modo de alto desempenho (isto é, quando a propriedade SAFETY é definida em OFF), este valor geralmente é 0.|  
|**time_recorded**|**datetime**|Hora em que a linha foi registrada pelo monitor de espelhamento de banco de dados. Essa é a hora do relógio do sistema do principal.|  
|**time_behind**|**datetime**|Hora de relógio do sistema aproximada do principal para o qual o banco de dados espelho é atualmente atualizado. Este valor é significante somente na instância de servidor principal.|  
|**local_time**|**datetime**|Hora de relógio de sistema na instância de servidor local quando esta linha foi atualizada.|  
  
## <a name="remarks"></a>Remarks  
 **sp_dbmmonitorresults** pode ser executado somente no contexto da **msdb** banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Requer a participação no **sysadmin** função de servidor fixa ou o **dbm_monitor** função de banco de dados fixa no **msdb** banco de dados. O **dbm_monitor** função permite que seus membros exibir o status de espelhamento de banco de dados, mas não atualizá-lo, mas não exibir ou configurar eventos de espelhamento de banco de dados.  
  
> [!NOTE]  
>  Na primeira vez que **sp_dbmmonitorupdate** é executado, ele cria o **dbm_monitor** função de banco de dados fixa no **msdb** banco de dados. Membros do **sysadmin** função de servidor fixa pode adicionar qualquer usuário para o **dbm_monitor** função fixa de banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte retorna as linhas registradas durante as duas horas anteriores sem atualizar o status do banco de dados.  
  
```  
USE msdb;  
EXEC sp_dbmmonitorresults AdventureWorks2012, 2, 0;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [sp_dbmmonitorchangemonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [sp_dbmmonitoraddmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)   
 [sp_dbmmonitordropmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)   
 [sp_dbmmonitorhelpmonitoring &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorupdate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)  
  
  
