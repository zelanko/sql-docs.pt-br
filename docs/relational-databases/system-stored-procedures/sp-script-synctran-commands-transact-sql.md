---
title: sp_script_synctran_commands (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
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
- sp_script_synctran_commands
- sp_script_synctran_commands_TSQL
helpviewer_keywords:
- sp_script_synctran_commands
ms.assetid: f132694a-dd05-405b-9d84-21acce9e564a
caps.latest.revision: 27
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b86c1064eb96174243ea15cba6f5f84a77e40a1f
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43031803"
---
# <a name="spscriptsynctrancommands-transact-sql"></a>sp_script_synctran_commands (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gera um script que contém o **sp_addsynctrigger** chamadas para serem aplicadas nos assinantes para assinaturas atualizáveis. Há um **sp_addsynctrigger** chamar para cada artigo na publicação. O script gerado também contém o **sp_addqueued_artinfo** chamadas que cria a **MSsubsciption_articles** tabela que é necessário para processar publicações enfileiradas. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_script_synctran_commands [@publication = ] 'publication'  
    [ , [@article = ] 'article']  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@publication** =] **'***publicação***'**  
 É o nome da publicação para a qual gerar um script. *publicação* está **sysname**, sem padrão.  
  
 [ **@article** =] **'***artigo***'**  
 É o nome do artigo para o qual gerar um script. *artigo* está **sysname**, com um padrão de **todos os**, que especifica todos os artigos são incluídos no script.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="results-set"></a>Conjunto de resultados  
 **sp_script_synctran_commands** retorna um conjunto de resultados que consiste em uma única **nvarchar (4000)** coluna. O conjunto de resultados forma os scripts completos necessários para criar as a **sp_addsynctrigger** e **sp_addqueued_artinfo** chamadas para serem aplicadas nos assinantes.  
  
## <a name="remarks"></a>Remarks  
 **sp_script_synctran_commands** é usado em replicação de instantâneo e transacional.  
  
 **sp_addqueued_artinfo** é usado para assinaturas atualizáveis enfileiradas.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou **db_owner** banco de dados fixa podem executar **sp_script_synctran_commands**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_addsynctriggers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsynctriggers-transact-sql.md)   
 [sp_addqueued_artinfo &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addqueued-artinfo-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
