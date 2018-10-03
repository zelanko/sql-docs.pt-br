---
title: sp_help_fulltext_catalog_components (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_catalog_components_TSQL
- sp_help_fulltext_catalog_components
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_fulltext_catalog_components
ms.assetid: fbd6a3d4-6a4c-42a2-bff8-2a5eb0745e47
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 54c22d025ae809d035fe75a0b8fe89160bdfb84f
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47720364"
---
# <a name="sphelpfulltextcatalogcomponents-transact-sql"></a>sp_help_fulltext_catalog_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna uma lista de todos os componentes (filtros, separadores de palavras e manipuladores de protocolo) usados em todos os catálogos de texto completo do banco de dados atual.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)]  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_fulltext_catalog_components  
```  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**nome do catálogo de texto completo**|**int**|Nome do catálogo de texto completo.|  
|**id do catálogo de texto completo**|**sysname**|Identificação do catálogo de texto completo.|  
|**componenttype**|**sysname**|Tipo de componente. Um dos seguintes:<br /><br /> Filtrar<br /><br /> Manipulador de protocolo<br /><br /> Separador de palavras|  
|**componentname**|**sysname**|O nome do componente.|  
|**clsid**|**uniqueidentifier**|Identificador de classe do componente.|  
|**fullpath**|**nvarchar(256)**|Caminho até a localização do componente.<br /><br /> NULL = o chamador não é membro de **serveradmin** função de servidor fixa.|  
|**version**|**nvarchar(30)**|A versão do componente.|  
|**manufacturer**|**sysname**|Nome do fabricante do componente.|  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de pesquisa de texto completo e pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [sys.fulltext_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md)   
 [sp_help_fulltext_system_components &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md)   
 [Pesquisa de Texto Completo](../../relational-databases/search/full-text-search.md)  
  
  
