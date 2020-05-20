---
title: IHpublisherconstraints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublisherconstraints
- IHpublisherconstraints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublisherconstraints system table
ms.assetid: 537b1e1a-7228-4680-aa27-5ad7072ea01e
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f8b7409a15c9e8f3df4991b2b7d20737f5cd82c6
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82813219"
---
# <a name="ihpublisherconstraints-transact-sql"></a>IHpublisherconstraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela do sistema **IHpublisherconstraints** contém uma linha para cada restrição replicada de Publicadores não SQL Server usando o distribuidor atual. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publisherconstraint_id**|**int**|Identifica uma restrição publicada.|  
|**table_id**|**int**|Identifica a tabela de [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) à qual a restrição pertence.|  
|**publisher_id**|**smallint**|Identifica o Editor não SQL Server do qual a coluna está sendo publicada.|  
|**Nome**|**Sysname**|O nome da restrição publicada.|  
|**Tipo**|**nvarchar (255)**|Um tipo de restrição com suporte da tabela do sistema [IHconstrainttypes](../../relational-databases/system-tables/ihconstrainttypes-transact-sql.md) .|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogêneo](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
