---
title: sp_helpmergearticlecolumn (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
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
- sp_helpmergearticlecolumn
- sp_helpmergearticlecolumn_TSQL
helpviewer_keywords:
- sp_helpmergearticlecolumn
ms.assetid: 651c017b-9e9a-48f2-a0bd-6fc896eab334
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 52f1f848b8c3fd5ae2432041387739c355c2ab08
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="sphelpmergearticlecolumn-transact-sql"></a>sp_helpmergearticlecolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna a lista de colunas na tabela especificada ou artigo de exibição para uma publicação de mesclagem. Como os procedimentos armazenados não têm colunas, esse procedimento armazenado retornará um erro se um procedimento armazenado for especificado como o artigo. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpmergearticlecolumn [ @publication = ] 'publication' ]  
        , [ @article= ] 'article' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@publication=**] **'***publicação***'**  
 É o nome da publicação. *publicação* é **sysname**, sem padrão.  
  
 [  **@article=**] **'***artigo***'**  
 É o nome de uma tabela ou exibição que é o artigo para recuperar informações. *artigo* é **sysname**, sem padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**column_id**|**sysname**|Identifica a coluna.|  
|**nome da coluna**|**sysname**|É o nome da coluna para uma tabela ou exibição.|  
|**publicado**|**bit**|Especifica se o nome da coluna é publicado.<br /><br /> **1** Especifica que a coluna está sendo publicada.<br /><br /> **0** Especifica que não é publicado.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpmergearticlecolumn** é usado em replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **replmonitor** função de banco de dados fixa no banco de dados de distribuição ou a lista de acesso da publicação para a publicação pode executar **sp_helpmergearticlecolumn**.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
