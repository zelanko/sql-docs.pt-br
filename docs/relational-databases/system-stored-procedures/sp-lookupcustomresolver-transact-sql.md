---
title: sp_lookupcustomresolver (Transact-SQL) | Microsoft Docs
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
- sp_lookupcustomresolver_TSQL
- sp_lookupcustomresolver
helpviewer_keywords:
- sp_lookupcustomresolver
ms.assetid: 356a7b8a-ae53-4fb5-86ee-fcfddbf23ddd
caps.latest.revision: 20
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 65770490b7a04efed2a4d7e70a2863fe45d5d453
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="splookupcustomresolver-transact-sql"></a>sp_lookupcustomresolver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna as informações em um valor de manipulador de lógica de negócios ou CLSID (identificador de classe) de um componente resolvedor personalizado com base em COM registrado no Distribuidor. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_lookupcustomresolver [ @article_resolver = ] 'article_resolver'   
    [, [ @resolver_clsid = ] 'resolver_clsid' OUTPUT ]  
    [ , [ @is_dotnet_assembly = ] is_dotnet_assembly OUTPUT ]  
    [ , [ @dotnet_assembly_name = ] 'dotnet_assembly_name' OUTPUT ]  
    [ , [ @dotnet_class_name = ] 'dotnet_class_name' OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@article_resolver =** ] **'***article_resolver***'**  
 Especifica o nome da lógica comercial personalizada cujo registro está sendo cancelado. *article_resolver* é **nvarchar (255)**, sem padrão. Se a lógica corporativa que está sendo removida for um componente COM, então esse parâmetro será o nome amigável do componente. Se a lógica corporativa for um assembly [!INCLUDE[msCoName](../../includes/msconame-md.md)].NET Framework, esse parâmetro será o nome do assembly.  
  
 [ **@resolver_clsid**=] **'***resolver_clsid***'** saída  
 É o valor CLSID do objeto COM associado ao nome da lógica de negócios personalizada especificada no *article_resolver* parâmetro. *resolver_clsid* é **nvarchar (50)**, com um padrão NULL.  
  
 [  **@is_dotnet_assembly=** ] **'***is_dotnet_assembly***'** saída  
 Especifica o tipo da lógica comercial personalizada que está sendo registrada. *is_dotnet_assembly* é **bit**, com um padrão de 0. **1** indica que a lógica de negócios personalizada que está sendo registrada é um manipulador de lógica de negócios Assembly. **0** indica que é um componente COM.  
  
 [  **@dotnet_assembly_name=** ] **'***dotnet_assembly_name***'** saída  
 É o nome do assembly que implementa o manipulador de lógica de negócios. *dotnet_assembly_name* é **nvarchar (255)**, com um valor padrão de NULL.  
  
 [  **@dotnet_class_name=** ] **'***dotnet_class_name***'** saída  
 É o nome da classe que substitui <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> para implementar o manipulador de lógica de negócios. *dotnet_class_name* é **nvarchar (255)**, com um valor padrão de NULL.  
  
 [  **@publisher=** ] **'***publicador***'**  
 É o nome do Publicador. *publicador* é **sysname**, com um valor padrão de NULL. Use este parâmetro quando o procedimento armazenado não é chamado do Publicador. Se não for especificado, será assumido que o servidor local é o Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_lookupcustomresolver** é usado em replicação de mesclagem.  
  
 **sp_lookupcustomresolver** retorna um valor nulo para *resolver_clsid* quando o componente não está registrado na distribuição e um valor de "00000000-0000-0000-0000-000000000000" quando o registro pertence a um Assembly do .NET framework registrado como um manipulador de lógica de negócios.  
  
 **sp_lookupcustomresolver** é chamado pelo [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) e [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) para validar especificado *article_resolver*.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **db_owner** função de banco de dados fixa no banco de dados de publicação pode executar **sp_lookupcustomresolver**.  
  
## <a name="see-also"></a>Consulte também  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Executar lógica de negócios durante sincronizações de mesclagem](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)   
 [Implementar um manipulador de lógica de negócios para um artigo de mesclagem](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [Especificar um resolvedor de artigo de mesclagem](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)   
 [sp_registercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
