---
title: Conjunto de linhas DISCOVER_STORAGE_TABLES | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 13df6f10-8efe-4fe9-83a6-96d108809ed1
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ae51d176ecef04060c58be629b72fe867cd51960
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019669"
---
# <a name="discoverstoragetables-rowset"></a>Conjunto de linhas DISCOVER_STORAGE_TABLES
  Permite ao cliente determinar as tabelas que são incluídas em um banco de dados do Analysis Services executado no modo Tabular ou SharePoint.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DISCOVER_STORAGE_TABLES` linhas contém as seguintes colunas.  
  
|**Nome da coluna**|**Indicador de tipo**|**Comprimento**|**Descrição**|  
|---------------------|------------------------|----------------|---------------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`||Especifica o nome do banco de dados que contém as tabelas.<br /><br /> O `DISCOVER_STORAGE_TABLES` linhas pode ser restringido usando esta coluna. Se esta coluna não for usada para restringir o conjunto de linhas, o banco de dados atual será usado.|  
|`CUBE_NAME`|`DBTYPE_WSTR`||Especifica o cubo ou modelo que contém as tabelas.<br /><br /> O `DISCOVER_STORAGE_TABLES` linhas pode ser restringido usando esta coluna.|  
|`MEASURE_GROUP_NAME`|`DBTYPE_WSTR`||O nome do grupo de medidas.|  
|`PARTITION_NAME`|`DBTYPE_WSTR`||O nome da partição.|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`||O nome da dimensão.|  
|`TABLE_ID`|`DBTYPE_WSTR`||A ID da tabela que é usada para armazenar os atributos de tabela.|  
|`TABLE_PARTITIONS_COUNT`|`DBTYPE_ WSTR`||A contagem de partições da tabela.|  
|`HINT_TABLE_TYPE`|`DBTYPE_ WSTR`||A dica do tipo de tabela.|  
|`ROWS_COUNT`|`DBTYPE_UI4`||O número de linhas na partição.|  
|`RIVIOLATION_COUNT`|`DBTYPE_UI4`||O número de linhas com violações de integridade referencial.|  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `DISCOVER_STORAGE_TABLES` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|**Nome da coluna**|**Indicador de tipo**|**Estado de restrição**|  
|---------------------|------------------------|---------------------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Opcional.|  
|`MEASURE_GROUP_NAME`|`DBTYPE_WSTR`|Opcional|  
|`PARTITION_NAME`|`DBTYPE_WSTR`|Opcional|  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir retorna uma lista das tabelas de armazenamento e o número de linhas em cada uma, a partir do banco de dados padrão na conexão atual.  
  
```  
SELECT TABLE_ID, ROWS_COUNT  
FROM $system.DISCOVER_STORAGE_TABLES  
ORDER BY TABLE_ID DESC  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas de esquema do Analysis Services](../../schema-rowsets/analysis-services-schema-rowsets.md)  
  
  