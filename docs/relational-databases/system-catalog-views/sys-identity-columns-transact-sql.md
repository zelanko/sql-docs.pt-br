---
title: sys. identity_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
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
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bb15938bf0d31b386dee5d5d814104cadc5c5711
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43077952"
---
# <a name="sysidentitycolumns-transact-sql"></a>sys.identity_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contém uma linha para cada coluna que seja do tipo identidade.  
  
 O **sys. identity_columns** herda linhas das **sys. Columns** modo de exibição. O **sys. identity_columns** retorna as colunas na **sys. Columns** modo de exibição, mais o **seed_value**, **increment_value**, **last_value**, e **is_not_for_replication** colunas. Para obter mais informações, veja [Exibições de catálogo e&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**\<colunas herdadas de sys. Columns >**||O **sys. identity_columns** retorna todas as colunas na **sys. Columns** modo de exibição. Ela também retorna as colunas adicionais descritas abaixo. Para obter uma descrição das colunas que o **sys. identity_columns** exibição herda **sys. Columns**, consulte [sys. Columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).|  
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
  
  
