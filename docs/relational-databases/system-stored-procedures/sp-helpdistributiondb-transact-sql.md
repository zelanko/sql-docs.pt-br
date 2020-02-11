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
ms.openlocfilehash: 90dee1076743ae54201248c808b04c6197d42198
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68770931"
---
# <a name="sp_helpdistributiondb-transact-sql"></a>sp_helpdistributiondb (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Retorna as propriedades do banco de dados de distribuição especificado. Esse procedimento armazenado é executado no Distribuidor, no banco de dados de distribuição.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpdistributiondb [ [ @database= ] 'database_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @database = ] 'database_name'`É o nome do banco de dados para o qual as propriedades são retornadas. *database_name* é **sysname**, com um padrão de **%** para todos os bancos de dados associados ao distribuidor e em que o usuário tem permissões.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do banco de dados de distribuição.|  
|**min_distretention**|**int**|Período mínimo de retenção, em horas, antes que as transações sejam excluídas.|  
|**max_distretention**|**int**|Período máximo de retenção, em horas, antes que as transações sejam excluídas.|  
|**history retention**|**int**|Número de horas para retenção de histórico.|  
|**history_cleanup_agent**|**sysname**|Nome do agente de limpeza do histórico.|  
|**distribution_cleanup_agent**|**sysname**|Nome do agente de limpeza da Distribuição.|  
|**Estado**|**int**|Somente para uso interno.|  
|**data_folder**|**nvarchar (255)**|Nome do diretório usado para armazenar os arquivos de banco de dados.|  
|**data_file**|**nvarchar (255)**|Nome do arquivo de banco de dados.|  
|**data_file_size**|**int**|Tamanho de arquivo de dados inicial em megabytes.|  
|**log_folder**|**nvarchar (255)**|Nome do diretório para o arquivo de log de banco de dados.|  
|**log_file**|**nvarchar (255)**|Nome do arquivo de log.|  
|**log_file_size**|**int**|Tamanho de arquivo de log inicial em megabytes.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpdistributiondb** é usado em todos os tipos de replicação.  
  
## <a name="permissions"></a>Permissões  
 Os membros da função de banco de dados fixa **db_owner** ou a função **replmonitor** em um banco de dados de distribuição e os usuários na lista de acesso à publicação de uma publicação usando o banco de dados de distribuição podem executar **sp_helpdistributiondb** para retornar informações relacionadas ao arquivo. Os membros da função **pública** podem executar **sp_helpdistributiondb** para retornar informações não relacionadas a arquivos para bancos de dados de distribuição aos quais eles têm acesso.  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e modificar propriedades de Publicador e Distribuidor](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [&#41;&#40;Transact-SQL de sp_adddistributiondb](../../relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changedistributiondb](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropdistributiondb](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
