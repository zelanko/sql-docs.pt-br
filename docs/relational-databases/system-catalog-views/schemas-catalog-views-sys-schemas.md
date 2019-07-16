---
title: sys.schemas (Transact-SQL) | Microsoft Docs
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8f5a0707c599b70ec3c006b00eacb5f8c1a8a87b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68018344"
---
# <a name="schemas-catalog-views---sysschemas"></a>Esquemas exibições - do catálogo sys. schemas
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Contém uma linha para cada esquema de banco de dados.  
  
> [!NOTE]  
>  Esquemas de banco de dados são diferentes de esquemas XML, que são usados para definir o modelo de conteúdo de documentos XML.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nome do esquema. É exclusiva no banco de dados.|  
|**schema_id**|**int**|ID do esquema. É exclusiva no banco de dados.|  
|**principal_id**|**int**|ID da entidade proprietária do esquema.|  
  
## <a name="remarks"></a>Comentários  
Esquemas de banco de dados atuam como namespaces ou contêineres para objetos, como tabelas, exibições, procedimentos e funções, que podem ser encontrados na **sys. Objects** exibição do catálogo.  

Cada esquema tem um proprietário. O proprietário é uma segurança [principal](../../relational-databases/security/authentication-access/principals-database-engine.md).
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
[Entidades](../../relational-databases/security/authentication-access/principals-database-engine.md)

[Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   

[Exibições do catálogo de esquemas &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/c516fb1c-b6ed-48ae-99c7-a78bc4336c8e)   

[sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)  
  
  
