---
title: sys. xml_indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.xml_indexes_TSQL
- xml_indexes_TSQL
- sys.xml_indexes
- xml_indexes
dev_langs:
- TSQL
helpviewer_keywords:
- sys.xml_indexes catalog view
ms.assetid: 3408de72-b067-4fda-b5d5-8e856dfd9db3
caps.latest.revision: 34
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8fb4cf3c027b3d514d7e458063bac7af80f80a69
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sysxmlindexes-transact-sql"></a>sys.xml_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha por índice XML.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**\<herdado colunas >**||Herda colunas de [sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).|  
|**using_xml_index_id**|**Int**|NULL = Índice XML primário.<br /><br /> Nonnull = Índice XML secundário.<br /><br /> Nonnull é uma referência de autojunção ao índice XML primário.|  
|**secondary_type**|**char(1)**|Descrição do tipo de índice secundário:<br /><br /> P = Índice XML secundário PATH<br /><br /> V = Índice XML secundário VALUE<br /><br /> R = Índice XML secundário PROPERTY<br /><br /> NULL = Índice XML primário|  
|**secondary_type_desc**|**nvarchar(60)**|Descrição do tipo de índice secundário:<br /><br /> PATH = Índice XML secundário PATH<br /><br /> VALUE = Índice XML secundário VALUE<br /><br /> PROPERTY = Índices xml secundários PROPERTY.<br /><br /> NULL = Índice XML primário|  
|**xml_index_type**|**tinyint**|Tipo de índice:<br /><br /> 0 = Índice XML primário<br /><br /> 1 = Índice XML secundário<br /><br /> 2 = Índice XML seletivo<br /><br /> 3 = Índice XML seletivo secundário|  
|**xml_index_type_description**|**nvarchar(60)**|Descrição de tipo de índice:<br /><br /> PRIMARY_XML<br /><br /> Índice XML secundário<br /><br /> Índice XML seletivo<br /><br /> Índice XML seletivo secundário|  
|**path_id**|**Int**|NULL para todos os índices XML, exceto o índice XML seletivo secundário.<br /><br /> A ID do caminho promovido em que o índice XML seletivo secundário será criado. Esse valor é o mesmo valor de path_id na exibição de sistema sys.selective_xml_index_paths.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições do catálogo de objeto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
