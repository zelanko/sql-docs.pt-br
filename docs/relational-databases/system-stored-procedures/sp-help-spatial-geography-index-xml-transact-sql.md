---
title: sp_help_spatial_geography_index_xml (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geography_index_xml_TSQL
- sp_help_spatial_geography_index_xml
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geography_index_xml procedure
ms.assetid: 821d4127-3ce5-4474-8561-043404a20d81
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: eba6e9c6fe0d979d9e07a7023d1746a1e0cfb2cd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="sphelpspatialgeographyindexxml-transact-sql"></a>sp_help_spatial_geography_index_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna o nome e valor para um conjunto especificado de propriedades sobre um **geografia** índice espacial. Você pode escolher retornar um conjunto principal de propriedades ou todas as propriedades do índice.  
  
 Os resultados são retornados em um fragmento de XML que exibe o nome e valor das propriedades selecionadas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_spatial_geography_index_xml [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ] 'verboseoutput' ]   
     [ , [ @query_sample = ] 'query_sample' ]   
     [ ,.[ @xml_output = ] 'xml_output' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 Consulte [argumentos e as propriedades do índice espacial procedimentos armazenados](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="properties"></a>Propriedades  
 Consulte [argumentos e as propriedades do índice espacial procedimentos armazenados](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter uma função PUBLIC atribuída a ele para acessar o procedimento. Requer permissão READ ACCESS no servidor e no objeto.  
  
## <a name="remarks"></a>Remarks  
 As propriedades que contêm valores NULL não são incluídas no conjunto de retorno.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir usa `sp_help_spatial_geography_index_xml` para investigar o índice espacial **SIndx_SpatialTable_geography_col2** definida na tabela **geography_col** para determinado exemplo de consulta em  **@qs**. Este exemplo retorna as propriedades principais do índice especificado em um fragmento XML que exibe o nome e valor das propriedades selecionadas.  
  
 Um [XQuery](../../xquery/xquery-basics.md) é executada no conjunto de resultados, retornando uma propriedade específica.  
  
```  
declare @qs geography  
        ='POLYGON((-90.0 -180, -90 180.0, 90 180.0, 90 -180, -90 -180.0))';  
declare @x xml;  
exec sp_help_spatial_geography_index_xml 'geography_col', 'SIndx_SpatialTable_geography_col2', 0, @qs, @x output;  
select @x.value('(/Primary_Filter_Efficiency/text())[1]', 'float');  
```  
  
 Semelhante ao [sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md), esse procedimento armazenado fornece acesso programático mais simples para as propriedades de um **geografia** índice espacial e relata o conjunto de resultados em XML.  
  
 A caixa delimitadora de uma **geografia** é toda a Terra.  
  
## <a name="requirements"></a>Requisitos  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de índice espacial](http://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)   
 [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Dados espaciais &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [Fundamentos de XQuery](../../xquery/xquery-basics.md)   
 [Referência de linguagem do XQuery](../../xquery/xquery-language-reference-sql-server.md)  
  
  
