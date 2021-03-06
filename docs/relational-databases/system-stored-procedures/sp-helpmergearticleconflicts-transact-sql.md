---
description: sp_helpmergearticleconflicts (Transact-SQL)
title: sp_helpmergearticleconflicts (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergearticleconflicts
- sp_helpmergearticleconflicts_TSQL
helpviewer_keywords:
- sp_helpmergearticleconflicts
ms.assetid: 4678a2b9-9a5f-4193-a20d-2e11fc896c3a
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 49ca95bebb40c13bf2044bef58e161bb2bacfdd2
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89535178"
---
# <a name="sp_helpmergearticleconflicts-transact-sql"></a>sp_helpmergearticleconflicts (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna os artigos na publicação que tem conflitos. Esse procedimento armazenado é executado no Publicador, no banco de dados de publicação ou no Assinante, no banco de dados de assinatura de mesclagem.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpmergearticleconflicts [ [ @publication = ] 'publication' ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @publisher_db = ] 'publsher_db' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'` É o nome da publicação de mesclagem. a *publicação* é **sysname**, com um padrão de **%** , que retorna todos os artigos no banco de dados que têm conflitos.  
  
`[ @publisher = ] 'publisher'` É o nome do Publicador. o *Publicador* é **sysname**, com um padrão de NULL.  
  
`[ @publisher_db = ] 'publisher_db'` É o nome do banco de dados do Publicador. *publisher_db* é **sysname**, com um padrão de NULL.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**artigo**|**sysname**|Nome do artigo.|  
|**source_owner**|**sysname**|Proprietário do objeto de origem.|  
|**source_object**|**nvarchar (386)**|Nome do objeto de origem.|  
|**conflict_table**|**nvarchar(258)**|Nome da tabela que armazena os conflitos de entrada ou atualização.|  
|**guidcolname**|**sysname**|Nome do RowGuidCol para o objeto de origem.|  
|**centralized_conflicts**|**int**|Se os registros de conflito são armazenados no Publicador determinado.|  
  
 Se o artigo tiver apenas conflitos de exclusão e nenhuma **conflict_table** linhas, o nome do **conflict_table** no conjunto de resultados será nulo.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpmergearticleconflicts** é usado na replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** e a função de banco de dados fixa **db_owner** podem executar **sp_helpmergearticleconflicts**.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
