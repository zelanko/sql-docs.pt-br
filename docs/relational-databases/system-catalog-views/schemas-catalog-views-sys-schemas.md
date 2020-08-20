---
description: Exibições de catálogo de esquemas-sys. schemas
title: sys. Schemas (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- schemas_TSQL
- sys.schemas_TSQL
- schemas
- sys.schemas
dev_langs:
- TSQL
helpviewer_keywords:
- sys.schemas catalog view
ms.assetid: 29af5ce5-2af7-4103-8f08-3ec92603ba05
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a8a48cbf6a2c50bafab98638c94dce8d5b833012
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88486546"
---
# <a name="schemas-catalog-views---sysschemas"></a>Exibições de catálogo de esquemas-sys. schemas
[!INCLUDE [sql-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdbmi-asa-pdw.md)]

  Contém uma linha para cada esquema de banco de dados.  
  
> [!NOTE]  
>  Esquemas de banco de dados são diferentes de esquemas XML, que são usados para definir o modelo de conteúdo de documentos XML.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do esquema. É exclusiva no banco de dados.|  
|**schema_id**|**int**|ID do esquema. É exclusiva no banco de dados.|  
|**principal_id**|**int**|ID da entidade proprietária do esquema.|  
  
## <a name="remarks"></a>Comentários  
Os esquemas de banco de dados atuam como namespaces ou contêineres para objetos, como tabelas, exibições, procedimentos e funções, que podem ser encontrados na exibição de catálogo **Sys. Objects** .  

Cada esquema tem um proprietário. O proprietário é uma [entidade](../../relational-databases/security/authentication-access/principals-database-engine.md)de segurança.
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
[Entidades](../../relational-databases/security/authentication-access/principals-database-engine.md)

[Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   

[Exibições de catálogo de esquemas &#40;&#41;Transact-SQL ](https://msdn.microsoft.com/library/c516fb1c-b6ed-48ae-99c7-a78bc4336c8e)   

[sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
