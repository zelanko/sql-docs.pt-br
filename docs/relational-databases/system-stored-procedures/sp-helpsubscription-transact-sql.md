---
title: sp_helpsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpsubscription_TSQL
- sp_helpsubscription
helpviewer_keywords:
- sp_helpsubscription
ms.assetid: ff96bcbf-e2b9-4da8-8515-d80d4ce86c16
author: stevestein
ms.author: sstein
ms.openlocfilehash: bf7712ceb55fc368d493be9999cd0b8d4d9f474c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68771567"
---
# <a name="sp_helpsubscription-transact-sql"></a>sp_helpsubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Lista informações de assinatura associadas a uma publicação, um artigo, Assinante ou conjunto de assinaturas específico. Esse procedimento armazenado é executado no Publicador, em um banco de dados de publicação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpsubscription [ [ @publication = ] 'publication' ]   
    [ , [ @article = ] 'article' ]  
    [ , [ @subscriber = ] 'subscriber' ]  
    [ , [ @destination_db = ] 'destination_db' ]   
    [ , [ @found=] found OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação associada. a *publicação* é **sysname**, com um padrão **%** de, que retorna todas as informações de assinatura para este servidor.  
  
`[ @article = ] 'article'`É o nome do artigo. o *artigo* é **sysname**, com um padrão **%** de, que retorna todas as informações de assinatura para as publicações e assinantes selecionados. Se **tudo**, apenas uma entrada será retornada para a assinatura completa em uma publicação.  
  
`[ @subscriber = ] 'subscriber'`É o nome do Assinante no qual obter informações de assinatura. o *assinante* é **sysname**, com um **%** padrão de, que retorna todas as informações de assinatura para as publicações e os artigos selecionados.  
  
`[ @destination_db = ] 'destination_db'`É o nome do banco de dados de destino. *destination_db* é **sysname**, com um padrão de **%**.  
  
`[ @found = ] 'found'OUTPUT`É um sinalizador para indicar linhas de retorno. *encontrado*é **int** e um parâmetro de saída, com um padrão de 23456.  
  
 **1** indica que a publicação foi encontrada.  
  
 **0** indica que a publicação não foi encontrada.  
  
`[ @publisher = ] 'publisher'`É o nome do Publicador. o *Publicador* é **sysname**e usa como padrão o nome do servidor atual.  
  
> [!NOTE]  
>  o *Publicador* não deve ser especificado, exceto quando é um Publicador Oracle.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**Assinante**|**sysname**|Nome do Assinante.|  
|**documento**|**sysname**|Nome da publicação.|  
|**artigo**|**sysname**|Nome do artigo.|  
|**banco de dados de destino**|**sysname**|Nome do banco de dados de destino no qual os dados replicados são colocados.|  
|**status da assinatura**|**tinyint**|O status da assinatura:<br /><br /> **0** = inativo<br /><br /> **1** = assinado<br /><br /> **2** = ativo|  
|**tipo de sincronização**|**tinyint**|O tipo de sincronização da assinatura:<br /><br /> **1** = automático<br /><br /> **2** = nenhum|  
|**tipo de assinatura**|**int**|O tipo de assinatura:<br /><br /> **0** = enviar por push<br /><br /> **1** = pull<br /><br /> **2** = anônimo|  
|**full subscription**|**bit**|Se a assinatura é para todos os artigos na publicação:<br /><br /> **0** = não<br /><br /> **1** = Sim|  
|**nome da assinatura**|**nvarchar (255)**|Nome da assinatura.|  
|**update mode**|**int**|**0** = somente leitura<br /><br /> **1** = atualização imediata-assinatura|  
|**distribution job id**|**Binary (16)**|A ID de trabalho do Distribution Agent.|  
|**loopback_detection**|**bit**|A detecção de loopback determina se o Distribution Agent envia transações originadas no Assinante de volta para o Assinante:<br /><br /> **0** = envia de volta.<br /><br /> **1** = não envia de volta.<br /><br /> Usado com replicação transacional bidirecional. Para obter mais informações, consulte [Bidirectional Transactional Replication](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md).|  
|**offload_enabled**|**bit**|Especifica se execução de descarga de um agente de replicação foi definida para executar no Assinante.<br /><br /> Se for **0**, o agente será executado no Publicador.<br /><br /> Se **1**, o agente será executado no Assinante.|  
|**offload_server**|**sysname**|Nome do servidor habilitado para ativação de agente remota. Se for NULL, a offload_server atual listada na tabela [MSdistribution_agents](../../relational-databases/system-tables/msdistribution-agents-transact-sql.md) será usada.|  
|**dts_package_name**|**sysname**|Especifica o nome do pacote DTS (Data Transformation Services).|  
|**dts_package_location**|**int**|Local do pacote DTS, se um estiver atribuído à assinatura. Se houver um pacote, um valor de **0** especifica o local do pacote no **distribuidor**. Um valor de **1** especifica o **assinante**.|  
|**subscriber_security_mode**|**smallint**|É o modo de segurança no Assinante, em que **1** significa autenticação do Windows e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **0** significa autenticação.|  
|**subscriber_login**|**sysname**|É o nome de logon no Assinante.|  
|**subscriber_password**||A senha do Assinante atual nunca é retornada. O resultado é mascarado por uma cadeia de caracteres "**&#42;&#42;&#42;&#42;&#42;&#42;**".|  
|**job_login**|**sysname**|Nome da conta do Windows na qual o Distribution Agent é executado.|  
|**job_password**||A senha de trabalho atual nunca é retornada. O resultado é mascarado por uma cadeia de caracteres "**&#42;&#42;&#42;&#42;&#42;&#42;**".|  
|**distrib_agent_name**|**nvarchar (100)**|Nome do trabalho de agente que sincroniza a assinatura.|  
|**subscriber_type**|**tinyint**|Tipo do Assinante, que pode ser um dos seguintes:<br /><br /> **0** = assinante SQL Server<br /><br /> **1** = servidor de fonte de dados ODBC<br /><br /> **2** = banco de dados Microsoft Jet (preterido)<br /><br /> **3** = provedor de OLE DB|  
|**subscriber_provider**|**sysname**|PROGID (identificador programático) exclusivo com o qual o provedor OLE DB para fonte de dados não SQL Server é registrado.|  
|**subscriber_datasource**|**nvarchar(4000)**|Nome da fonte de dados conforme entendido pelo provedor OLE DB.|  
|**subscriber_providerstring**|**nvarchar(4000)**|Cadeia de conexão específica de provedor OLE DB que identifica a fonte de dados.|  
|**subscriber_location**|**nvarchar(4000)**|Local do banco de dados conforme entendido pelo provedor OLE DB|  
|**subscriber_catalog**|**sysname**|Catálogo a ser usado ao fazer uma conexão com o provedor OLE DB.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpsubscription** é usado em instantâneo e replicação transacional.  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução assumem como padrão a função **pública** . Só são retornadas informações aos usuários sobre assinaturas criadas por eles. As informações sobre todas as assinaturas são retornadas aos membros da função de servidor fixa **sysadmin** no Publicador ou membros da função de banco de dados fixa **db_owner** no banco de dados de publicação.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_addsubscription](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_changesubstatus](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dropsubscription](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
