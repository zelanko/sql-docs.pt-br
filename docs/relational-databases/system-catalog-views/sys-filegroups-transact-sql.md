---
description: sys.filegroups (Transact-SQL)
title: sys. FileGroups (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.filegroups_TSQL
- filegroups
- sys.filegroups
- filegroups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.filegroups catalog view
ms.assetid: 9e851f72-1f8e-4515-a25d-152ebc12ed56
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d5e55e91e0a2ad031236f3d5fc7a255e9752f2a2
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97473017"
---
# <a name="sysfilegroups-transact-sql"></a>sys.filegroups (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Contém uma linha para cada espaço de dados, que é um grupo de arquivos.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**\<inherited columns>**|--|Para obter uma lista de colunas que essa exibição herda, consulte [sys.data_spaces &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/sys-data-spaces-transact-sql.md).|  
|**filegroup_guid**|**uniqueidentifier**|GUID do grupo de arquivos.<br /><br /> NULL = Grupo de arquivos PRIMARY|  
|**log_filegroup_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)] No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o valor é NULL.|  
|**is_read_only**|**bit**|1 = O grupo de arquivos é somente leitura.<br /><br /> 0 = O grupo de arquivos é leitura/gravação.|  
|**is_autogrow_all_files**|**bit**|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] até a [versão atual](../../sql-server/what-s-new-in-sql-server-2016.md)).<br /><br /> 1 = quando um arquivo no grupo de arquivos atende ao limite de aumento automático, todos os arquivos no grupo de arquivos crescem.<br /><br /> 0 = quando um arquivo no grupo de arquivos atender ao limite de aumento automático, somente esse arquivo aumentará. Este é o padrão.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** . Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Espaços de dados &#40;&#41;Transact-SQL ](../../relational-databases/system-catalog-views/data-spaces-transact-sql.md)  
  
