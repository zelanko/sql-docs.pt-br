---
title: . identity_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- identity_columns
- sys.identity_columns
- sys.identity_columns_TSQL
- identity_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.identity_columns catalog view
ms.assetid: 97ee01e6-9c9e-4fd9-884b-68b4084669d5
caps.latest.revision: 44
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 21749d2f0f8f2db22399700031f17f4f2bc65132
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysidentitycolumns-transact-sql"></a>sys.identity_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha para cada coluna que seja do tipo identidade.  
  
 O **. identity_columns** exibição herda linhas do **Columns** exibição. O **. identity_columns** exibição retorna as colunas a **Columns** exibição, mais o **seed_value**, **increment_value**, **last_value**, e **is_not_for_replication** colunas. Para obter mais informações, veja [Exibições de catálogo e&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**\<colunas herdadas de sys. Columns >**||O **. identity_columns** exibição retorna todas as colunas de **Columns** exibição. Ela também retorna as colunas adicionais descritas abaixo. Para obter uma descrição das colunas que o **. identity_columns** exibição herda de **Columns**, consulte [Columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).|  
|**seed_value**|**sql_variant**|Valor de semente para esta coluna de identidade. O tipo de dados do valor de semente é igual ao tipo de dados da própria coluna.|  
|**increment_value**|**sql_variant**|Valor de incremento para esta coluna de identidade. O tipo de dados do valor de semente é igual ao tipo de dados da própria coluna.|  
|**last_value**|**sql_variant**|Último valor gerado para esta coluna de identidade. O tipo de dados do valor de semente é igual ao tipo de dados da própria coluna.|  
|**is_not_for_replication**|**bit**|A coluna de identidade foi declarada NOT FOR REPLICATION.|  
  
> [!NOTE]  
>  Para criar um número incrementado automaticamente, que possa ser usado em várias tabelas ou ser chamado de aplicativos, sem referenciar tabelas, consulte [Números de Sequência](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
