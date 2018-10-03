---
title: sp_helpsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_helpsubscription_TSQL
- sp_helpsubscription
helpviewer_keywords:
- sp_helpsubscription
ms.assetid: ff96bcbf-e2b9-4da8-8515-d80d4ce86c16
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 41a23e9885a2d5bd49d074dc72699601eb08a6d9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47850554"
---
# <a name="sphelpsubscription-transact-sql"></a>sp_helpsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Lista informações de assinatura associadas a uma publicação, um artigo, Assinante ou conjunto de assinaturas específico. Esse procedimento armazenado é executado no Publicador, em um banco de dados de publicação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@publication =** ] **'***publicação***'**  
 É o nome da publicação associada. *publicação* está **sysname**, com um padrão de **%**, que retorna todas as informações de assinatura para esse servidor.  
  
 [  **@article=** ] **'***artigo***'**  
 É o nome do artigo. *artigo* está **sysname**, com um padrão de **%**, que retorna todas as informações de assinatura para as publicações e assinantes selecionados. Se **todos os**, apenas uma entrada é retornada para a assinatura completa em uma publicação.  
  
 [  **@subscriber=** ] **'***assinante***'**  
 É o nome do Assinante no qual obter informações de assinaturas. *assinante* está **sysname**, com um padrão de **%**, que retorna todas as informações de assinatura para as publicações e assinantes selecionados.  
  
 [  **@destination_db=** ] **'***destination_db***'**  
 É o nome do banco de dados de destino. *destination_db* está **sysname**, com um padrão de **%**.  
  
 [  **@found=** ] **'***encontrado***'** saída  
 É um sinalizador para indicar linhas de retorno. *encontrado*está **int** e um parâmetro de saída, com um padrão de 23456.  
  
 **1** indica que a publicação foi localizada.  
  
 **0** indica a publicação não foi encontrada.  
  
 [ **@publisher**=] **'***publisher***'**  
 É o nome do Publicador. *Publisher* está **sysname**e assume como padrão o nome do servidor atual.  
  
> [!NOTE]  
>  *publicador* não deve ser especificado, exceto quando ele for um publicador Oracle.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**Assinante**|**sysname**|Nome do Assinante.|  
|**publicação**|**sysname**|Nome da publicação.|  
|**article**|**sysname**|Nome do artigo.|  
|**banco de dados de destino**|**sysname**|Nome do banco de dados de destino no qual os dados replicados são colocados.|  
|**status da assinatura**|**tinyint**|O status da assinatura:<br /><br /> **0** = inativo<br /><br /> **1** = assinado<br /><br /> **2** = ativo|  
|**tipo de sincronização**|**tinyint**|O tipo de sincronização da assinatura:<br /><br /> **1** = automático<br /><br /> **2** = nenhum|  
|**tipo de assinatura**|**int**|O tipo de assinatura:<br /><br /> **0** = push<br /><br /> **1** = pull<br /><br /> **2** = anônimo|  
|**assinatura completa**|**bit**|Se a assinatura é para todos os artigos na publicação:<br /><br /> **0** = Não<br /><br /> **1** = Sim|  
|**nome da assinatura**|**nvarchar(255)**|O nome da assinatura.|  
|**modo de atualização**|**int**|**0** = somente leitura<br /><br /> **1** = assinatura da atualização imediata|  
|**id do trabalho de distribuição**|**binary(16)**|A ID de trabalho do Distribution Agent.|  
|**loopback_detection**|**bit**|A detecção de loopback determina se o Distribution Agent envia transações originadas no Assinante de volta para o Assinante:<br /><br /> **0** = envia de volta.<br /><br /> **1** = não envia de volta.<br /><br /> Usado com replicação transacional bidirecional. Para obter mais informações, consulte [Bidirectional Transactional Replication](../../relational-databases/replication/transactional/bidirectional-transactional-replication.md).|  
|**offload_enabled**|**bit**|Especifica se execução de descarga de um agente de replicação foi definida para executar no Assinante.<br /><br /> Se **0**, agente é executado no publicador.<br /><br /> Se **1**, agente é executado no assinante.|  
|**offload_server**|**sysname**|Nome do servidor habilitado para ativação de agente remota. Se for NULL, então o offload_server atual listado no [MSdistribution_agents](../../relational-databases/system-tables/msdistribution-agents-transact-sql.md) tabela é usada.|  
|**dts_package_name**|**sysname**|Especifica o nome do pacote DTS (Data Transformation Services).|  
|**dts_package_location**|**int**|Local do pacote DTS, se um estiver atribuído à assinatura. Se houver um pacote, um valor de **0** Especifica o local do pacote na **distribuidor**. Um valor de **1** Especifica a **assinante**.|  
|**subscriber_security_mode**|**smallint**|É o modo de segurança no assinante, onde **1** significa que a autenticação do Windows, e **0** significa [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação.|  
|**subscriber_login**|**sysname**|É o nome de logon no Assinante.|  
|**subscriber_password**||A senha do Assinante atual nunca é retornada. O resultado é mascarado por um "**\*\*\*\*\*\***" cadeia de caracteres.|  
|**job_login**|**sysname**|Nome da conta do Windows na qual o Distribution Agent é executado.|  
|**job_password**||A senha de trabalho atual nunca é retornada. O resultado é mascarado por um "**\*\*\*\*\*\***" cadeia de caracteres.|  
|**distrib_agent_name**|**nvarchar(100)**|Nome do trabalho de agente que sincroniza a assinatura.|  
|**subscriber_type**|**tinyint**|Tipo do Assinante, que pode ser um dos seguintes:<br /><br /> **0** = assinante do SQL Server<br /><br /> **1** = servidor de fonte de dados ODBC<br /><br /> **2** = banco de dados Microsoft JET (preterido)<br /><br /> **3** = provedor OLE DB|  
|**subscriber_provider**|**sysname**|PROGID (identificador programático) exclusivo com o qual o provedor OLE DB para fonte de dados não SQL Server é registrado.|  
|**subscriber_datasource**|**nvarchar(4000)**|Nome da fonte de dados conforme entendido pelo provedor OLE DB.|  
|**subscriber_providerstring**|**nvarchar(4000)**|Cadeia de conexão específica de provedor OLE DB que identifica a fonte de dados.|  
|**subscriber_location**|**nvarchar(4000)**|Local do banco de dados conforme entendido pelo provedor OLE DB|  
|**subscriber_catalog**|**sysname**|Catálogo a ser usado ao fazer uma conexão com o provedor OLE DB.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpsubscription** é usado em replicação de instantâneo e transacional.  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução têm como padrão a função **public** . Só são retornadas informações aos usuários sobre assinaturas criadas por eles. Informações sobre todas as assinaturas são retornadas aos membros do **sysadmin** função de servidor fixa no publicador ou membros da **db_owner** função de banco de dados fixa do banco de dados de publicação.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)   
 [sp_changesubstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changesubstatus-transact-sql.md)   
 [sp_dropsubscription &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
