---
title: sp_register_custom_scripting (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_register_custom_scripting
- sp_register_custom_scripting_TSQL
helpviewer_keywords:
- sp_register_custom_scripting
ms.assetid: a8159282-de3b-4b9e-bdc9-3d3fce485c7f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: af2feda317d3cbcbf7391179c0797291644eca26
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85719219"
---
# <a name="sp_register_custom_scripting-transact-sql"></a>sp_register_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  A replicação permite procedimentos armazenados personalizados definidos pelo usuário, para substituir um ou mais dos procedimentos padrão usados em replicação transacional. Quando uma alteração de esquema é feita em uma tabela replicada, esses procedimentos armazenados são recriados. **sp_register_custom_scripting** registra um procedimento armazenado ou [!INCLUDE[tsql](../../includes/tsql-md.md)] arquivo de script que é executado quando uma alteração de esquema ocorre para gerar o script da definição para um novo procedimento armazenado personalizado definido pelo usuário. Esse novo procedimento armazenado personalizado deve refletir o novo esquema da tabela. **sp_register_custom_scripting** é executado no Publicador do banco de dados de publicação, e o arquivo de script registrado ou o procedimento armazenado é executado no Assinante quando ocorre uma alteração de esquema.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_register_custom_scripting [ @type  = ] 'type'  
    [ @value = ] 'value'   
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @type = ] 'type'`É o tipo de procedimento armazenado personalizado ou script que está sendo registrado. o *tipo* é **varchar (16)**, sem padrão, e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**inserido**|Procedimento armazenado personalizado registrado é executado quando uma instrução INSERT é replicada.|  
|**update**|Procedimento armazenado personalizado registrado é executado quando uma instrução UPDATE é replicada.|  
|**delete**|Procedimento armazenado personalizado registrado é executado quando uma instrução DELETE é replicada.|  
|**custom_script**|O script é executado ao término do gatilho DDL (Data Definition Language).|  
  
`[ @value = ] 'value'`Nome de um procedimento armazenado ou nome e caminho totalmente qualificado para o [!INCLUDE[tsql](../../includes/tsql-md.md)] arquivo de script que está sendo registrado. o *valor* é **nvarchar (1024)**, sem padrão.  
  
> [!NOTE]  
>  A especificação de NULL para o parâmetro *Value*cancelará o registro de um script previamente registrado, que é o mesmo que executar [sp_unregister_custom_scripting](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md).  
  
 Quando o valor do *tipo* é **custom_script**, o nome e o caminho completo de um [!INCLUDE[tsql](../../includes/tsql-md.md)] arquivo de script são esperados. Caso contrário, o *valor* deve ser o nome de um procedimento armazenado registrado.  
  
`[ @publication = ] 'publication'`Nome da publicação para a qual o procedimento armazenado personalizado ou o script está sendo registrado. a *publicação* é **sysname**, com um padrão de **NULL**.  
  
`[ @article = ] 'article'`Nome do artigo para o qual o procedimento armazenado personalizado ou o script está sendo registrado. o *artigo* é **sysname**, com um padrão de **NULL**.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_register_custom_scripting** é usado em instantâneo e replicação transacional.  
  
 Esse procedimento armazenado deve ser executado antes de efetuar uma alteração de esquema em uma  tabela replicada. Para obter mais informações sobre como usar esse procedimento armazenado, consulte [regenerar procedimentos transacionais personalizados para refletir alterações de esquema](../../relational-databases/replication/transactional/transactional-articles-regenerate-to-reflect-schema-changes.md).  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** , a função de banco de dados fixa **db_owner** ou a função de banco de dados fixa **db_ddladmin** podem ser executados **sp_register_custom_scripting**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_unregister_custom_scripting](../../relational-databases/system-stored-procedures/sp-unregister-custom-scripting-transact-sql.md)  
  
  
