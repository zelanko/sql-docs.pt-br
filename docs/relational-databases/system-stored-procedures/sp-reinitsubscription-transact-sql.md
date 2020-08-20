---
description: sp_reinitsubscription (Transact-SQL)
title: sp_reinitsubscription (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_reinitsubscription
- sp_reinitsubscription_TSQL
helpviewer_keywords:
- sp_reinitsubscription
ms.assetid: d56ae218-6128-4ff9-b06c-749914505c7b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: b6aad3d76fca41075bd022eac703ce7d1a112bc1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464035"
---
# <a name="sp_reinitsubscription-transact-sql"></a>sp_reinitsubscription (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Marca a assinatura para reinicialização. Esse procedimento armazenado é executado no Publicador para assinaturas push.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @publication = ] 'publication'` É o nome da publicação. a *publicação* é **sysname**, com um padrão de todos.  
  
`[ @article = ] 'article'` É o nome do artigo. o *artigo* é **sysname**, com um padrão de todos. Para uma publicação de atualização imediata, o *artigo* deve ser **tudo**; caso contrário, o procedimento armazenado ignora a publicação e relata um erro.  
  
`[ @subscriber = ] 'subscriber'` É o nome do Assinante. o *assinante* é **sysname**, sem padrão.  
  
`[ @destination_db = ] 'destination_db'` É o nome do banco de dados de destino. *destination_db* é **sysname**, com um padrão de todos.  
  
`[ @for_schema_change = ] 'for_schema_change'` Indica se a reinicialização ocorre como resultado de uma alteração de esquema no banco de dados de publicação. *for_schema_change* é **bit**, com um padrão de 0. Se **0**, as assinaturas ativas para publicações que permitem atualização imediata são reativadas desde que toda a publicação e não apenas alguns de seus artigos sejam reinicializadas. Isso significa que a reinicialização está ocorrendo como resultado de alterações de esquema. Se **1**, as assinaturas ativas não serão reativadas até que o agente de instantâneo seja executado.  
  
`[ @publisher = ] 'publisher'` Especifica um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Publicador* não deve ser usado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores.  
  
`[ @ignore_distributor_failure = ] ignore_distributor_failure` Permite a reinicialização, mesmo que o distribuidor não exista ou esteja offline. *ignore_distributor_failure* é **bit**, com um padrão de 0. Se **0**, a reinicialização falhará se o distribuidor não existir ou estiver offline.  
  
`[ @invalidate_snapshot = ] invalidate_snapshot` Invalida o instantâneo de publicação existente. *invalidate_snapshot* é **bit**, com um padrão de 0. Se for **1**, um novo instantâneo será gerado para a publicação.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_reinitsubscription** é usado na replicação transacional.  
  
 Não há suporte para **sp_reinitsubscription** para replicação transacional ponto a ponto.  
  
 Para assinaturas onde o instantâneo inicial é aplicado automaticamente e onde a publicação não permite assinaturas atualizáveis, o Agente de Instantâneo deve ser executado depois que esse procedimento armazenado é executado para que o esquema e os arquivos de programa de cópia em massa sejam preparados e o Agente de Distribuição possa então sincronizar novamente as assinaturas.  
  
 Para assinaturas onde o instantâneo inicial é aplicado automaticamente e onde a publicação permite assinaturas atualizáveis, o Agente de Distribuição sincroniza novamente as assinaturas usando o esquema e os arquivos de programa de cópia em massa mais recentes anteriormente criados pelo Agente de Instantâneo. O Agente de Distribuição ressincroniza a assinatura imediatamente após o usuário executar **sp_reinitsubscription**, se a agente de distribuição não estiver ocupada; caso contrário, a sincronização pode ocorrer após o intervalo de mensagem (especificado pelo Agente de Distribuição parâmetro de prompt de comando: **MessageInterval**).  
  
 **sp_reinitsubscription** não tem nenhum efeito nas assinaturas em que o instantâneo inicial é aplicado manualmente.  
  
 Para ressincronizar assinaturas anônimas em uma publicação, passe **todos** ou nulo como *assinante*.  
  
 A replicação Transacional dá suporte à reinicialização de assinatura no nível do artigo. O instantâneo do artigo é reaplicado no Assinante durante a próxima sincronização, depois que o artigo é marcado para reinicialização. No entanto, se houver artigos dependentes também assinados pelo mesmo Assinante, a reaplicação do instantâneo no artigo poderá falhar, a menos que os artigos dependentes na publicação sejam também automaticamente reiniciados em certas circunstâncias.  
  
-   Se o comando de pré-criação do artigo for descartado, artigos de exibições associadas a esquema e procedimentos armazenados associados a esquema no objeto base daquele artigo serão também marcados para reinicialização.  
  
-   Se a opção de esquema no artigo incluir geração de script para integridade referencial declarada de chaves primárias, artigos que têm tabelas base com relações de chave estrangeira com as tabelas base do artigo reiniciado também serão marcados para reinicialização.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_reinittranpushsub](../../relational-databases/replication/codesnippet/tsql/sp-reinitsubscription-tr_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** , os membros da função de banco de dados fixa **db_owner** ou o criador da assinatura podem executar **sp_reinitsubscription**.  
  
## <a name="see-also"></a>Consulte Também  
 [Reinicializar uma assinatura](../../relational-databases/replication/reinitialize-a-subscription.md)   
 [Reinicializar as assinaturas](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
