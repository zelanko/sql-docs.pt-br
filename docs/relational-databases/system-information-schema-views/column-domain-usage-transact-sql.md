---
title: COLUMN_DOMAIN_USAGE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- COLUMN_DOMAIN_USAGE_TSQL
- COLUMN_DOMAIN_USAGE
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.COLUMN_DOMAIN_USAGE view
- COLUMN_DOMAIN_USAGE view
ms.assetid: deb20037-6a51-47ae-9f49-7601698fafaf
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 3cfc7b44672554fc810b54ef0c554d2a570b8325
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950869"
---
# <a name="columndomainusage-transact-sql"></a>COLUMN_DOMAIN_USAGE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada coluna no banco de dados atual que tem um tipo de dado de alias. Esta exibição de esquema de informações retorna informações sobre os objetos para os quais o usuário atual tem permissões.  
  
 Para recuperar informações dessas exibições, especifique o nome totalmente qualificado do **INFORMATION_SCHEMA.** _view_name_.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**DOMAIN_CATALOG**|**nvarchar(** 128 **)**|Banco de dados no qual o tipo de dados de alias existe.|  
|**DOMAIN_SCHEMA**|**nvarchar(** 128 **)**|Nome do esquema que contém o tipo de dados de alias.<br /><br /> **&#42;&#42;Importante &#42; &#42;**  não use exibições INFORMATION_SCHEMA para determinar o esquema de um tipo de dados. O único modo seguro para localizar o esquema de um tipo é usar a função TYPEPROPERTY.|  
|**DOMAIN_NAME**|**sysname**|Tipo de dados de alias.|  
|**TABLE_CATALOG**|**nvarchar(** 128 **)**|Qualificador da tabela.|  
|**TABLE_SCHEMA**|**nvarchar(** 128 **)**|Proprietário da tabela.<br /><br /> **&#42;&#42;Importante &#42; &#42;**  não use exibições INFORMATION_SCHEMA para determinar o esquema de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição de catálogo sys.objects.|  
|**TABLE_NAME**|**sysname**|Tabela na qual o tipo de dados de alias é usado.|  
|**COLUMN_NAME**|**sysname**|Coluna que usa o tipo de dados de alias.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições do esquema de informações &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  
