---
title: sp_helpdistributiondb (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpdistributiondb_TSQL
- sp_helpdistributiondb
helpviewer_keywords:
- sp_helpdistributiondb
ms.assetid: a2917020-26d1-4011-99f8-9212d120fd2d
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2c97fec403da1913f7f39f1da706d107cd964aa4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67902924"
---
# <a name="sphelpdistributiondb-transact-sql"></a>sp_helpdistributiondb (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna as propriedades do banco de dados de distribuição especificado. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpdistributiondb [ [ @database= ] 'database_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @database = ] 'database_name'` É o nome do banco de dados para o qual as propriedades são retornadas. *Database_Name* está **sysname**, com um padrão de **%** para todos os bancos de dados associados ao distribuidor e no qual o usuário tem permissões.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do banco de dados de distribuição.|  
|**min_distretention**|**int**|Período mínimo de retenção, em horas, antes que as transações sejam excluídas.|  
|**max_distretention**|**int**|Período máximo de retenção, em horas, antes que as transações sejam excluídas.|  
|**retenção de histórico**|**int**|Número de horas para retenção de histórico.|  
|**history_cleanup_agent**|**sysname**|Nome do agente de limpeza do histórico.|  
|**distribution_cleanup_agent**|**sysname**|Nome do agente de limpeza da Distribuição.|  
|**status**|**int**|Somente para uso interno.|  
|**data_folder**|**nvarchar(255)**|Nome do diretório usado para armazenar os arquivos de banco de dados.|  
|**data_file**|**nvarchar(255)**|Nome do arquivo de banco de dados.|  
|**data_file_size**|**int**|Tamanho de arquivo de dados inicial em megabytes.|  
|**log_folder**|**nvarchar(255)**|Nome do diretório para o arquivo de log de banco de dados.|  
|**log_file**|**nvarchar(255)**|Nome do arquivo de log.|  
|**log_file_size**|**int**|Tamanho de arquivo de log inicial em megabytes.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpdistributiondb** é usado em todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Os membros a **db_owner** função de banco de dados fixa ou o **replmonitor** função em um banco de dados de distribuição e os usuários na lista de acesso da publicação de uma publicação usando o banco de dados de distribuição podem executar **sp_helpdistributiondb** para retornar informações relacionadas ao arquivo. Os membros de **pública** podem executar **sp_helpdistributiondb** para retornar informações relacionadas ao arquivo para bancos de dados de distribuição aos quais têm acesso.  
  
## <a name="see-also"></a>Consulte também  
 [Exibir e modificar propriedades de Publicador e Distribuidor](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_adddistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [sp_changedistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [sp_dropdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
