---
title: MSmerge_replinfo (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSmerge_replinfo_TSQL
- MSmerge_replinfo
dev_langs:
- TSQL
helpviewer_keywords:
- MSmerge_replinfo system table
ms.assetid: b0924094-c0cc-49c1-869a-65be0d0465a0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5dfda378d9d5327ab62803d07316c12e0eb9d3a9
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="msmergereplinfo-transact-sql"></a>MSmerge_replinfo (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **MSmerge_replinfo** tabela contém uma linha para cada assinatura. Essa tabela localiza informações sobre assinaturas. Essa tabela é armazenada nos bancos de dados de publicação e assinatura.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**repid**|**uniqueidentifier**|A ID exclusiva da replicação.|  
|**use_interactive_resolver**|**bit**|Especifica se o resolvedor interativo é usado durante a reconciliação.<br /><br /> **0** = não não usar o resolvedor interativo.<br /><br /> **1** = usar o resolvedor interativo.|  
|**validation_level**|**int**|Tipo de validação para executar na assinatura. O nível de validação especificado pode ser um destes valores:<br /><br /> **0** não = nenhuma validação.<br /><br /> **1** = validação somente do número de linhas.<br /><br /> **2** = número de linhas e soma de verificação de validação.<br /><br /> **3** = número de linhas e soma de verificação binária.|  
|**resync_gen**|**bigint**|O número de geração usado para nova sincronização da assinatura. Um valor de **– 1** indica que a assinatura não está marcada para ser sincronizada novamente.|  
|**login_name**|**sysname**|O nome do usuário que criou a assinatura.|  
|**nome do host**|**sysname**|O valor usado pelo filtro de linha com parâmetros ao gerar a partição para a assinatura.|  
|**merge_jobid**|**binário (16)**|A ID do trabalho de mesclagem para esta assinatura.|  
|**sync_info**|**int**|Interno-somente para uso.|  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
