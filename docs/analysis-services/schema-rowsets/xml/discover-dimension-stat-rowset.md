---
title: Conjunto de linhas DISCOVER_DIMENSION_STAT | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 639f8cd7-3b43-40d5-8b84-552daf60d484
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a844cea3f7e71fc8cef341d84f1d9f50c49f38d8
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="discoverdimensionstat-rowset"></a>Conjunto de linhas DISCOVER_DIMENSION_STAT
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Fornece informações sobre uma dimensão, inclusive o nome do banco de dados que a contém, o nome da dimensão, seus atributos e uma contagem dos membros de cada atributo. Em um modelo de tabela, isso corresponde às colunas em uma tabela e ao número de valores em cada coluna.  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_DIMENSION_STAT** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Restrição|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|Obrigatório|O nome do banco de dados que contém a dimensão.<br /><br /> Esta coluna é obrigatória na lista de restrições.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**|Obrigatório|O nome da dimensão.<br /><br /> Esta coluna é obrigatória na lista de restrições.|  
|**ATTRIBUTE_NAME**|**DBTYPE_WSTR**||O atributo de um atributo na dimensão.|  
|**ATTRIBUTE_COUNT**|**DBTYPE_I8**||A contagem de valores no atributo nomeado. Para um modelo de tabela, o valor sempre equivale ao número de linhas na tabela.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd90-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionDimensionStat|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
