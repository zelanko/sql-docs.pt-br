---
title: sp_lookupcustomresolver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_lookupcustomresolver_TSQL
- sp_lookupcustomresolver
helpviewer_keywords:
- sp_lookupcustomresolver
ms.assetid: 356a7b8a-ae53-4fb5-86ee-fcfddbf23ddd
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fafdcdd2d0fea423ddf44058e7615aff7241565e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85899375"
---
# <a name="sp_lookupcustomresolver-transact-sql"></a>sp_lookupcustomresolver (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna as informações em um valor de manipulador de lógica de negócios ou CLSID (identificador de classe) de um componente resolvedor personalizado com base em COM registrado no Distribuidor. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
`[ @article_resolver = ] 'article_resolver'`Especifica o nome da lógica de negócios personalizada que está sendo cancelada. *article_resolver* é **nvarchar (255)**, sem padrão. Se a lógica corporativa que está sendo removida for um componente COM, então esse parâmetro será o nome amigável do componente. Se a lógica corporativa for um assembly [!INCLUDE[msCoName](../../includes/msconame-md.md)].NET Framework, esse parâmetro será o nome do assembly.  
  
`[ @resolver_clsid = ] 'resolver_clsid' OUTPUT`É o valor de CLSID do objeto COM associado ao nome da lógica de negócios personalizada especificada no parâmetro *article_resolver* . *resolver_clsid* é **nvarchar (50)**, com um padrão de NULL.  
  
`[ @is_dotnet_assembly = ] 'is_dotnet_assembly' OUTPUT`Especifica o tipo de lógica de negócios personalizada que está sendo registrada. *is_dotnet_assembly* é **bit**, com um padrão de 0. **1** indica que a lógica de negócios personalizada que está sendo registrada é um assembly de manipulador de lógica de negócios; **0** indica que se trata de um componente com.  
  
`[ @dotnet_assembly_name = ] 'dotnet_assembly_name' OUTPUT`É o nome do assembly que implementa o manipulador de lógica de negócios. *dotnet_assembly_name* é **nvarchar (255)**, com um valor padrão de NULL.  
  
`[ @dotnet_class_name = ] 'dotnet_class_name' OUTPUT`É o nome da classe que substitui <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> para implementar o manipulador de lógica de negócios. *dotnet_class_name* é **nvarchar (255)**, com um valor padrão de NULL.  
  
`[ @publisher = ] 'publisher'`É o nome do Publicador. o *Publicador* é **sysname**, com um valor padrão de NULL. Use este parâmetro quando o procedimento armazenado não é chamado do Publicador. Se não for especificado, será assumido que o servidor local é o Publicador.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_lookupcustomresolver** é usado na replicação de mesclagem.  
  
 **sp_lookupcustomresolver** retorna um valor nulo para *resolver_clsid* quando o componente não está registrado na distribuição e um valor de "00000000-0000-0000-0000-000000000000" quando o registro pertence a um assembly .NET Framework registrado como um manipulador de lógica de negócios.  
  
 **sp_lookupcustomresolver** é chamado por [sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) e [sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md) para validar o *article_resolver*especificado.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de banco de dados fixa **db_owner** no banco de dados de publicação podem executar **sp_lookupcustomresolver**.  
  
## <a name="see-also"></a>Consulte Também  
 [Detecção e resolução de conflitos de replicação de mesclagem avançada](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [Executar lógica de negócios durante a sincronização de mesclagem](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)   
 [Implementar um manipulador de lógica de negócios para um artigo de mesclagem](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [Especificar um resolvedor de artigo de mesclagem](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)   
 [&#41;&#40;Transact-SQL de sp_registercustomresolver](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_unregistercustomresolver](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
