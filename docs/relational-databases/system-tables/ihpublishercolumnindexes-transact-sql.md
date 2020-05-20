---
title: IHpublishercolumnindexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishercolumnindexes
- IHpublishercolumnindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumnindexes system table
ms.assetid: 95b95a1d-b502-4838-825f-82a456487e25
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: fe01417988e21951722b7dbe5e1716cb13abe866
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82832410"
---
# <a name="ihpublishercolumnindexes-transact-sql"></a>IHpublishercolumnindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela do sistema **IHpublishercolumnindexes** mapeia colunas de uma publicação não SQL Server na tabela do sistema [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) para índices na tabela do sistema [IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md) . Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|Identifica a coluna de [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) com um índice associado.|  
|**publisherindex_id**|**int**|Identifica um índice da tabela [IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md) associada à coluna.|  
|**indid**|**int**|Indica posição da coluna na tabela publicada.|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogêneo](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
