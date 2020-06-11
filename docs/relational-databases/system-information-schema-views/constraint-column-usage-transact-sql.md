---
title: CONSTRAINT_COLUMN_USAGE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CONSTRAINT_COLUMN_USAGE_TSQL
- CONSTRAINT_COLUMN_USAGE
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.CONSTRAINT_COLUMN_USAGE view
- CONSTRAINT_COLUMN_USAGE view
ms.assetid: 0f3ae521-6b19-43ad-b2c4-3822adb19591
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0176185aab7de80b844e3d1502aea40b1c8aeb18
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669535"
---
# <a name="constraint_column_usage-transact-sql"></a>CONSTRAINT_COLUMN_USAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada coluna no banco de dados atual que tem uma restrição definida na coluna. Esta exibição de esquema de informações retorna informações sobre os objetos para os quais o usuário atual tem permissões.  
  
 Para recuperar informações dessas exibições, especifique o nome totalmente qualificado de **INFORMATION_SCHEMA.** _view_name_.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**TABLE_CATALOG**|**nvarchar (** 128 **)**|Qualificador da tabela.|  
|**TABLE_SCHEMA**|**nvarchar (** 128 **)**|Nome do esquema que contém o proprietário da tabela.<br /><br /> **&#42;&#42; importantes &#42;&#42;** Não use INFORMATION_SCHEMA exibições para determinar o esquema de um objeto. INFORMATION_SCHEMA exibições representam apenas um subconjunto dos metadados de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição de catálogo sys.objects.|  
|**TABLE_NAME**|**nvarchar (** 128 **)**|Nome da tabela.|  
|**COLUMN_NAME**|**nvarchar (** 128 **)**|Nome da coluna.|  
|**CONSTRAINT_CATALOG**|**nvarchar (** 128 **)**|Qualificador da restrição.|  
|**CONSTRAINT_SCHEMA**|**nvarchar (** 128 **)**|Nome do esquema que contém a restrição.<br /><br /> **&#42;&#42; importantes &#42;&#42;** Não use INFORMATION_SCHEMA exibições para determinar o esquema de um objeto. INFORMATION_SCHEMA exibições representam apenas um subconjunto dos metadados de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição de catálogo sys.objects.|  
|**CONSTRAINT_NAME**|**nvarchar (** 128 **)**|Nome da restrição.|  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições do sistema &#40;&#41;Transact-SQL](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições do esquema de informações &#40;&#41;Transact-SQL](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [&#41;sys. Columns &#40;Transact-SQL](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys. Objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [os tipos sys. Types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)   
 [sys. check_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)   
 [sys. key_constraints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [sys. foreign_keys &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-foreign-keys-transact-sql.md)  
  
  
