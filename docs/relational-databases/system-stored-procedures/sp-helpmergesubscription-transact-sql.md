---
title: sp_helpmergesubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergesubscription
- sp_helpmergesubscription_TSQL
helpviewer_keywords:
- sp_helpmergesubscription
ms.assetid: da564112-f769-4e67-9251-5699823e8c86
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4643cfc08db68e5369cfca25d2de76d314ffb347
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58530668"
---
# <a name="sphelpmergesubscription-transact-sql"></a>sp_helpmergesubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre uma assinatura para uma publicação de mesclagem, push e pull. Esse procedimento armazenado é executado no Publicador no banco de dados de publicação ou em um Assinante de republicação no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpmergesubscription [ [ @publication=] 'publication']  
    [ , [ @subscriber=] 'subscriber']  
    [ , [ @subscriber_db=] 'subscriber_db']  
    [ , [ @publisher=] 'publisher']  
    [ , [ @publisher_db=] 'publisher_db']  
    [ , [ @subscription_type=] 'subscription_type']  
    [ , [ @found=] 'found' OUTPUT]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação. *publicação* está **sysname**, com um padrão de **%**. A publicação já deve existir e obedecer às regras para identificadores. Se for NULL ou **%**, serão retornadas informações sobre todas as publicações de mesclagem e assinaturas no banco de dados atual.  
  
`[ @subscriber = ] 'subscriber'` É o nome do assinante. *assinante* está **sysname**, com um padrão de **%**. Se for NULL ou %, informações sobre todas as assinaturas da publicação determinada serão retornadas.  
  
`[ @subscriber_db = ] 'subscriber_db'` É o nome do banco de dados de assinatura. *subscriber_db*está **sysname**, com um padrão de **%**, que retorna informações sobre todos os bancos de dados de assinatura.  
  
`[ @publisher = ] 'publisher'` É o nome do publicador. O Publicador deve ser um servidor válido. *Publisher*está **sysname**, com um padrão de **%**, que retorna informações sobre todos os publicadores.  
  
`[ @publisher_db = ] 'publisher_db'` É o nome do banco de dados publicador. *publisher_db*está **sysname**, com um padrão de **%**, que retorna informações sobre todos os bancos de dados do publicador.  
  
`[ @subscription_type = ] 'subscription_type'` É o tipo de assinatura. *subscription_type*está **nvarchar(15)**, e pode ser um destes valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**envio por push** (padrão)|Assinatura push.|  
|**pull**|Assinatura Pull|  
|**ambos**|Assinaturas push e pull|  
  
`[ @found = ] 'found'OUTPUT` É um sinalizador para indicar linhas de retorno. *encontrado*está **int** e um parâmetro de saída, com um padrão NULL. **1** indica que a publicação foi localizada. **0** indica a publicação não foi encontrada.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**subscription_name**|**sysname**|O nome da assinatura.|  
|**publication**|**sysname**|Nome da publicação.|  
|**publisher**|**sysname**|Nome do Publicador.|  
|**publisher_db**|**sysname**|Nome do banco de dados publicador.|  
|**Assinante**|**sysname**|Nome do Assinante.|  
|**subscriber_db**|**sysname**|Nome do banco de dados de assinatura.|  
|**status**|**int**|Status da assinatura:<br /><br /> **0** = todos os trabalhos estão esperando para iniciar<br /><br /> **1** = um ou mais trabalhos estão iniciando<br /><br /> **2** = todos os trabalhos foram executados com êxito<br /><br /> **3** = pelo menos um trabalho está em execução<br /><br /> **4** = todos os trabalhos estão agendados e ociosos<br /><br /> **5** = pelo menos um trabalho está tentando executar após uma falha anterior<br /><br /> **6** = pelo menos um trabalho falhou em executar com êxito|  
|**subscriber_type**|**int**|O tipo de Assinante.|  
|**subscription_type**|**int**|O tipo de assinatura:<br /><br /> **0** = push<br /><br /> **1** = pull<br /><br /> **2** = ambos|  
|**priority**|**float(8)**|Número que indica a prioridade da assinatura.|  
|**sync_type**|**tinyint**|Tipo de sincronização da Assinatura.|  
|**description**|**nvarchar(255)**|Descrição breve da assinatura de mesclagem.|  
|**merge_jobid**|**binary(16)**|ID do trabalho do Merge Agent.|  
|**full_publication**|**tinyint**|Se a assinatura é para uma publicação completa ou filtrada.|  
|**offload_enabled**|**bit**|Especifica se execução de descarga de um agente de replicação foi definida para executar no Assinante. Se for NULL, a execução será executada no Publicador.|  
|**offload_server**|**sysname**|Nome do servidor para onde o agente está executando.|  
|**use_interactive_resolver**|**int**|Retorna se o resolvedor interativo é usado ou não durante a reconciliação. Se **0**, o resolvedor interativo não é usado.|  
|**hostname**|**sysname**|Valor fornecido quando uma assinatura é filtrada pelo valor de [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) função.|  
|**subscriber_security_mode**|**smallint**|É o modo de segurança no assinante, onde **1** significa que a autenticação do Windows, e **0** significa [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.|  
|**subscriber_login**|**sysname**|É o nome de logon no Assinante.|  
|**subscriber_password**|**sysname**|A senha do Assinante atual nunca é retornada. O resultado é mascarado por um "**\*\*\*\*\*\***" cadeia de caracteres.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpmergesubscription** é usado em replicação de mesclagem para retornar informações de assinatura armazenadas no publicador ou assinante de republicação.  
  
 Para assinaturas anônimas, o *subscription_type*valor é sempre **1** (pull). No entanto, você deve executar [sp_helpmergepullsubscription](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md) no assinante para obter informações sobre assinaturas anônimas.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa, o **db_owner** função fixa de banco de dados ou a lista de acesso à publicação da publicação à qual a assinatura pertence pode executar **SP _ helpmergesubscription**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [sp_changemergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [sp_dropmergesubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
