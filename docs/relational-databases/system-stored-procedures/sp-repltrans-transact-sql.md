---
title: sp_repltrans (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
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
- sp_repltrans_TSQL
- sp_repltrans
helpviewer_keywords:
- sp_repltrans
ms.assetid: 738e2322-335b-44fa-820e-f31c02743978
caps.latest.revision: 15
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 00bc0a5fbc86d1e1d1aebcfac801e49fd975a4b3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sprepltrans-transact-sql"></a>sp_repltrans (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna um conjunto de resultados de todas as transações no log de transações do banco de dados de publicação marcado para replicação, mas ainda não marcado como distribuído. Esse procedimento armazenado é executado no publicador em um banco de dados de publicação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_repltrans  
```  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_repltrans** retorna informações sobre o banco de dados de publicação do qual ele é executado, permitindo que você exiba transações atualmente não distribuídas (aquelas transações que permanecem no log de transações que não foram enviadas para o Distribuidor). O conjunto de resultados exibe os números de sequência de log do primeiro e do último registro para cada transação. **sp_repltrans** é semelhante a [sp_replcmds &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) , mas não retorna os comandos para as transações.  
  
## <a name="remarks"></a>Remarks  
 **sp_repltrans** é usado em replicação transacional.  
  
 **sp_repltrans** não há suporte para não -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] editores.  
  
## <a name="permissions"></a>Permissões  
 Somente membros do **sysadmin** função de servidor fixa ou **db_owner** pode executar a função de banco de dados fixa **sp_repltrans**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
