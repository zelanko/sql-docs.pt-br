---
title: sp_help_spatial_geography_index_xml (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_help_spatial_geography_index_xml_TSQL
- sp_help_spatial_geography_index_xml
dev_langs:
- TSQL
helpviewer_keywords:
- sp_help_spatial_geography_index_xml procedure
ms.assetid: 821d4127-3ce5-4474-8561-043404a20d81
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c2503e5d3b94b5bc73d9bf2427e0162ba2eda2fe
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72304905"
---
# <a name="sp_help_spatial_geography_index_xml-transact-sql"></a>sp_help_spatial_geography_index_xml (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Retorna o nome e o valor de um conjunto especificado de propriedades sobre um índice espacial de **geografia** . Você pode escolher retornar um conjunto principal de propriedades ou todas as propriedades do índice.  
  
 Os resultados são retornados em um fragmento de XML que exibe o nome e valor das propriedades selecionadas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_spatial_geography_index_xml [ @tabname =] 'tabname'   
     [ , [ @indexname = ] 'indexname' ]   
     [ , [ @verboseoutput = ] 'verboseoutput' ]   
     [ , [ @query_sample = ] 'query_sample' ]   
     [ ,.[ @xml_output = ] 'xml_output' ]   
```  
  
## <a name="arguments"></a>Argumentos  
 Consulte [argumentos e propriedades de procedimentos armazenados de índice espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="properties"></a>Propriedades  
 Consulte [argumentos e propriedades de procedimentos armazenados de índice espacial](../../relational-databases/system-stored-procedures/spatial-index-stored-procedures-arguments-and-properties.md).  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter uma função PUBLIC atribuída a ele para acessar o procedimento. Requer permissão READ ACCESS no servidor e no objeto.  
  
## <a name="remarks"></a>Comentários  
 As propriedades que contêm valores NULL não são incluídas no conjunto de retorno.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir `sp_help_spatial_geography_index_xml` usa para investigar o índice espacial **SIndx_SpatialTable_geography_col2** definido na tabela **geography_col** para o exemplo de consulta fornecido em ** \@QS**. Este exemplo retorna as propriedades principais do índice especificado em um fragmento XML que exibe o nome e valor das propriedades selecionadas.  
  
 Em seguida, um [XQuery](../../xquery/xquery-basics.md) é executado no conjunto de resultados, retornando uma propriedade específica.  
  
```  
declare @qs geography  
        ='POLYGON((-90.0 -180, -90 180.0, 90 180.0, 90 -180, -90 -180.0))';  
declare @x xml;  
exec sp_help_spatial_geography_index_xml 'geography_col', 'SIndx_SpatialTable_geography_col2', 0, @qs, @x output;  
select @x.value('(/Primary_Filter_Efficiency/text())[1]', 'float');  
```  
  
 Semelhante ao [sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md), esse procedimento armazenado fornece acesso programático mais simples às propriedades de um índice espacial de **geografia** e relata o conjunto de resultados em XML.  
  
 A caixa delimitadora de uma **geografia** é toda a terra.  
  
## <a name="requirements"></a>Requisitos  
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados de índice espacial](https://msdn.microsoft.com/library/1be0f34e-3d5a-4a1f-9299-bd482362ec7a)   
 [sp_help_spatial_geography_index](../../relational-databases/system-stored-procedures/sp-help-spatial-geography-index-transact-sql.md)   
 [Visão geral de índices espaciais](../../relational-databases/spatial/spatial-indexes-overview.md)   
 [Dados espaciais &#40;SQL Server&#41;](../../relational-databases/spatial/spatial-data-sql-server.md)   
 [Noções básicas do XQuery](../../xquery/xquery-basics.md)   
 [Referência da linguagem XQuery](../../xquery/xquery-language-reference-sql-server.md)  
  
  
