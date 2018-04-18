---
title: sp_helpmergefilter (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
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
- sp_helpmergefilter
- sp_helpmergefilter_TSQL
helpviewer_keywords:
- sp_helpmergefilter
ms.assetid: f133a094-0009-4771-b93b-e86a5c01e40b
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 35e478a3eb65b030d61f32ea57ed23510d1eb994
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpmergefilter-transact-sql"></a>sp_helpmergefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna informações sobre filtros de mesclagem. Esse procedimento armazenado é executado no Publicador, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpmergefilter [ @publication= ] 'publication'   
    [ , [ @article= ] 'article']  
    [ , [ @filtername= ] 'filtername']  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
 [  **@article=**] **'***artigo***'**  
 É o nome do artigo. *artigo* é **sysname**, com um padrão de **%**, que retorna os nomes de todos os artigos.  
  
 [  **@filtername=**] **'***filtername***'**  
 É o nome do filtro sobre o qual retornar informações. *FilterName* é **sysname**, com um padrão de **%**, que retorna informações sobre todos os filtros definidos no artigo ou publicação.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**join_filterid**|**Int**|ID do filtro de junção.|  
|**FilterName**|**sysname**|Nome do filtro.|  
|**nome do artigo de junção**|**sysname**|Nome do artigo de junção.|  
|**join_filterclause**|**nvarchar(2000)**|Cláusula de filtro que qualifica a junção.|  
|**join_unique_key**|**Int**|Se a junção está em uma chave exclusiva.|  
|**proprietário da tabela base**|**sysname**|Nome do proprietário da tabela base.|  
|**nome da tabela base**|**sysname**|Nome da tabela base.|  
|**proprietário da tabela de junção**|**sysname**|Nome do proprietário da tabela que é adicionada à tabela base.|  
|**nome da tabela de junção**|**sysname**|Nome da tabela que é adicionada à tabela base.|  
|**nome do artigo**|**sysname**|Nome do artigo de tabela que é adicionado à tabela base.|  
|**filter_type**|**tinyint**|Tipo de filtro de mesclagem, que pode ser um dos seguintes:<br /><br /> **1** = somente filtro de junção<br /><br /> **2** = relação de registro lógico<br /><br /> **3** = ambos|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 **sp_helpmergefilter** é usado em replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função fixa de servidor e o **db_owner** pode executar a função de banco de dados fixa **sp_helpmergefilter**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md)   
 [sp_changemergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_dropmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
