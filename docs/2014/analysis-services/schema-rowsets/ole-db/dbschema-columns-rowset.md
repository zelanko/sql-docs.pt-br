---
title: Linhas de DBSCHEMA_COLUMNS | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DBSCHEMA_COLUMNS
topic_type:
- apiref
helpviewer_keywords:
- DBSCHEMA_COLUMNS rowset
ms.assetid: 653bdd07-a533-4a99-8b6a-6e5c7322e1f3
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 413e86e156db59e7621c94bdc1c99cd0087a987f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115304"
---
# <a name="dbschemacolumns-rowset"></a>Conjunto de linhas de DBSCHEMA_COLUMNS
  Oferece informações de coluna por todas as colunas que atendem aos critérios de restrição fornecidos.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DBSCHEMA_COLUMNS` linhas contém as seguintes colunas.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`||O nome do Banco de dados.|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`||Sem suporte.|  
|`TABLE_NAME`|`DBTYPE_WSTR`||O nome do cubo.|  
|`COLUMN_NAME`|`DBTYPE_WSTR`||O nome da hierarquia ou da medida do atributo.|  
|`COLUMN_GUID`|`DBTYPE_GUID`||Sem suporte.|  
|`COLUMN_PROPID`|`DBTYPE_UI4`||Sem suporte.|  
|`ORDINAL_POSITION`|`DBTYPE_UI4`||A posição da coluna, começando por 1.|  
|`COLUMN_HAS_DEFAULT`|`DBTYPE_BOOL`||Sem suporte.|  
|`COLUMN_DEFAULT`|`DBTYPE_WSTR`||Sem suporte.|  
|`COLUMN_FLAGS`|`DBTYPE_UI4`||Uma máscara de bits `DBCOLUMNFLAGS` que indica propriedades da coluna. Consulte 'Tipo enumerado DBCOLUMNFLAGS' em [icolumnsinfo:: Getcolumninfo](http://msdn2.microsoft.com/library/ms722704.aspx)|  
|`IS_NULLABLE`|`DBTYPE_BOOL`||Sempre retorna `false`.|  
|`DATA_TYPE`|`DBTYPE_WSTR`<br /><br /> `DBTYPE_VARIANT`||O tipo de dados da coluna. Retorna uma cadeia de caracteres para colunas de dimensão e uma variante para medidas.|  
|`TYPE_GUID`|`DBTYPE_GUID`||Sem suporte.|  
|`CHARACTER_MAXIMUM_LENGTH`|`DBTYPE_UI4`||O comprimento máximo possível de um valor na coluna.<br /><br /> Recuperado por meio da propriedade `DataSize` de `DataItem`.|  
|`CHARACTER_OCTET_LENGTH`|`DBTYPE_UI4`||O máximo comprimento possível de um valor da coluna, em bytes, para colunas de caractere ou de binários.<br /><br /> Um valor zero (0) indica que a coluna não tem um comprimento máximo.<br /><br /> `NULL` será retornado para as colunas que não retornam os tipos de dados binários ou caracteres.|  
|`NUMERIC_PRECISION`|`DBTYPE_UI2`||A precisão máxima da coluna para os tipos de dados numéricos diferentes de `DBTYPE_VARNUMERIC`.|  
|`NUMERIC_SCALE`|`DBTYPE_I2`||O número de dígitos à direita da vírgula decimal para `DBTYPE_DECIMAL`, `DBTYPE_NUMERIC`, `DBTYPE_VARNUMERIC`. Caso contrário, será `NULL`.|  
|`DATETIME_PRECISION`|`DBTYPE_UI4`||Sem suporte.|  
|`CHARACTER_SET_CATALOG`|`DBTYPE_WSTR`||Sem suporte.|  
|`CHARACTER_SET_SCHEMA`|`DBTYPE_WSTR`||Sem suporte.|  
|`CHARACTER_SET_NAME`|`DBTYPE_WSTR`||Sem suporte.|  
|`COLLATION_CATALOG`|`DBTYPE_WSTR`||Sem suporte.|  
|`COLLATION_SCHEMA`|`DBTYPE_WSTR`||Sem suporte.|  
|`COLLATION_NAME`|`DBTYPE_WSTR`||Sem suporte.|  
|`DOMAIN_CATALOG`|`DBTYPE_WSTR`||Sem suporte.|  
|`DOMAIN_SCHEMA`|`DBTYPE_WSTR`||Sem suporte.|  
|`DOMAIN_NAME`|`DBTYPE_WSTR`||Sem suporte.|  
|`DESCRIPTION`|`DBTYPE_WSTR`||Sem suporte.|  
|`COLUMN_OLAP_TYPE`|`DBTYPE_WSTR`||O tipo OLAP do objeto.<br /><br /> `MEASURE` indica que o objeto é uma medida.<br /><br /> `ATTRIBUTE` indica que o objeto é um atributo de dimensão.<br /><br /> `SCHEMA` indica se o objeto é uma coluna em um esquema.|  
  
 O conjunto de linhas é classificado em `TABLE_CATALOG`, `TABLE_SCHEMA`, `TABLE_NAME`.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `DBSCHEMA_COLUMNS` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`TABLE_CATALOG`|`DBTYPE_WSTR`|Opcional|  
|`TABLE_SCHEMA`|`DBTYPE_WSTR`|Opcional|  
|`TABLE_NAME`|`DBTYPE_WSTR`|Opcional|  
|`COLUMN_NAME`|`DBTYPE_WSTR`|Opcional|  
|`COLUMN_OLAP_TYPE`|`DBTYPE_WSTR`|Opcional|  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas do esquema OLE DB](ole-db-schema-rowsets.md)  
  
  