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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 473dd22d2f19d29e5b778a585ad59d0d99acbaee
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97479097"
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

[Exibições de catálogo de esquemas &#40;&#41;Transact-SQL ](./catalog-views-transact-sql.md)   

[sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
