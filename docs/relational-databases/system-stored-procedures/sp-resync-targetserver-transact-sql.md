---
title: sp_resync_targetserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_resync_targetserver
- sp_resync_targetserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_resync_targetserver
ms.assetid: 40e44df7-d3e3-44ee-b149-08aba629a21f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8275c27eac96a5cb6d88e7bd5e9e50d9a878a6be
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85718659"
---
# <a name="sp_resync_targetserver-transact-sql"></a>sp_resync_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Sincroniza novamente todos os trabalhos multisservidor no servidor de destino especificado.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_resync_targetserver  
     [ @server_name = ] 'server'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @server_name = ] 'server'`O nome do servidor a ser ressincronizado. *server* é **sysname**, sem padrão. Se **All** for especificado, todos os servidores de destino serão ressincronizados.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Relata o resultado de **sp_post_msx_operation** ações.  
  
## <a name="remarks"></a>Comentários  
 **sp_resync_targetserver** exclui o conjunto atual de instruções para o servidor de destino e posta um novo conjunto para download do servidor de destino. O novo conjunto consiste em uma instrução para excluir todos os trabalhos multisservidor, seguida por uma inserção para cada trabalho atualmente destinado no servidor.  
  
## <a name="permissions"></a>Permissões  
 As permissões para executar este procedimento assumem como padrão os membros da função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir sincroniza novamente o servidor de destino `SEATTLE1`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_resync_targetserver  
    N'SEATTLE1' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_help_downloadlist](../../relational-databases/system-stored-procedures/sp-help-downloadlist-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_post_msx_operation](../../relational-databases/system-stored-procedures/sp-post-msx-operation-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
