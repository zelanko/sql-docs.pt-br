---
title: sp_dbmmonitorresults (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: e46116111e9f1e85cdaad48e9742e62fba187e74
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "67899172"
---
# <a name="sp_dbmmonitorresults-transact-sql"></a>sp_dbmmonitorresults (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna as linhas de status de um banco de dados monitorado a partir da tabela de status na qual o monitoramento de espelhamento de banco de dados é armazenado e permite selecionar se o procedimento obtém o último status antes.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
  
 7 = últimas 500 linhas  
  
 8 = últimas 1.000 linhas  
  
 9 = Últimas 1.000.000 linhas  
  
 *update_status*  
 Especifica que antes de retornar resultados, o procedimento:  
  
 0 = Não atualiza o status do banco de dados. Os resultados são computados utilizando somente as últimas duas linhas, a idade depende de quando a tabela de status foi atualizada.  
  
 1 = atualiza o status do banco de dados chamando **sp_dbmmonitorupdate** antes de calcular os resultados. No entanto, se a tabela de status tiver sido atualizada nos 15 segundos anteriores ou se o usuário não for membro da função de servidor fixa **sysadmin** , o **sp_dbmmonitorresults** será executado sem Atualizar o status.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Retorna o número solicitado de linhas de status de histórico do banco de dados especificado. Cada linha contém as seguintes informações:  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_name**|**sysname**|Nome de um banco de dados espelho.|  
|**role**|**int**|Função de espelhamento atual da instância do servidor:<br /><br /> 1 = Principal<br /><br /> 2 = Espelhamento|  
|**mirroring_state**|**int**|Estado do banco de dados:<br /><br /> 0 = suspenso<br /><br /> 1 = desconectado<br /><br /> 2 = Sincronização<br /><br /> 3 = Failover pendente<br /><br /> 4 = Sincronizado|  
|**witness_status**|**int**|O status da conexão da testemunha na sessão de espelhamento de banco de dados pode ser:<br /><br /> 0 = Desconhecido<br /><br /> 1 = conectado<br /><br /> 2 = Desconectado|  
|**log_generation_rate**|**int**|Quantidade de log gerado desde a atualização anterior do status de espelhamento deste banco de dados em kilobytes/segundo.|  
|**unsent_log**|**int**|Tamanho de log não enviado na fila de envio do principal em kilobytes.|  
|**send_rate**|**int**|Taxa de envio de logs do principal para o espelhamento em kilobytes/segundo.|  
|**unrestored_log**|**int**|Tamanho da fila de restauração do espelhamento em kilobytes.|  
|**recovery_rate**|**int**|Taxa de restauração do espelhamento em kilobytes/segundo.|  
|**transaction_delay**|**int**|Atraso total de todas as transações em milissegundos.|  
|**transactions_per_sec**|**int**|Número de transações que estão ocorrendo por segundo na instância do servidor principal.|  
|**average_delay**|**int**|Espera média na instância de servidor principal para cada transação devido ao espelhamento de banco de dados. Em modo de alto desempenho (isto é, quando a propriedade SAFETY é definida em OFF), este valor geralmente é 0.|  
|**time_recorded**|**datetime**|Hora em que a linha foi registrada pelo monitor de espelhamento de banco de dados. Essa é a hora do relógio do sistema do principal.|  
|**time_behind**|**datetime**|Hora de relógio do sistema aproximada do principal para o qual o banco de dados espelho é atualmente atualizado. Este valor é significante somente na instância de servidor principal.|  
|**local_time**|**datetime**|Hora de relógio de sistema na instância de servidor local quando esta linha foi atualizada.|  
  
## <a name="remarks"></a>Comentários  
 **sp_dbmmonitorresults** pode ser executado somente no contexto do banco de dados **msdb** .  
  
## <a name="permissions"></a>Permissões  
 Requer a associação na função de servidor fixa **sysadmin** ou na função de banco de dados fixa **dbm_monitor** no banco de dados **msdb** . A função **dbm_monitor** permite que seus membros exibam o status de espelhamento de banco de dados, mas não os atualize, mas não exiba nem configure eventos de espelhamento de banco de dados.  
  
> [!NOTE]  
>  Na primeira vez que **sp_dbmmonitorupdate** é executado, ele cria a função de banco de dados fixa **dbm_monitor** no banco de dados **msdb** . Os membros da função de servidor fixa **sysadmin** podem adicionar qualquer usuário à função de banco de dados fixa **dbm_monitor** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo seguinte retorna as linhas registradas durante as duas horas anteriores sem atualizar o status do banco de dados.  
  
```  
USE msdb;  
EXEC sp_dbmmonitorresults AdventureWorks2012, 2, 0;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitorchangemonitoring](../../relational-databases/system-stored-procedures/sp-dbmmonitorchangemonitoring-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitoraddmonitoring](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitordropmonitoring](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitorhelpmonitoring](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorupdate &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorupdate-transact-sql.md)  
  
  
