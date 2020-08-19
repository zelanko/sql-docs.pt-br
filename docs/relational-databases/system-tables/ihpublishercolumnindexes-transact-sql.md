---
description: IHpublishercolumnindexes (Transact-SQL)
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
ms.openlocfilehash: 0efc9145416e468756bbe861e2e3d36631cd25bb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88446567"
---
# <a name="ihpublishercolumnindexes-transact-sql"></a>IHpublishercolumnindexes (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela do sistema **IHpublishercolumnindexes** mapeia colunas de uma publicação não SQL Server na tabela do sistema [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) para índices na tabela do sistema [IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md) . Esta tabela é armazenada no banco de dados de distribuição.  
  
## <a name="definition"></a>Definição  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|Identifica a coluna de [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) com um índice associado.|  
|**publisherindex_id**|**int**|Identifica um índice da tabela [IHpublisherindexes](../../relational-databases/system-tables/ihpublisherindexes-transact-sql.md) associada à coluna.|  
|**indid**|**int**|Indica posição da coluna na tabela publicada.|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
