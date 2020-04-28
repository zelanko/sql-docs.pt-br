---
title: sp_helpmergearticlecolumn (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_helpmergearticlecolumn
- sp_helpmergearticlecolumn_TSQL
helpviewer_keywords:
- sp_helpmergearticlecolumn
ms.assetid: 651c017b-9e9a-48f2-a0bd-6fc896eab334
author: stevestein
ms.author: sstein
ms.openlocfilehash: da2eec998176dfd46ab261fa405ecaa4b6e90044
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68126438"
---
# <a name="sp_helpmergearticlecolumn-transact-sql"></a>sp_helpmergearticlecolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna a lista de colunas na tabela especificada ou artigo de exibição para uma publicação de mesclagem. Como os procedimentos armazenados não têm colunas, esse procedimento armazenado retornará um erro se um procedimento armazenado for especificado como o artigo. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_helpmergearticlecolumn [ @publication = ] 'publication' ]  
        , [ @article= ] 'article' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação. a *publicação* é **sysname**, sem padrão.  
  
`[ @article = ] 'article'`É o nome de uma tabela ou exibição que é o artigo no qual recuperar informações. o *artigo* é **sysname**, sem padrão.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**column_id**|**sysname**|Identifica a coluna.|  
|**column_name**|**sysname**|É o nome da coluna para uma tabela ou exibição.|  
|**published**|**bit**|Especifica se o nome da coluna é publicado.<br /><br /> **1** especifica que a coluna está sendo publicada.<br /><br /> **0** especifica que não está publicado.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_helpmergearticlecolumn** é usado na replicação de mesclagem.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de banco de dados fixa **replmonitor** no banco de dados de distribuição ou na lista de acesso à publicação da publicação podem ser executados **sp_helpmergearticlecolumn**.  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
