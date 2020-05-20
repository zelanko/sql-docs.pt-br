---
title: sp_addpullsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addpullsubscription
- sp_addpullsubscription_TSQL
helpviewer_keywords:
- sp_addpullsubscription
ms.assetid: 0f4bbedc-0c1c-414a-b82a-6fd47f0a6a7f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c983f72d3ba08f3ffc70991a13e312947ee77378
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820648"
---
# <a name="sp_addpullsubscription-transact-sql"></a>sp_addpullsubscription (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Adiciona uma assinatura pull a um instantâneo ou publicação transacional. Esse procedimento armazenado é executado no Assinante, no banco de dados onde a assinatura pull será criada.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publisher = ] 'publisher'`É o nome do Publicador. o *Publicador* é **sysname**, sem padrão.  
  
`[ @publisher_db = ] 'publisher_db'`É o nome do banco de dados do Publicador. *publisher_db* é **sysname**, com um padrão de NULL. *publisher_db* é ignorado pelos Publicadores Oracle.  
  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @independent_agent = ] 'independent_agent'`Especifica se há um Agente de Distribuição autônomo para esta publicação. *independent_agent* é **nvarchar (5)**, com um padrão de true. Se for **true**, haverá um agente de distribuição autônomo para essa publicação. Se for **false**, há um agente de distribuição para cada par de banco de dados do Publicador/Assinante. *independent_agent* é uma propriedade da publicação e deve ter o mesmo valor aqui que ela tem no Publicador.  
  
`[ @subscription_type = ] 'subscription_type'`É o tipo de assinatura. *subscription_type* é **nvarchar (9)**, com um padrão de **anônimo**. Você deve especificar um valor de **pull** para *subscription_type*, a menos que queira criar uma assinatura sem registrar a assinatura no Publicador. Nesse caso, você deve especificar um valor de **Anonymous**. Isso é necessário em casos nos quais você não pode estabelecer uma conexão [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o Publicador durante configuração da assinatura.  
  
`[ @description = ] 'description'`É a descrição da publicação. a *Descrição* é **nvarchar (100)**, com um padrão de NULL.  
  
`[ @update_mode = ] 'update_mode'`É o tipo de atualização. *update_mode* é **nvarchar (30)** e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**somente leitura** (padrão)|A assinatura é somente leitura. Qualquer alteração no Assinante não será mandada de volta ao Publicador. Deve ser usado quando não são feitas atualizações no Assinante.|  
|**synctran**|Habilita suporte para assinaturas de atualização imediata.|  
|**queued tran**|Habilita a assinatura de atualização enfileirada. As modificações de dados podem ser feitas no Assinante, armazenadas em uma fila e, depois, propagadas ao Publicador.|  
|**pós-falha**|Habilita a assinatura para atualização imediata com atualização enfileirada como um failover. Modificações de dados podem ser feitas no Assinante e propagadas ao Publicador imediatamente. Se o Publicador e o Assinante não estiverem conectados, as modificações de dados feitas no Assinante poderão ser armazenadas em uma fila até que o Assinante e o Publicador sejam reconectados.|  
|**queued failover**|Habilita a assinatura como uma assinatura de atualização enfileirada com a capacidade de alterar para o modo de atualização imediata. Modificações de dados podem ser feitas no Assinante e armazenadas em uma fila até que a conexão seja estabelecida entre o Assinante e o Publicador. Quando uma conexão contínua é estabelecida, o modo de atualização pode ser alterado para atualização imediata. *Não há suporte para Publicadores Oracle*.|  
  
`[ @immediate_sync = ] immediate_sync`É se os arquivos de sincronização são criados ou recriados sempre que o Agente de Instantâneo é executado. *immediate_sync* é **bit** com um padrão de 1 e deve ser definido com o mesmo valor que *immediate_sync* em **sp_addpublication**. *immediate_sync* é uma propriedade da publicação e deve ter o mesmo valor aqui que ela tem no Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_addpullsubscription** é usado na replicação de instantâneo e na replicação transacional.  
  
> [!IMPORTANT]  
>  Para assinaturas de atualização enfileiradas, use Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conexões com Assinantes, e especifique uma conta diferente para conexão com cada assinante. Ao criar uma assinatura pull que oferece suporte a atualização em fila, a replicação sempre define a conexão para usar a Autenticação do Windows (em assinaturas pull, a replicação não pode acessar metadados em Assinante com Autenticação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Nesse caso, você deve executar [sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md) para alterar a conexão para usar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] autenticação depois que a assinatura for configurada.  
  
 Se o [MSreplication_subscriptions &#40;tabela&#41;Transact-SQL](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) não existir no Assinante, o **sp_addpullsubscription** o criará. Ele também adiciona uma linha ao [MSreplication_subscriptions &#40;tabela&#41;Transact-SQL](../../relational-databases/system-tables/msreplication-subscriptions-transact-sql.md) . Para assinaturas pull, [sp_addsubscription &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) deve ser chamado primeiro no Publicador.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_addtranpullsubscriptionagent](../../relational-databases/replication/codesnippet/tsql/sp-addpullsubscription-t_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_addpullsubscription**.  
  
## <a name="see-also"></a>Consulte Também  
 [Create a Pull Subscription](../../relational-databases/replication/create-a-pull-subscription.md)   
 [Criar uma assinatura atualizável para uma publicação transacional](../../relational-databases/replication/publish/create-an-updatable-subscription-to-a-transactional-publication.md) [assinar publicações](../../relational-databases/replication/subscribe-to-publications.md)   
 [&#41;&#40;Transact-SQL de sp_addpullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_change_subscription_properties](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_droppullsubscription](../../relational-databases/system-stored-procedures/sp-droppullsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helppullsubscription](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_helpsubscription_properties](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
