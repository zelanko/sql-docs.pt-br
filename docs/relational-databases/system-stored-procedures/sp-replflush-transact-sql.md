---
title: sp_replflush (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_replflush
- sp_replflush_TSQL
helpviewer_keywords:
- sp_replflush
ms.assetid: 20809f5f-941d-427f-8f0c-de7a6c487584
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2f4919103db6881a99a65572e7c8492147a50b23
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47638314"
---
# <a name="spreplflush-transact-sql"></a>sp_replflush (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Libera o cache de artigo. Esse procedimento armazenado é executado no Publicador, no banco de dados publicador.  
  
> [!IMPORTANT]  
>  Você não deve precisar executar esse procedimento manualmente. **sp_replflush** só deve ser usado para solucionar problemas de replicação conforme direcionado por um profissional de suporte de replicação experiente.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replflush  
```  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 **sp_replflush** é usado em replicação transacional.  
  
 As definições de artigo são armazenadas no cache para maior eficiência. **sp_replflush** é usado por outros procedimentos armazenados de replicação sempre que uma definição de artigo é modificada ou descartada.  
  
 Somente uma conexão de cliente pode ter acesso de Log Reader a um determinado banco de dados. Se um cliente tem acesso de leitor de log para um banco de dados, executando **sp_replflush** faz com que o cliente libere seu acesso. Outros clientes, então, podem verificar o log de transações usando **sp_replcmds** ou **sp_replshowcmds**.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou o **db_owner** banco de dados fixa podem executar **sp_replflush**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_repltrans &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repltrans-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
