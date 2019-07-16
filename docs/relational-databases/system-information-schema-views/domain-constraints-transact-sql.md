---
title: DOMAIN_CONSTRAINTS (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- DOMAIN_CONSTRAINTS
- DOMAIN_CONSTRAINTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- INFORMATION_SCHEMA.DOMAIN_CONSTRAINTS view
- DOMAIN_CONSTRAINTS view
ms.assetid: 436c4480-f1e3-403f-b2bd-de04539afe3c
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7392edabcef2b1ff8348bab641380b6ab64cea0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67950761"
---
# <a name="domainconstraints-transact-sql"></a>DOMAIN_CONSTRAINTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Retorna uma linha para cada tipo de dados de alias no banco de dados atual, que tem uma regra associada e que pode ser acessado pelo usuário atual.  
  
 Para recuperar informações dessas exibições, especifique o nome totalmente qualificado do **INFORMATION_SCHEMA.** _view_name_.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**CONSTRAINT_CATALOG**|**nvarchar(** 128 **)**|Banco de dados no qual a regra existe.|  
|**CONSTRAINT_SCHEMA**|**nvarchar(** 128 **)**|Nome do esquema que contém a restrição.<br /><br /> <strong>\*\* Importante \* \*</strong>  não use exibições INFORMATION_SCHEMA para determinar o esquema de um objeto. O único modo seguro de localizar o esquema de um objeto é consultar a exibição de catálogo sys.objects.|  
|**CONSTRAINT_NAME**|**sysname**|Nome de regra.|  
|**DOMAIN_CATALOG**|**nvarchar(** 128 **)**|Banco de dados no qual o tipo de dados de alias existe.|  
|**DOMAIN_SCHEMA**|**nvarchar(** 128 **)**|Nome do esquema que contém o tipo de dados de alias.<br /><br /> <strong>\*\* Importante \* \*</strong>  não use exibições INFORMATION_SCHEMA para determinar o esquema de um tipo de dados. O único modo seguro para localizar o esquema de um tipo é usar a função TYPEPROPERTY.|  
|**DOMAIN_NAME**|**sysname**|Tipo de dados de alias.|  
|**IS_DEFERRABLE**|**varchar(** 2 **)**|Especifica se a verificação de restrição é adiável. Sempre retorna NO.|  
|**INITIALLY_DEFERRED**|**varchar(** 2 **)**|Especifica se a verificação de restrição é inicialmente adiada. Sempre retorna NO.|  
  
## <a name="see-also"></a>Consulte também  
 [Exibições do sistema &#40;Transact-SQL&#41;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [Exibições do esquema de informações &#40;Transact-SQL&#41;](~/relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)  
  
  
