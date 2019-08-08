---
title: sp_droparticle (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_droparticle_TSQL
- sp_droparticle
helpviewer_keywords:
- sp_droparticle
ms.assetid: 09fec594-53f4-48a5-8edb-c50731c7adb2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 882c57c552d9666ec3ef308f63a6c5058c21e8e2
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68768927"
---
# <a name="sp_droparticle-transact-sql"></a>sp_droparticle (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Descarta um artigo de uma publicação de instantâneo ou transacional. Um artigo não poderá ser removido se tiver uma ou mais assinaturas associadas. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_droparticle [ @publication= ] 'publication'  
        , [ @article= ] 'article'  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @from_drop_publication = ] from_drop_publication ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação que contém o artigo a ser Descartado. a *publicação* é **sysname**, sem padrão.  
  
`[ @article = ] 'article'`É o nome do artigo a ser removido. o *artigo* é **sysname**, sem padrão.  
  
`[ @ignore_distributor = ] ignore_distributor` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot`O reconhece que a ação executada por esse procedimento armazenado pode invalidar um instantâneo existente. *force_invalidate_snapshot* é um **bit**, com um padrão de **0**.  
  
 **0** especifica que as alterações no artigo não fazem com que o instantâneo seja inválido. Se o procedimento armazenado detectar que a alteração requer um novo instantâneo, ocorrerá um erro e nenhuma alteração será feita.  
  
 **1** especifica que as alterações no artigo podem fazer com que o instantâneo seja inválido e, se houver assinaturas existentes que exijam um novo instantâneo, concederá permissão para o instantâneo existente ser marcado como obsoleto e um novo instantâneo gerado.  
  
`[ @publisher = ] 'publisher'`Especifica um não [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicador. o Publicador é **sysname**, com um padrão de NULL.  
  
> [!NOTE]  
>  o Publicador não deve ser usado ao alterar as propriedades [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] do artigo em um Publicador.  
  
`[ @from_drop_publication = ] from_drop_publication` [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_droparticle** é usado em instantâneo e replicação transacional.  
  
 Para artigos filtrados horizontalmente, **sp_droparticle** verifica a coluna **tipo** do artigo na tabela [Transact &#40;&#41; -SQL sysarticles](../../relational-databases/system-tables/sysarticles-transact-sql.md) para determinar se um modo de exibição ou filtro também deve ser Descartado. Se uma exibição ou filtro foram gerados automaticamente, serão descartados com o artigo. Se foram criados manualmente, não serão descartados.  
  
 A execução de **sp_droparticle** para descartar um artigo de uma publicação não remove o objeto do banco de dados de publicação ou o objeto correspondente do banco de dados de assinatura. Use `DROP <object>` para remover esses objetos manualmente, se necessário.  
  
## <a name="example"></a>Exemplo  
 [!code-sql[HowTo#sp_droparticle](../../relational-databases/replication/codesnippet/tsql/sp-droparticle-transact-_1.sql)]  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou da função de banco de dados fixa **db_owner** podem executar **sp_droparticle**.  
  
## <a name="see-also"></a>Consulte também  
 [Excluir um artigo](../../relational-databases/replication/publish/delete-an-article.md)   
 [Adicionar e remover artigos de publicações existentes](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [sp_addarticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_helparticle &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
