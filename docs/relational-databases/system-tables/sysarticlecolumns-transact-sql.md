---
title: sysarticlecolumns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sysarticlecolumns
- sysarticlecolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysarticlecolumns system table
ms.assetid: 55918592-e05d-43b6-843b-7e4d82fa6275
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 8c7a77aa4850765e37963a5a59995fd9e9004004
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82834130"
---
# <a name="sysarticlecolumns-transact-sql"></a>sysarticlecolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  A tabela **sysarticlecolumns** contém uma linha para cada coluna de tabela que é publicada em uma publicação de instantâneo ou transacional e mapeia cada coluna para seu artigo. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Identifica um artigo.|  
|**colid**|**smallint**|Identifica uma coluna em um artigo.|  
|**is_udt**|**bit**|Indica se a coluna é uma coluna UDT (User-Defined Data Type). Um valor de **1** indica uma coluna UDT.|  
|**is_xml**|**bit**|Indica se a coluna é uma coluna **XML** . Um valor de **1** indica uma coluna XML.|  
|**is_max**|**bit**|Indica se a coluna é uma coluna de tipo de dados de valor grande, **varchar (max)**, **nvarchar (max)** e **varbinary (max)**. Um valor de **1** indica uma coluna de valor grande.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
