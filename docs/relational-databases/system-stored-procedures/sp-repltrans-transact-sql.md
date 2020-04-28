---
title: sp_repltrans (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_repltrans_TSQL
- sp_repltrans
helpviewer_keywords:
- sp_repltrans
ms.assetid: 738e2322-335b-44fa-820e-f31c02743978
author: stevestein
ms.author: sstein
ms.openlocfilehash: 40477973efebac9a484e89e7627f0996285b430b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68770859"
---
# <a name="sp_repltrans-transact-sql"></a>sp_repltrans (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Retorna um conjunto de resultados de todas as transações no log de transações do banco de dados de publicação marcado para replicação, mas ainda não marcado como distribuído. Esse procedimento armazenado é executado no Publicador em um banco de dados de publicação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_repltrans  
```  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_repltrans** retorna informações sobre o banco de dados de publicação do qual ele é executado, permitindo que você exiba transações atualmente não distribuídas (as transações restantes no log de transações que não foram enviadas para o distribuidor). O conjunto de resultados exibe os números de sequência de log do primeiro e do último registro para cada transação. **sp_repltrans** é semelhante a [sp_replcmds &#40;&#41;do Transact-SQL](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) , mas não retorna os comandos para as transações.  
  
## <a name="remarks"></a>Comentários  
 **sp_repltrans** é usado na replicação transacional.  
  
 Não há suporte para **sp_repltrans** para [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores não.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros da função de servidor fixa **sysadmin** ou a função de banco de dados fixa **db_owner** podem ser executados **sp_repltrans**.  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_repldone](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_replflush](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
