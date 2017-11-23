---
title: sp_addpullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_addpullsubscription
- sp_addpullsubscription_TSQL
helpviewer_keywords: sp_addpullsubscription
ms.assetid: 0f4bbedc-0c1c-414a-b82a-6fd47f0a6a7f
caps.latest.revision: "44"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4b6c772cc91d922ceb8acd5c205c9b19dc67d50d
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spaddpullsubscription-transact-sql"></a>sp_addpullsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Adiciona uma assinatura pull a um instantâneo ou publicação transacional. Esse procedimento armazenado é executado no Assinante, no banco de dados onde a assinatura pull será criada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_addpullsubscription [ @publisher= ] 'publisher'  
    [ , [ @publisher_db= ] 'publisher_db' ]  
        , [ @publication= ] 'publication'  
    [ , [ @independent_agent= ] 'independent_agent' ]  
    [ , [ @subscription_type= ] 'subscription_type' ]  
    [ , [ @description= ] 'description' ]  
    [ , [ @update_mode= ] 'update_mode' ]  
    [ , [ @immediate_sync = ] immediate_sync ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publisher=**] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, sem padrão.  
  
 [  **@publisher_db=**] **'***publisher_db***'**  
 É o nome do banco de dados Publicador. *publisher_db* é **sysname**, com um padrão NULL. *publisher_db* é ignorado por Publicadores Oracle.  
  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
 [  **@independent_agent=**] **'***independent_agent***'**  
 Especifica se existe um Agente de Distribuição autônomo para esta publicação. *independent_agent* é **nvarchar (5)**, com um padrão de TRUE. Se **true**, há um Distribution Agent autônomo para essa publicação. Se **false**, há um agente de distribuição para cada par de banco de dados de assinante/banco de dados do publicador. *independent_agent* é uma propriedade da publicação e deve ter o mesmo valor aqui, que tem no publicador.  
  
 [  **@subscription_type=**] **'***subscription_type***'**  
 É o tipo de assinatura. *subscription_type* é **nvarchar(9)**, com um padrão de **anônimo**. Você deve especificar um valor de **pull** para *subscription_type*, a menos que você deseja criar uma assinatura sem registrar a assinatura no publicador. Nesse caso, você deve especificar um valor de **anônimo**. Isso é necessário em casos nos quais você não pode estabelecer uma [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conexão com o publicador durante a configuração de assinatura.  
  
 [  **@description=**] **'***descrição***'**  
 É a descrição da publicação. *Descrição* é **nvarchar (100)**, com um padrão NULL.  
  
 [  **@update_mode=**] **'***update_mode***'**  
 É o tipo de atualização. *update_mode* é **nvarchar (30)**, e pode ser um dos valores a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|**somente leitura** (padrão)|A assinatura é somente leitura. Qualquer alteração no Assinante não será mandada de volta ao Publicador. Deve ser usado quando não são feitas atualizações no Assinante.|  
|**Synctran**|Habilita suporte para assinaturas de atualização imediata.|  
|**em fila tran**|Habilita a assinatura de atualização enfileirada. As modificações de dados podem ser feitas no Assinante, armazenadas em uma fila e, depois, propagadas ao Publicador.|  
|**failover**|Habilita a assinatura para atualização imediata com atualização enfileirada como um failover. Modificações de dados podem ser feitas no Assinante e propagadas ao Publicador imediatamente. Se o Publicador e o Assinante não estiverem conectados, as modificações de dados feitas no Assinante poderão ser armazenadas em uma fila até que o Assinante e o Publicador sejam reconectados.|  
|**failover em fila**|Habilita a assinatura como uma assinatura de atualização enfileirada com a capacidade de alterar para o modo de atualização imediata. Modificações de dados podem ser feitas no Assinante e armazenadas em uma fila até que a conexão seja estabelecida entre o Assinante e o Publicador. Quando uma conexão contínua é estabelecida, o modo de atualização pode ser alterado para atualização imediata. *Não há suportada para editores Oracle*.|  
  
 [  **@immediate_sync =**] *immediate_sync*  
 Especifica se os arquivos de sincronização serão criados ou recriados em cada execução do Agente de Instantâneo. *immediate_sync* é **bit** com um padrão de 1 e deve ser definido com o mesmo valor como *immediate_sync* na **sp_addpublication**. *immediate_sync* é uma propriedade da publicação e deve ter o mesmo valor aqui, que tem no publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addpullsubscription** é usado em replicação de instantâneo e replicação transacional.  
  
> [!IMPORTANT]  
>  Para assinaturas de atualização enfileiradas, use Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conexões com Assinantes, e especifique uma conta diferente para conexão com cada assinante. Ao criar uma assinatura pull que oferece suporte a atualização em fila, a replicação sempre define a conexão para usar a Autenticação do Windows (em assinaturas pull, a replicação não pode acessar metadados em Assinante com Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Nesse caso, você deve executar [sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md) para alterar a conexão para usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação depois que a assinatura está configurada.  
  
 Se o [MSreplication_subscriptions &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) tabela não existe no assinante, **sp_addpullsubscription** cria. Ele também adiciona uma linha para o [MSreplication_subscriptions &#40; Transact-SQL &#41; ](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) tabela. Para assinaturas pull, [sp_addsubscription &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) deve ser chamado no publicador pela primeira vez.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addpullsubscription-t_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_addpullsubscription**.  
  
## <a name="see-also"></a>Consulte também  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Criar uma assinatura atualizável para uma publicação transacional](../../relational-databases/replication/publish/create-updatable-subscription-to-transactional-publication.md) [assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)   
 [sp_addpullsubscription_agent &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [sp_change_subscription_properties &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [sp_droppullsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [sp_helppullsubscription &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [sp_helpsubscription_properties &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
