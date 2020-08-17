---
description: sys.spatial_reference_systems (Transact-SQL)
title: sys. spatial_reference_systems (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- spatial_reference_systems_TSQL
- sys.spatial_reference_systems_TSQL
- sys.spatial_reference_systems
- spatial_reference_systems
dev_langs:
- TSQL
helpviewer_keywords:
- sys.spatial_reference_systems catalog view
- spatial_reference_systems
ms.assetid: 3c9bc120-67c3-463f-9e24-29fd623f25a0
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ccfdd98e3bf9eb4252ae0f91bfab4b00ea5722df
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88376202"
---
# <a name="sysspatial_reference_systems-transact-sql"></a>sys.spatial_reference_systems (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Lista os sistemas de referência espaciais (SRIDs) com suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  

  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|spatial_reference_id|**int**|O SRID com suporte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|authority_name|**nvarchar(128)**|A autoridade do SRID.|  
|authorized_spatial_reference_id|**int**|O SRID fornecido pela autoridade chamada em **authority_name**.|  
|well_known_text|**nvarchar(4000)**|A representação WKT do SRID.|  
|unit_of_measure|**nvarchar(128)**|O nome da unidade de medida.|  
|unit_conversion_factor|**float**|O comprimento da unidade de medida em metros.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
  
