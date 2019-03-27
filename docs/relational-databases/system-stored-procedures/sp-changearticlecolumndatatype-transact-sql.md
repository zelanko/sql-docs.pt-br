---
title: sp_changearticlecolumndatatype (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_changearticlecolumndatatype
- sp_changearticlecolumndatatype_TSQL
helpviewer_keywords:
- sp_changearticlecolumndatatype
ms.assetid: 0db80e08-fb77-4d0c-aa41-455b13ffa9b4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 31895afacaee167bccf5144f1ab94e344a36be5f
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58492466"
---
# <a name="spchangearticlecolumndatatype-transact-sql"></a>sp_changearticlecolumndatatype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera o mapeamento de tipo de dados da coluna de artigo para uma publicação Oracle. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
> [!NOTE]  
>  Os mapeamentos de tipo de dados entre os tipos de Editor com suporte são fornecidos por padrão. Use **sp_changearticlecolumndatatype** somente quando substituir essas configurações padrão.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_changearticlecolumndatatype [ @publication= ] 'publication'  
    [ @article = ] 'article'   
    [ @column = ] 'column'  
    [ , [ @type = ] 'type' ]  
    [ , [ @length = ] length ]  
    [ , [ @precision = ] precision ]  
    [ , [ @scale = ] scale ]  
    [ , [ @publisher = ] 'publisher'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação Oracle. *publicação* está **sysname**, sem padrão.  
  
`[ @article = ] 'article'` É o nome do artigo. *artigo* está **sysname**, sem padrão.  
  
`[ @column = ] 'column'` É o nome da coluna para o qual alterar o tipo de dados de mapeamento. *coluna* está **sysname**, sem padrão.  
  
`[ @type = ] 'type'` É o nome da [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados na coluna de destino. *tipo de* está **sysname**, com um padrão NULL.  
  
`[ @length = ] length` É o comprimento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados na coluna de destino. *comprimento* está **bigint**, com um padrão NULL.  
  
`[ @precision = ] precision` É a precisão do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados na coluna de destino. *precisão* está **bigint**, com um padrão NULL.  
  
`[ @publisher = ] 'publisher'` Especifica um não [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] publicador. *Publisher* está **sysname**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **Sp_changearticlecolumndatatype** é usada para substituir os mapeamentos de tipo de dados padrão entre tipos com suporte do publicador (Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Para exibir esses mapeamentos de tipo de dados padrão, execute [sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md).  
  
 **sp_changearticlecolumndatatype** só tem suporte para Publicadores Oracle. A execução desse procedimento armazenado em uma publicação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resulta em um erro.  
  
 **sp_changearticlecolumndatatype** deve ser executado para cada mapeamento de coluna do artigo que deve ser alterado.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_changearticlecolumndatatype**.  
  
## <a name="see-also"></a>Consulte também  
 [Alterar propriedades da publicação e do artigo](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
