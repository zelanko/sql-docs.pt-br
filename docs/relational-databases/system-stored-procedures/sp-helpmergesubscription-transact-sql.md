---
description: sp_helpmergesubscription (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 48d40b3209311968443a6c6d2b713b4aa1e3d43a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535183"
---
# <a name="sp_helpmergesubscription-transact-sql"></a>sp_helpmergesubscription (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre uma assinatura para uma publicação de mesclagem, push e pull. Esse procedimento armazenado é executado no Publicador no banco de dados de publicação ou em um Assinante de republicação no banco de dados de assinatura.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publication = ] 'publication'` É o nome da publicação. a *publicação* é **sysname**, com um padrão de **%** . A publicação já deve existir e estar em conformidade com as regras para identificadores. Se for NULL ou **%** , serão retornadas informações sobre todas as publicações de mesclagem e assinaturas no banco de dados atual.  
  
`[ @subscriber = ] 'subscriber'` É o nome do Assinante. o *assinante* é **sysname**, com um padrão de **%** . Se for NULL ou %, informações sobre todas as assinaturas da publicação determinada serão retornadas.  
  
`[ @subscriber_db = ] 'subscriber_db'` É o nome do banco de dados de assinatura. *subscriber_db*é **sysname**, com um padrão de **%** , que retorna informações sobre todos os bancos de dados de assinatura.  
  
`[ @publisher = ] 'publisher'` É o nome do Publicador. O Publicador deve ser um servidor válido. o *Publicador*é **sysname**, com um padrão de **%** , que retorna informações sobre todos os Publicadores.  
  
`[ @publisher_db = ] 'publisher_db'` É o nome do banco de dados do Publicador. *publisher_db*é **sysname**, com um padrão de **%** , que retorna informações sobre todos os bancos de dados do Publicador.  
  
`[ @subscription_type = ] 'subscription_type'` É o tipo de assinatura. *subscription_type*é **nvarchar (15)** e pode ser um desses valores.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**enviar por push** (padrão)|Assinatura push.|  
|**recebimento**|Assinatura pull|  
|**mesmo**|Assinaturas push e pull|  
  
`[ @found = ] 'found'OUTPUT` É um sinalizador para indicar linhas de retorno. *encontrado*é **int** e um parâmetro de saída, com um padrão de NULL. **1** indica que a publicação foi encontrada. **0** indica que a publicação não foi encontrada.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**subscription_name**|**sysname**|O nome da assinatura.|  
|**documento**|**sysname**|Nome da publicação.|  
|**programa**|**sysname**|Nome do Publicador.|  
|**publisher_db**|**sysname**|Nome do banco de dados do Publicador.|  
|**farão**|**sysname**|Nome do Assinante.|  
|**subscriber_db**|**sysname**|Nome do banco de dados de assinatura.|  
|**status**|**int**|Status da assinatura:<br /><br /> **0** = todos os trabalhos estão aguardando para iniciar<br /><br /> **1** = um ou mais trabalhos estão sendo iniciados<br /><br /> **2** = todos os trabalhos foram executados com êxito<br /><br /> **3** = pelo menos um trabalho está em execução<br /><br /> **4** = todos os trabalhos estão agendados e ociosos<br /><br /> **5** = pelo menos um trabalho está tentando ser executado após uma falha anterior<br /><br /> **6** = pelo menos um trabalho falhou ao ser executado com êxito|  
|**subscriber_type**|**int**|O tipo de Assinante.|  
|**subscription_type**|**int**|O tipo de assinatura:<br /><br /> **0** = enviar por push<br /><br /> **1** = pull<br /><br /> **2** = ambos|  
|**priority**|**float (8)**|Número que indica a prioridade da assinatura.|  
|**sync_type**|**tinyint**|Tipo de sincronização da Assinatura.|  
|**descrição**|**nvarchar(255)**|Descrição breve da assinatura de mesclagem.|  
|**merge_jobid**|**binary(16)**|ID do trabalho do Agente de Mesclagem.|  
|**full_publication**|**tinyint**|Se a assinatura é para uma publicação completa ou filtrada.|  
|**offload_enabled**|**bit**|Especifica se execução de descarga de um agente de replicação foi definida para executar no Assinante. Se for NULL, a execução será executada no Publicador.|  
|**offload_server**|**sysname**|Nome do servidor para onde o agente está executando.|  
|**use_interactive_resolver**|**int**|Retorna se o resolvedor interativo é usado ou não durante a reconciliação. Se for **0**, o resolvedor interativo não será usado.|  
|**hostname**|**sysname**|Valor fornecido quando uma assinatura é filtrada pelo valor da função [HOST_NAME](../../t-sql/functions/host-name-transact-sql.md) .|  
|**subscriber_security_mode**|**smallint**|É o modo de segurança no Assinante, em que **1** significa autenticação do Windows e **0** significa [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.|  
|**subscriber_login**|**sysname**|É o nome de logon no Assinante.|  
|**subscriber_password**|**sysname**|A senha do Assinante atual nunca é retornada. O resultado é mascarado por uma **\*\*\*\*\*\*** cadeia de caracteres "".|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpmergesubscription** é usado na replicação de mesclagem para retornar as informações de assinatura armazenadas no Publicador ou no Assinante de republicação.  
  
 Para assinaturas anônimas, o valor de *subscription_type*é sempre **1** (pull). No entanto, você deve executar [sp_helpmergepullsubscription](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md) no Assinante para obter informações sobre assinaturas anônimas.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** , a **db_owner** função de banco de dados fixa ou a lista de acesso à publicação para a publicação à qual a assinatura pertence pode ser executada **sp_helpmergesubscription**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_addmergesubscription ](../../relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changemergesubscription ](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropmergesubscription ](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
