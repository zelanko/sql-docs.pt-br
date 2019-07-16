---
title: sp_help_spatial_geometry_index_xml (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geometry_index_xml_TSQL
- sp_help_spatial_geometry_index_xml
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geometry_index_xml procedure
ms.assetid: 9668ae6d-9ed5-418e-bb9a-9e7b66f7dd16
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 823cd652537cbba486ffd4e432f9413b43f05b12
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68085100"
---
# <a name="sphelpspatialgeometryindexxml-transact-sql"></a>sp_help_spatial_geometry_index_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna os nomes e valores para um conjunto especificado de propriedades sobre um **geometria** índice espacial. Você pode escolher retornar um conjunto principal de propriedades ou todas as propriedades do índice.  
  
 Os resultados são retornados em um fragmento de XML que exibe o nome e valor das propriedades selecionadas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_spatial_geometry_index [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ]'{ 0 | 1 }]   
     [ , [ @query_sample = ] 'query_sample' ]   
     [ ,.[ @xml_output = ] 'xml_output' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 Ver [procedimentos armazenados de argumentos e propriedades de índice espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="properties"></a>Propriedades  
 Ver [procedimentos armazenados de argumentos e propriedades de índice espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="permissions"></a>Permissões  
 Usuário deve ser um membro do **pública** função. Requer permissão READ ACCESS no servidor e no objeto.  
  
## <a name="remarks"></a>Comentários  
 As propriedades que contêm valores NULL não são incluídas no conjunto de retorno de XML.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa `sp_help_spatial_geometry_index_xml` para investigar o índice espacial **SIndx_SpatialTable_geometry_col2** definida na tabela **geometry_col** para determinado exemplo de consulta em **@qs** . Este exemplo retorna as propriedades principais do índice especificado em um fragmento XML que exibe o nome e valor das propriedades selecionadas.  
  
 Uma [XQuery](../../xquery/xquery-basics.md) é executado no conjunto de resultados, retornando uma propriedade específica.  
  
```  
DECLARE @qs geometry  
        ='POLYGON((-90.0 -180.0, -90.0 180.0, 90.0 180.0, 90.0 -180.0, -90.0 -180.0))';  
DECLARE @x xml;  
EXEC sp_help_spatial_geometry_index_xml 'geometry_col', 'SIndx_SpatialTable_geometry_col2', 0, @qs, @x output;  
SELECT @x.value('(/Primary_Filter_Efficiency/text())[1]', 'float');  
```  
  
 Semelhante ao [sp_help_spatial_geometry_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md), esse procedimento armazenado fornece acesso programático mais simples às propriedades de um índice espacial e relata o conjunto de resultados em XML.  
  
## <a name="requirements"></a>Requisitos  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de índice de argumentos e propriedades de espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)   
 [Procedimentos armazenados de índice espacial](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geometry_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)   
 [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Dados espaciais &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [Fundamentos de XQuery](../../xquery/xquery-basics.md)   
 [Referência de linguagem do XQuery](../../xquery/xquery-language-reference-sql-server.md)  
  
  
