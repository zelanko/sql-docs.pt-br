---
title: sp_unregister_custom_scripting (Transact-SQL) | Microsoft Docs
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
- sp_unregister_custom_scripting_TSQL
- sp_unregister_custom_scripting
helpviewer_keywords:
- sp_unregister_custom_scripting
ms.assetid: b6e9e0d2-9144-434d-88af-4874f2582399
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: fce6b2d16e732b76519cb0fbf66a16ca5db6928f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spunregistercustomscripting-transact-sql"></a>sp_unregister_custom_scripting (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Este procedimento armazenado remove um procedimento de armazenado personalizado definido pelo usuário ou [!INCLUDE[tsql](../../includes/tsql-md.md)] arquivo de script que foi registrado executando [sp_register_custom_scripting](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md). Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_unregister_custom_scripting [ @type  = ] 'type'  
    [ , [ @publication = ] 'publication' ]  
    [ , [ @article = ] 'article' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@type**  =] **'***tipo***'**  
 É o tipo de procedimento armazenado personalizado ou o script que está sendo removido. *tipo* é **varchar (16)**, sem padrão e pode ser um dos valores a seguir.  
  
|Valor|Description|  
|-----------|-----------------|  
|**Inserir**|Procedimento armazenado personalizado registrado ou script executado quando uma instrução INSERT é replicada.|  
|**Atualizar**|Procedimento armazenado personalizado registrado ou script executado quando uma instrução UPDATE é replicada.|  
|**Excluir**|Procedimento armazenado personalizado registrado ou script executado quando uma instrução DELETE é replicada.|  
|**CUSTOM_SCRIPT**|Procedimento armazenado personalizado registrado ou script executado ao término do gatilho DDL (Data Definition Language).|  
  
 [  **@publication**  =] **'***publicação***'**  
 Nome da publicação para a qual o procedimento armazenado personalizado ou o script está sendo removido. *publicação* é **sysname**, com um padrão NULL.  
  
 [  **@article**  =] **'***artigo***'**  
 Nome do artigo para o qual o procedimento armazenado personalizado ou o script está sendo removido. *artigo* é **sysname**, com um padrão NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_unregister_custom_scripting** é usado em replicação de instantâneo e transacional.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função fixa de servidor a **db_owner** função de banco de dados fixa ou **db_ddladmin** pode executar a função de banco de dados fixa **SP _ unregister_custom_scripting**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_register_custom_scripting &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-register-custom-scripting-transact-sql.md)  
  
  
