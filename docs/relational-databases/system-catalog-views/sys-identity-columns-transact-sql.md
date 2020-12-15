---
description: sys.identity_columns (Transact-SQL)
title: sys.identity_columns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 195768c830e13f2cb61f04bff9fe67f6eefe6dc4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97484758"
---
# <a name="sysidentity_columns-transact-sql"></a>sys.identity_columns (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Contém uma linha para cada coluna que seja do tipo identidade.  
  
 A exibição **Sys.identity_columns** herda linhas da exibição **Sys. Columns** . A exibição **Sys.identity_columns** retorna as colunas na exibição **Sys. Columns** , além das colunas **seed_value**, **increment_value**, **last_value** e **is_not_for_replication** . Para obter mais informações, veja [Exibições de catálogo e&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md).  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**\<columns inherited from sys.columns>**||A exibição **Sys.identity_columns** retorna todas as colunas na exibição **Sys. Columns** . Ela também retorna as colunas adicionais descritas abaixo. Para obter uma descrição das colunas que a exibição de **Sys.identity_columns** herda de **Sys. Columns**, consulte [Sys. Columns &#40;&#41;Transact-SQL](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).|  
|**seed_value**|**sql_variant**|Valor de semente para esta coluna de identidade. O tipo de dados do valor de semente é igual ao tipo de dados da própria coluna.|  
|**increment_value**|**sql_variant**|Valor de incremento para esta coluna de identidade. O tipo de dados do valor de semente é igual ao tipo de dados da própria coluna.|  
|**last_value**|**sql_variant**|Último valor gerado para esta coluna de identidade. O tipo de dados do valor de semente é igual ao tipo de dados da própria coluna.|  
|**is_not_for_replication**|**bit**|A coluna de identidade foi declarada NOT FOR REPLICATION. **Observação:** Esta coluna não se aplica ao Azure Synapse Analytics.|  
  
> [!NOTE]  
>  Para criar um número incrementado automaticamente, que possa ser usado em várias tabelas ou ser chamado de aplicativos, sem referenciar tabelas, consulte [Números de Sequência](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Consultando as perguntas frequentes do catálogo do sistema do SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
