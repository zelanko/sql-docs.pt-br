---
title: sp_script_synctran_commands (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_script_synctran_commands
- sp_script_synctran_commands_TSQL
helpviewer_keywords:
- sp_script_synctran_commands
ms.assetid: f132694a-dd05-405b-9d84-21acce9e564a
author: stevestein
ms.author: sstein
ms.openlocfilehash: d7caca72f684dfb6428361a4550860b3bea3f273
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68126406"
---
# <a name="sp_script_synctran_commands-transact-sql"></a>sp_script_synctran_commands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gera um script que contém as chamadas de **sp_addsynctrigger** a serem aplicadas em assinantes para assinaturas atualizáveis. Há uma chamada **sp_addsynctrigger** para cada artigo na publicação. O script gerado também contém as chamadas de **sp_addqueued_artinfo** que criam a tabela **MSsubsciption_articles** necessária para processar publicações em fila. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_script_synctran_commands [@publication = ] 'publication'  
    [ , [@article = ] 'article']  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @publication = ] 'publication'`É o nome da publicação a ser inserida no script. a *publicação* é **sysname**, sem padrão.  
  
`[ @article = ] 'article'`É o nome do artigo a ser inserido no script. o *artigo* é **sysname**, com um padrão de **todos**, que especifica que todos os artigos são incluídos no script.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="results-set"></a>Conjunto de resultados  
 **sp_script_synctran_commands** retorna um conjunto de resultados que consiste em uma única coluna **nvarchar (4000)** . O conjunto de resultados forma os scripts completos necessários para criar as chamadas **sp_addsynctrigger** e **sp_addqueued_artinfo** a serem aplicadas nos assinantes.  
  
## <a name="remarks"></a>Comentários  
 **sp_script_synctran_commands** é usado em instantâneo e replicação transacional.  
  
 **sp_addqueued_artinfo** é usado para assinaturas atualizáveis enfileiradas.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou **db_owner** função de banco de dados fixa podem ser executados **sp_script_synctran_commands**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_addsynctriggers](../../relational-databases/system-stored-procedures/sp-addsynctriggers-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_addqueued_artinfo](../../relational-databases/system-stored-procedures/sp-addqueued-artinfo-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
