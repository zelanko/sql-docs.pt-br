---
description: IHconstrainttypes (Transact-SQL)
title: IHconstrainttypes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHconstrainttypes_TSQL
- IHconstrainttypes
dev_langs:
- TSQL
helpviewer_keywords:
- IHconstrainttypes system table
ms.assetid: 955d6fa9-0b31-4335-a3cd-e4c4d90ad308
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d03babf8250ee41f15fa5f06cd32318873ec276d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88480798"
---
# <a name="ihconstrainttypes-transact-sql"></a>IHconstrainttypes (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela do sistema **IHconstrainttypes** contém uma linha para cada tipo de restrição não SQL Server com suporte para Publicadores não SQL Server. Esta tabela é armazenada no banco de dados de distribuição.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**tipo**|**nvarchar(255)**|O nome de um tipo de restrição com suporte não SQL Server.|  
  
## <a name="see-also"></a>Consulte Também  
 [Replicação de banco de dados heterogênea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
