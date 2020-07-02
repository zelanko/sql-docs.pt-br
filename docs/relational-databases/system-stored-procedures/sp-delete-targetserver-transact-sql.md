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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4dc25d35d1037b3fae934ab6112ea2afdf40ca7a
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85790383"
---
# <a name="sp_delete_targetserver-transact-sql"></a>sp_delete_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Remove o servidor especificado da lista de servidores de destino disponíveis.  
   
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_delete_targetserver [ @server_name = ] 'server'   
     [ , [ @clear_downloadlist = ] clear_downloadlist ]  
     [ , [ @post_defection = ] post_defection ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @server_name = ] 'server'`O nome do servidor a ser removido como um servidor de destino disponível. o *servidor* é **nvarchar (30)**, sem padrão.  
  
`[ @clear_downloadlist = ] clear_downloadlist`Especifica se a lista de downloads do servidor de destino deve ser desmarcada. *clear_downloadlist* é de tipo **bit**, com um padrão de **1**. Quando *clear_downloadlist* é **1**, o procedimento limpa a lista de download do servidor antes de excluir o servidor. Quando *clear_downloadlist* for **0**, a lista de download não será desmarcada.  
  
`[ @post_defection = ] post_defection`Especifica se uma instrução de defeito deve ser postada no servidor de destino. *post_defection* é de tipo **bit**, com um padrão de 1. Quando *post_defection* é **1**, o procedimento posta uma instrução de defeito no servidor de destino antes de excluir o servidor. Quando *post_defection* é **0**, o procedimento não publica uma instrução de defeito no servidor de destino.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 A maneira normal de excluir um servidor de destino é chamar **sp_msx_defect** no servidor de destino. Use **sp_delete_targetserver** somente quando uma remoção manual for necessária.  
  
## <a name="permissions"></a>Permissões  
 Para executar esse procedimento armazenado, os usuários devem receber a função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir remove o servidor `LONDON1` dos servidores de trabalho disponíveis.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_targetserver  
  @server_name = N'LONDON1' ;  
GO  
```  
  
## <a name="see-also"></a>Veja também  
 [&#41;&#40;Transact-SQL de sp_help_targetserver](../../relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_msx_defect](../../relational-databases/system-stored-procedures/sp-msx-defect-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
