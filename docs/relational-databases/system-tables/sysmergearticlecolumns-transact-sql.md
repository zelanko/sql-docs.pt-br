---
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
author: stevestein
ms.author: sstein
ms.openlocfilehash: 2edf9a5656eaf9dd3f18adff28562e279db892e7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68029957"
---
# <a name="sysmergearticlecolumns-transact-sql"></a>sysmergearticlecolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **sysmergearticlecolumns** contém uma linha para cada coluna de tabela que é publicada em uma publicação de mesclagem e mapeia cada coluna para seu artigo de mesclagem. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|DESCRIÇÃO|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Identifica um artigo.|  
|**colid**|**smallint**|Identifica uma coluna em um artigo.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
