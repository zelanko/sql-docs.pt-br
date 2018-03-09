---
title: sp_changearticlecolumndatatype (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_changearticlecolumndatatype
- sp_changearticlecolumndatatype_TSQL
helpviewer_keywords:
- sp_changearticlecolumndatatype
ms.assetid: 0db80e08-fb77-4d0c-aa41-455b13ffa9b4
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1defb009948d01147e4b8f9e333cdd108c8bbba9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spchangearticlecolumndatatype-transact-sql"></a>sp_changearticlecolumndatatype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Altera o mapeamento de tipo de dados da coluna de artigo para uma publicação Oracle. Esse procedimento armazenado é executado no Distribuidor em qualquer banco de dados.  
  
> [!NOTE]  
>  Os mapeamentos de tipo de dados entre os tipos de Editor com suporte são fornecidos por padrão. Use **sp_changearticlecolumndatatype** somente quando substituir essas configurações padrão.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [  **@publication=** ] **'***publicação***'**  
 É o nome da publicação Oracle. *publicação* é **sysname**, sem padrão.  
  
 [  **@article =** ] **'***artigo***'**  
 É o nome do artigo. *artigo* é **sysname**, sem padrão.  
  
 [  **@column** =] **'***coluna***'**  
 É o nome da coluna da qual alterar o mapeamento de tipos de dados. *coluna* é **sysname**, sem padrão.  
  
 [  **@type**  =] **'***tipo***'**  
 É o nome do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados na coluna de destino. *tipo* é **sysname**, com um padrão NULL.  
  
 [  **@length**  =] *comprimento*  
 É o comprimento do tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na coluna de destino. *comprimento* é **bigint**, com um padrão NULL.  
  
 [  **@precision** =] *precisão*  
 É a precisão do tipo de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] na coluna de destino. *precisão* é **bigint**, com um padrão NULL.  
  
 [  **@publisher** =] **'***publicador***'**  
 Especifica um publicador que não é do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. *publicador* é **sysname**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **Sp_changearticlecolumndatatype** é usada para substituir os mapeamentos de tipo de dados padrão entre tipos com suporte do publicador (Oracle e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Para exibir esses mapeamentos de tipo de dados padrão, execute [sp_getdefaultdatatypemapping](../../relational-databases/system-stored-procedures/sp-getdefaultdatatypemapping-transact-sql.md).  
  
 **sp_changearticlecolumndatatype** só tem suporte para editores Oracle. A execução desse procedimento armazenado em uma publicação [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] resulta em um erro.  
  
 **sp_changearticlecolumndatatype** deve ser executado para cada mapeamento de coluna do artigo deve ser alterado.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_changearticlecolumndatatype**.  
  
## <a name="see-also"></a>Consulte também  
 [Alterar propriedades da publicação e do artigo](../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [Data Type Mapping for Oracle Publishers](../../relational-databases/replication/non-sql/data-type-mapping-for-oracle-publishers.md)   
 [Procedimentos armazenados de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
