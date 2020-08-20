---
description: sysarticlecolumns (Transact-SQL)
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
ms.openlocfilehash: 45cc5fc3a39f13f7795e2f26aa91a15b618e2d38
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88460225"
---
# <a name="sysarticlecolumns-transact-sql"></a>sysarticlecolumns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  A tabela **sysarticlecolumns** contém uma linha para cada coluna de tabela que é publicada em uma publicação de instantâneo ou transacional e mapeia cada coluna para seu artigo. Essa tabela é armazenada no banco de dados de publicação.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**artid**|**int**|Identifica um artigo.|  
|**colid**|**smallint**|Identifica uma coluna em um artigo.|  
|**is_udt**|**bit**|Indica se a coluna é uma coluna UDT (User-Defined Data Type). Um valor de **1** indica uma coluna UDT.|  
|**is_xml**|**bit**|Indica se a coluna é uma coluna **XML** . Um valor de **1** indica uma coluna XML.|  
|**is_max**|**bit**|Indica se a coluna é uma coluna de tipo de dados de valor grande, **varchar (max)**, **nvarchar (max)** e **varbinary (max)**. Um valor de **1** indica uma coluna de valor grande.|  
  
## <a name="see-also"></a>Consulte Também  
 [Tabelas de replicação &#40;&#41;Transact-SQL ](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Exibições de replicação &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
