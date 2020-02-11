---
title: sp_marksubscriptionvalidation (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_marksubscriptionvalidation
- sp_marksubscriptionvalidation_TSQL
helpviewer_keywords:
- sp_marksubscriptionvalidation
ms.assetid: e68fe0b9-5993-4880-917a-b0f661f8459b
author: stevestein
ms.author: sstein
ms.openlocfilehash: bb8c38d24fbf6c96c61a7b2e83874d15218797c3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68092670"
---
# <a name="sp_marksubscriptionvalidation-transact-sql"></a>sp_marksubscriptionvalidation (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Marca a transação aberta atual para ser uma transação de validação do nível de assinatura para o assinante especificado. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_marksubscriptionvalidation [ @publication = ] 'publication'  
        , [ @subscriber = ] 'subscriber'  
        , [ @destination_db = ] 'destination_db'  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @subscriber = ] 'subscriber'`É o nome do Assinante. o *assinante* é sysname, sem padrão.  
  
`[ @destination_db = ] 'destination_db'`É o nome do banco de dados de destino. *destination_db* é **sysname**, sem padrão.  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o *Editor* não deve ser usado para uma publicação que pertença [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a um Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_marksubscriptionvalidation** é usado na replicação transacional.  
  
 **sp_marksubscriptionvalidation** não oferece suporte a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assinantes não.  
  
 Para não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicadores, você não pode executar **sp_marksubscriptionvalidation** de dentro de uma transação explícita. Isso porque transações explícitas não têm suporte em conexão de servidor vinculada usada para acessar o Editor.  
  
 **sp_marksubscriptionvalidation** deve ser usado junto com [sp_article_validation &#40;&#41;do Transact-SQL ](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md), especificando um valor de **1** para *subscription_level*e pode ser usado com outras chamadas para **sp_marksubscriptionvalidation** para marcar a transação aberta atual para outros assinantes.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_marksubscriptionvalidation**.  
  
## <a name="example"></a>Exemplo  
 A consulta seguinte pode ser aplicada ao banco de dados de publicação para publicar comandos de validação de nível de assinatura. Esses comandos são retirados pelos Distribution Agents de Assinantes especificados. Observe que a primeira transação valida o artigo '**ART1**', enquanto a segunda transação valida '**ART2**'. Observe também que as chamadas para **sp_marksubscriptionvalidation** e [sp_article_validation &#40;&#41;do Transact-SQL](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) foram encapsuladas em uma transação. Recomendamos apenas uma chamada para [sp_article_validation &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) por transação. Isso ocorre porque [sp_article_validation &#40;&#41;Transact-SQL](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) mantém um bloqueio de tabela compartilhada na tabela de origem durante a transação. A transação deve ser curta para maximizar simultaneidade.  
  
```  
begin tran  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub', @destination_db = 'SubDB'  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub2', @destination_db = 'SubDB'  
  
exec sp_article_validation @publication = 'pub1', @article = 'art1',  
 @rowcount_only = 0, @full_or_fast = 0, @shutdown_agent = 0,  
 @subscription_level = 1  
  
commit tran  
  
begin tran  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub', @destination_db = 'SubDB'  
  
exec sp_marksubscriptionvalidation @publication = 'pub1',  
 @subscriber = 'Sub2', @destination_db = 'SubDB'  
  
exec sp_article_validation @publication = 'pub1', @article = 'art2',  
 @rowcount_only = 0, @full_or_fast = 0, @shutdown_agent = 0,  
 @subscription_level = 1  
  
commit tran  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Validar os dados replicados](../../relational-databases/replication/validate-data-at-the-subscriber.md)  
  
  
