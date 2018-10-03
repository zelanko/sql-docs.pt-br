---
title: sp_repltrans (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_repltrans_TSQL
- sp_repltrans
helpviewer_keywords:
- sp_repltrans
ms.assetid: 738e2322-335b-44fa-820e-f31c02743978
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 09e10f4214d3a7f1d81b347b7d18ee3e5d1ce77d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47668584"
---
# <a name="sprepltrans-transact-sql"></a>sp_repltrans (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna um conjunto de resultados de todas as transações no log de transações do banco de dados de publicação marcado para replicação, mas ainda não marcado como distribuído. Esse procedimento armazenado é executado no publicador do banco de dados de publicação.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_repltrans  
```  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 **sp_repltrans** retorna informações sobre o banco de dados de publicação do qual ele é executado, permitindo que você exiba transações atualmente não distribuídas (aquelas transações que permanecem no log de transações que não foram enviadas para o Distribuidor). O conjunto de resultados exibe os números de sequência de log do primeiro e do último registro para cada transação. **sp_repltrans** é semelhante ao [sp_replcmds &#40;Transact-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) , mas não retorna os comandos para as transações.  
  
## <a name="remarks"></a>Comentários  
 **sp_repltrans** é usado em replicação transacional.  
  
 **sp_repltrans** não há suporte para não -[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Publicadores.  
  
## <a name="permissions"></a>Permissões  
 Somente os membros dos **sysadmin** função de servidor fixa ou o **db_owner** banco de dados fixa podem executar **sp_repltrans**.  
  
## <a name="see-also"></a>Consulte também  
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
