---
title: sp_replcounters (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_replcounters
- sp_replcounters_TSQL
helpviewer_keywords:
- sp_replcounters
ms.assetid: fe585b1f-edda-421f-81d6-8a03a3a535d2
author: stevestein
ms.author: sstein
ms.openlocfilehash: 12ddbfe11a2b1a29dadaacde845f96e70959bebb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "68770997"
---
# <a name="sp_replcounters-transact-sql"></a>sp_replcounters (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Retorna estatísticas de replicação sobre contagem de latência, transferência e transação para cada banco de dados publicado. Esse procedimento armazenado é executado no Publicador, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replcounters  
  
```  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**Backup de banco de dados**|**sysname**|Nome do banco de dados.|  
|**Replicated transactions**|**int**|Número de transações no log esperando serem entregues ao banco de dados de distribuição.|  
|**Replication rate trans/sec**|**float**|Número médio de transações por segundo entregue ao banco de dados de distribuição.|  
|**Latência de replicação**|**float**|Tempo médio, em segundos, de permanência das transações no log antes de serem distribuídas.|  
|**Replbeginlsn**|**binary(10)**|LSN (número de sequência de log) do ponto atual de truncamento no log.|  
|**Replnextlsn**|**binary(10)**|LSN do próximo registro de confirmação que aguarda entrega ao banco de dados de distribuição.|  
  
## <a name="remarks"></a>Comentários  
 **sp_replcounters** é usado na replicação transacional.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa **db_owner** ou função de servidor fixa **sysadmin** .  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_replcmds](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_repldone](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_replflush](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
