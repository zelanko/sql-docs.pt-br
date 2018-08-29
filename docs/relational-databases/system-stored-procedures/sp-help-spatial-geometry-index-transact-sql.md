---
title: sp_help_spatial_geometry_index (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geometry_index
- sp_help_spatial_geometry_index_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geometry_index procedure
ms.assetid: f1bcefb1-09c8-4b49-8c51-5d471065849f
caps.latest.revision: 13
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 40eff48fed7d9ba3a687d32858ad2a3f3cdbf154
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43033449"
---
# <a name="sphelpspatialgeometryindex-transact-sql"></a>sp_help_spatial_geometry_index (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna os nomes e valores para um conjunto especificado de propriedades sobre um **geometria** índice espacial. O resultado é retornado em um formato de tabela. Você pode escolher retornar um conjunto principal de propriedades ou todas as propriedades do índice.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_spatial_geometry_index [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ] 'verboseoutput'   
     [ , [ @query_sample = ] 'query_sample']   
```  
  
## <a name="arguments"></a>Argumentos  
 Ver [procedimentos armazenados de argumentos e propriedades de índice espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Ver [procedimentos armazenados de argumentos e propriedades de índice espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter uma função PUBLIC atribuída a ele para acessar o procedimento. Requer permissão READ ACCESS no servidor e no objeto.  
  
## <a name="remarks"></a>Remarks  
 As propriedades que contêm valores NULL não são incluídas no conjunto de retorno.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa `sp_help_spatial_geometry_index` para investigar o índice espacial **SIndx_SpatialTable_geometry_col2** definida na tabela **geometry_col** para determinado exemplo de consulta em **@qs**. Este exemplo retorna apenas as propriedades principais do índice especificado.  
  
```  
declare @qs geometry  
        ='POLYGON((-90.0 -180.0, -90.0 180.0, 90.0 180.0, 90.0 -180.0, -90.0 -180.0))';  
exec sp_help_spatial_geometry_index 'geometry_col', 'SIndx_SpatialTable_geometry_col2', 0, @qs;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de índice espacial](http://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geometry_index_xml](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-xml-transact-sql.md)   
 [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Dados espaciais &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)  
  
  
