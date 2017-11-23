---
title: sp_helpmergearticleconflicts (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_helpmergearticleconflicts
- sp_helpmergearticleconflicts_TSQL
helpviewer_keywords: sp_helpmergearticleconflicts
ms.assetid: 4678a2b9-9a5f-4193-a20d-2e11fc896c3a
caps.latest.revision: "28"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b7a1d10d6d2ba731ceaaaba51b8f786b262a2e28
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpmergearticleconflicts-transact-sql"></a>sp_helpmergearticleconflicts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna os artigos na publicação que tem conflitos. Esse procedimento armazenado é executado no Publicador, no banco de dados de publicação ou no Assinante, no banco de dados de assinatura de mesclagem.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpmergearticleconflicts [ [ @publication = ] 'publication' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publsher_db' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação de mesclagem. *publicação* é **sysname**, com um padrão de  **%** , que retorna todos os artigos no banco de dados que tem conflitos.  
  
 [  **@publisher=**] **'***publicador***'**  
 É o nome do publicador. *publicador* é **sysname**, com um padrão NULL.  
  
 [  **@publisher_db=**] **'***publisher_db***'**  
 É o nome do banco de dados publicador. *publisher_db* é **sysname**, com um padrão NULL.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**artigo**|**sysname**|Nome do artigo.|  
|**source_owner**|**sysname**|Proprietário do objeto de origem.|  
|**source_object**|**nvarchar (386)**|Nome do objeto de origem.|  
|**conflict_table**|**nvarchar (258)**|Nome da tabela que armazena os conflitos de entrada ou atualização.|  
|**guidcolname**|**sysname**|Nome do RowGuidCol para o objeto de origem.|  
|**centralized_conflicts**|**int**|Se os registros de conflito são armazenados no Publicador determinado.|  
  
 Se o artigo tiver somente conflitos excluídos e não **conflict_table** linhas, o nome do **conflict_table** no resultado do conjunto é NULL.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpmergearticleconflicts** é usado em replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função fixa de servidor e o **db_owner** pode executar a função de banco de dados fixa **sp_helpmergearticleconflicts**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
