---
title: sys.sp_xtp_checkpoint_force_garbage_collection (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_checkpoint_force_garbage_collection_TSQL
- sys.sp_xtp_checkpoint_force_garbage_collection
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_checkpoint_force_garbage_collection
ms.assetid: 82b35b2b-edbd-44ac-9fc8-80695f2fd1df
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0c6d57012abbdf6a83587a1d3ffb5c4c9a610850
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysspxtpcheckpointforcegarbagecollection-transact-sql"></a>sys.sp_xtp_checkpoint_force_garbage_collection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Marca os arquivos de origem usados na operação de mesclagem com o LSN (número de sequência de log) após o qual eles não são mais necessários e podem ser limpos. Além disso, move os arquivos cujo LSN associado é menor que o ponto de truncamento do log para a coleta de lixo de FILESTREAM.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
 
## <a name="syntax"></a>Sintaxe  
  
```  
sys.sp_xtp_checkpoint_force_garbage_collection [[ @dbname=database_name]  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name*  
 O banco de dados no qual será executada a coleta de lixo. O padrão é o banco de dados atual.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 para êxito. Diferente de zero para falha.  
  
## <a name="result-set"></a>Conjunto de resultados  
 Uma linha retornada contém as seguintes informações:  
  
|Coluna|Description|  
|------------|-----------------|  
|num_collected_items|Indica o número de arquivos que foram movidos para a coleta de lixo de FILESTREAM. Estes são os arquivos cujo LSN (número de sequência de log) é menor que o LSN do ponto de truncamento de log.|  
|num_marked_for_collection_items|Indica o número de arquivos de dados/delta cujo LSN foi atualizado com o blockID de log do LSN de fim de log.|  
|last_collected_xact_seqno|Retorna o último LSN correspondente cujos arquivos foram movidos para a coleta de lixo de FILESTREAM.|  
  
## <a name="permissions"></a>Permissões  
 Requer permissão de proprietário de banco de dados.  
  
## <a name="sample"></a>Amostra  
  
```  
exec [sys].[sp_xtp_checkpoint_force_garbage_collection] hkdb1  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [OLTP na memória &#40;Otimização na memória&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
