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
ms.sourcegitcommit: 728a4fa5a3022c237b68b31724fce441c4e4d0ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2019
ms.locfileid: "68770997"
---
# <a name="spreplcounters-transact-sql"></a>sp_replcounters (Transact-SQL)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Retorna estatísticas de replicação sobre contagem de latência, transferência e transação para cada banco de dados publicado. Esse procedimento armazenado é executado no Publicador, em qualquer banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_replcounters  
  
```  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**Backup de banco de dados**|**sysname**|Nome do banco de dados.|  
|**Transações replicadas**|**int**|Número de transações no log esperando serem entregues ao banco de dados de distribuição.|  
|**Trans. de taxa de replicação/s**|**float**|Número médio de transações por segundo entregue ao banco de dados de distribuição.|  
|**Latência de replicação**|**float**|Tempo médio, em segundos, de permanência das transações no log antes de serem distribuídas.|  
|**Replbeginlsn**|**binary(10)**|LSN (número de sequência de log) do ponto atual de truncamento no log.|  
|**Replnextlsn**|**binary(10)**|LSN do próximo registro de confirmação que aguarda entrega ao banco de dados de distribuição.|  
  
## <a name="remarks"></a>Comentários  
 **sp_replcounters** é usado na replicação transacional.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função de banco de dados fixa **db_owner** ou à função de servidor fixa **sysadmin** .  
  
## <a name="see-also"></a>Consulte também  
 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md)   
 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md)   
 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
