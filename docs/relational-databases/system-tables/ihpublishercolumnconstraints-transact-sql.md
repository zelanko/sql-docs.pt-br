---
title: IHpublishercolumnconstraints (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
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
- IHpublishercolumnconstraints
- IHpublishercolumnconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumnconstraints system table
ms.assetid: d7a41da6-e067-430a-8da2-3f6745b8a4f3
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b9dd056bc97aeb438339303813d6661a02dcc63f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="ihpublishercolumnconstraints-transact-sql"></a>IHpublishercolumnconstraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  O **IHpublishercolumnconstraints** tabela do sistema mapeia as colunas de uma publicação não SQL Server no [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) tabela do sistema para restrições na [IHpublisherconstraints ](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md) tabela do sistema. Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|Identifica a coluna de [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) com uma restrição associada.|  
|**publisherconstraint_id**|**int**|Identifica uma restrição de [IHpublisherconstraints](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md) associada à coluna.|  
|**indid**|**int**|Indica posição da coluna na tabela publicada.|  
  
## <a name="see-also"></a>Consulte também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
