---
description: sys.check_constraints (Transact-SQL)
title: sys. check_constraints (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/28/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.check_constraints
- sys.check_constraints_TSQL
- check_constraints_TSQL
- check_constraints
dev_langs:
- TSQL
helpviewer_keywords:
- sys.check_constraints catalog view
ms.assetid: 940ebc5e-44ba-4dae-8b29-da94f2d1d6c4
author: VanMSFT
ms.author: vanto
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 767714d75fcb885a23899161714695237fcb8149
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88323852"
---
# <a name="syscheck_constraints-transact-sql"></a>sys.check_constraints (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Contém uma linha para cada objeto que é uma restrição de verificação, com **Sys. Objects. Type** = ' C'.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**\<Columns inherited from sys.objects>**||Para obter uma lista de colunas que essa exibição herda, consulte [Sys. objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).|  
|**is_disabled**|**bit**|A restrição CHECK está desabilitada.|  
|**is_not_for_replication**|**bit**|A restrição CHECK foi criada com a opção NOT FOR REPLICATION.|  
|**is_not_trusted**|**bit**|A restrição CHECK não foi verificada pelo sistema para todas as linhas.|  
|**parent_column_id**|**int**|0 indica uma restrição CHECK do nível da tabela.<br /><br /> O valor diferente de zero indica que esta é uma restrição CHECK em nível de coluna definida na coluna com o valor de ID especificado.|  
|**defini**|**nvarchar(max)**|Expressão SQL que define esta restrição CHECK.|  
|**uses_database_collation**|**bit**|1 = A definição de restrição depende da ordenação padrão do banco de dados para avaliação correta; caso contrário, 0. Tal dependência impede a alteração da ordenação padrão do banco de dados.|  
|**is_system_named**|**bit**|1 = O nome foi gerado pelo sistema.<br /><br /> 0 = O nome foi fornecido pelo usuário.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo de objeto&#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
