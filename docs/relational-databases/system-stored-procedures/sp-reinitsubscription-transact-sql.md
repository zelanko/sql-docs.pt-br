---
title: sp_reinitsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_reinitsubscription
- sp_reinitsubscription_TSQL
helpviewer_keywords:
- sp_reinitsubscription
ms.assetid: d56ae218-6128-4ff9-b06c-749914505c7b
caps.latest.revision: 32
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 233448ed17ee55bb2d2c1c2b0a906191c73d4cf6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33000683"
---
# <a name="spreinitsubscription-transact-sql"></a>sp_reinitsubscription (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Marca a assinatura para reinicialização. Esse procedimento armazenado é executado no Publicador para assinaturas push.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_reinitsubscription [ [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
        , [ @subscriber = ] 'subscriber'  
    [ , [ @destination_db = ] 'destination_db']  
    [ , [ @for_schema_change = ] 'for_schema_change']  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @ignore_distributor_failure = ] ignore_distributor_failure ]   
    [ , [ @invalidate_snapshot = ] invalidate_snapshot ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, com um padrão de all.  
  
 [  **@article=**] **'***artigo***'**  
 É o nome do artigo. *artigo* é **sysname**, com um padrão de all. Para uma publicação de atualização imediata, *artigo* devem ser **todos os**; caso contrário, o procedimento armazenado ignora a publicação e relata um erro.  
  
 [  **@subscriber=**] **'***assinante***'**  
 É o nome do Assinante. *assinante* é **sysname**, sem padrão.  
  
 [  **@destination_db=**] **'***destination_db***'**  
 É o nome do banco de dados de destino. *destination_db* é **sysname**, com um padrão de all.  
  
 [  **@for_schema_change=**] **'***for_schema_change***'**  
 Indica se a reinicialização ocorre como resultado de uma alteração de esquema no banco de dados de publicação. *for_schema_change* é **bit**, com um padrão de 0. Se **0**, assinaturas ativas para publicações que permitem atualização imediata serão reativadas quando toda a publicação e não apenas alguns de seus artigos sejam reinicializados. Isso significa que a reinicialização está ocorrendo como resultado de alterações de esquema. Se **1**, assinaturas ativas não serão reativadas até que o Snapshot Agent é executado.  
  
 [  **@publisher=** ] **'***publicador***'**  
 Especifica um publicador que não é do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publicador* é **sysname**, com um padrão NULL.  
  
> [!NOTE]  
>  *publicador* não deve ser usado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] editores.  
  
 [  **@ignore_distributor_failure=** ] *ignore_distributor_failure*  
 Permite a reinicialização mesmo que o Distribuidor não exista ou esteja offline. *ignore_distributor_failure* é **bit**, com um padrão de 0. Se **0**, reinicialização falhará se o distribuidor não existe ou está offline.  
  
 [  **@invalidate_snapshot=** ] *invalidate_snapshot*  
 Invalida o instantâneo da publicação existente. *invalidate_snapshot* é **bit**, com um padrão de 0. Se **1**, um novo instantâneo é gerado para a publicação.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_reinitsubscription** é usado em replicação transacional.  
  
 **sp_reinitsubscription** não há suporte para replicação transacional ponto a ponto.  
  
 Para assinaturas onde o instantâneo inicial é aplicado automaticamente e onde a publicação não permite assinaturas atualizáveis, o Agente de Instantâneo deve ser executado depois que esse procedimento armazenado é executado para que o esquema e os arquivos de programa de cópia em massa sejam preparados e o Agente de Distribuição possa então sincronizar novamente as assinaturas.  
  
 Para assinaturas onde o instantâneo inicial é aplicado automaticamente e onde a publicação permite assinaturas atualizáveis, o Agente de Distribuição sincroniza novamente as assinaturas usando o esquema e os arquivos de programa de cópia em massa mais recentes anteriormente criados pelo Agente de Instantâneo. O agente de distribuição sincroniza novamente as assinaturas imediatamente depois que o usuário executa **sp_reinitsubscription**, se o agente de distribuição não estiver ocupado; caso contrário, sincronização pode ocorrer depois de (intervalo de mensagem especificado pelo parâmetro de prompt de comando do agente de distribuição: **MessageInterval**).  
  
 **sp_reinitsubscription** não tem nenhum efeito em assinaturas onde o instantâneo inicial é aplicado manualmente.  
  
 Para sincronizar novamente assinaturas anônimas para uma publicação, passe **todos os** ou NULL como *assinante*.  
  
 A replicação Transacional dá suporte à reinicialização de assinatura no nível do artigo. O instantâneo do artigo é reaplicado no Assinante durante a próxima sincronização, depois que o artigo é marcado para reinicialização. No entanto, se houver artigos dependentes também assinados pelo mesmo Assinante, a reaplicação do instantâneo no artigo poderá falhar, a menos que os artigos dependentes na publicação sejam também automaticamente reiniciados em certas circunstâncias.  
  
-   Se o comando de pré-criação do artigo for descartado, artigos de exibições associadas a esquema e procedimentos armazenados associados a esquema no objeto base daquele artigo serão também marcados para reinicialização.  
  
-   Se a opção de esquema no artigo incluir geração de script para integridade referencial declarada de chaves primárias, artigos que têm tabelas base com relações de chave estrangeira com as tabelas base do artigo reiniciado também serão marcados para reinicialização.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_reinittranpushsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitsubscription-tr_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa, membros do **db_owner** função fixa de banco de dados ou o criador da assinatura pode executar **sp_reinitsubscription** .  
  
## <a name="see-also"></a>Consulte também  
 [Reinicializar uma assinatura](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [Reinicializar as assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
