---
title: sys. xml_indexes (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
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
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 69e6102d6d74604c59a6dc6e827dfd0226170987
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47777974"
---
# <a name="sysxmlindexes-transact-sql"></a>sys.xml_indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma linha por índice XML.  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**\<herdado colunas >**||Herda colunas de [sys. Indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).|  
|**using_xml_index_id**|**int**|NULL = Índice XML primário.<br /><br /> Nonnull = Índice XML secundário.<br /><br /> Nonnull é uma referência de autojunção ao índice XML primário.|  
|**secondary_type**|**char(1)**|Descrição do tipo de índice secundário:<br /><br /> P = Índice XML secundário PATH<br /><br /> V = Índice XML secundário VALUE<br /><br /> R = Índice XML secundário PROPERTY<br /><br /> NULL = Índice XML primário|  
|**secondary_type_desc**|**nvarchar(60)**|Descrição do tipo de índice secundário:<br /><br /> PATH = Índice XML secundário PATH<br /><br /> VALUE = Índice XML secundário VALUE<br /><br /> PROPERTY = Índices xml secundários PROPERTY.<br /><br /> NULL = Índice XML primário|  
|**xml_index_type**|**tinyint**|Tipo de índice:<br /><br /> 0 = Índice XML primário<br /><br /> 1 = Índice XML secundário<br /><br /> 2 = Índice XML seletivo<br /><br /> 3 = Índice XML seletivo secundário|  
|**xml_index_type_description**|**nvarchar(60)**|Descrição de tipo de índice:<br /><br /> PRIMARY_XML<br /><br /> Índice XML secundário<br /><br /> Índice XML seletivo<br /><br /> Índice XML seletivo secundário|  
|**path_id**|**int**|NULL para todos os índices XML, exceto o índice XML seletivo secundário.<br /><br /> A ID do caminho promovido em que o índice XML seletivo secundário será criado. Esse valor é o mesmo valor de path_id na exibição de sistema sys.selective_xml_index_paths.|  
  
## <a name="permissions"></a>Permissões  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obter mais informações, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte também  
 [Exibições de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Exibições do catálogo do objeto &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)  
  
  
