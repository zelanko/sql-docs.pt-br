---
description: sysmergearticlecolumns (Transact-SQL)
title: sysmergearticlecolumns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysmergearticlecolumns
- sysmergearticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysmergearticlecolumns system table
ms.assetid: 1ad8663f-a624-42a2-8641-fefac3433c97
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8bae31473976690ea60575b7ab3ce902f46d3c32
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88427618"
---
# <a name="sysmergearticlecolumns-transact-sql"></a>sysmergearticlecolumns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **sysmergearticlecolumns** contém uma linha para cada coluna de tabela que é publicada em uma publicação de mesclagem e mapeia cada coluna para seu artigo de mesclagem. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Identifica um artigo.|  
|**colid**|**smallint**|Identifica uma coluna em um artigo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
