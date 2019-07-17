---
title: sp_delete_targetserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_targetserver
- sp_delete_targetserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_targetserver
ms.assetid: cc438701-ad91-419d-9f23-ebc4c548c700
author: stevestein
ms.author: sstein
ms.openlocfilehash: 487d88a7580432bf947893920d307e2f0adffd18
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111988"
---
# <a name="spdeletetargetserver-transact-sql"></a>sp_delete_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove o servidor especificado da lista de servidores de destino disponíveis.  
   
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_targetserver [ @server_name = ] 'server'   
     [ , [ @clear_downloadlist = ] clear_downloadlist ]  
     [ , [ @post_defection = ] post_defection ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @server_name = ] 'server'` O nome do servidor a ser removido como um servidor de destino disponíveis. *servidor* está **nvarchar (30)** , sem padrão.  
  
`[ @clear_downloadlist = ] clear_downloadlist` Especifica se é necessário limpar a lista de download para o servidor de destino. *clear_downloadlist* é do tipo **bit**, com um padrão de **1**. Quando *clear_downloadlist* é **1**, o procedimento desmarca a lista de download para o servidor antes de excluir o servidor. Quando *clear_downloadlist* é **0**, a lista de download não é limpo.  
  
`[ @post_defection = ] post_defection` Especifica se deve lançar uma instrução de defeito para o servidor de destino. *post_defection* é do tipo **bit**, com um padrão de 1. Quando *post_defection* é **1**, o procedimento posta uma instrução de defeito para o servidor de destino antes de excluir o servidor. Quando *post_defection* é **0**, o procedimento não posta uma instrução de defeito para o servidor de destino.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 O modo normal para excluir um servidor de destino é chamar **sp_msx_defect** no servidor de destino. Use **sp_delete_targetserver** apenas quando uma remoção manual é necessária.  
  
## <a name="permissions"></a>Permissões  
 Para executar esse procedimento armazenado, os usuários devem ter o **sysadmin** função de servidor fixa.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove o servidor `LONDON1` dos servidores de trabalho disponíveis.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_targetserver  
  @server_name = N'LONDON1' ;  
GO  
```  
  
## <a name="see-also"></a>Confira também  
 [sp_help_targetserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql.md)   
 [sp_msx_defect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-msx-defect-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
