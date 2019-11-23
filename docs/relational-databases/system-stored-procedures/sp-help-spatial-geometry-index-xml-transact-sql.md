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
ms.openlocfilehash: 9e7eb2e007191088a0259360924b2f5f931dec0a
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/14/2019
ms.locfileid: "72304893"
---
# <a name="sp_help_spatial_geometry_index_xml-transact-sql"></a>sp_help_spatial_geometry_index_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna os nomes e valores de um conjunto especificado de propriedades sobre um índice espacial de **Geometry** . Você pode escolher retornar um conjunto principal de propriedades ou todas as propriedades do índice.  
  
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
 Consulte [argumentos e propriedades de procedimentos armazenados de índice espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="properties"></a>Propriedades  
 Consulte [argumentos e propriedades de procedimentos armazenados de índice espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ser um membro da função **pública** . Requer permissão READ ACCESS no servidor e no objeto.  
  
## <a name="remarks"></a>Remarks  
 As propriedades que contêm valores NULL não são incluídas no conjunto de retorno de XML.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa `sp_help_spatial_geometry_index_xml` para investigar o índice espacial **SIndx_SpatialTable_geometry_col2** definido na tabela **geometry_col** para o exemplo de consulta fornecido em **\@QS**. Este exemplo retorna as propriedades principais do índice especificado em um fragmento XML que exibe o nome e valor das propriedades selecionadas.  
  
 Em seguida, um [XQuery](../../xquery/xquery-basics.md) é executado no conjunto de resultados, retornando uma propriedade específica.  
  
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
 [Argumentos e propriedades de procedimentos armazenados de índice espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md)   
 [Procedimentos armazenados de índice espacial](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geometry_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geometry-index-transact-sql.md)   
 [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Dados espaciais &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [Noções básicas do XQuery](../../xquery/xquery-basics.md)   
 [Referência de linguagem do XQuery](../../xquery/xquery-language-reference-sql-server.md)  
  
  
