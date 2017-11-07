---
title: Conjunto de linhas DISCOVER_STORAGE_TABLES | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 13df6f10-8efe-4fe9-83a6-96d108809ed1
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: d882e8b20949a656c1402af084a6e017c33b444f
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="discoverstoragetables-rowset"></a>Conjunto de linhas DISCOVER_STORAGE_TABLES
  Permite ao cliente determinar as tabelas que são incluídas em um banco de dados do Analysis Services executado no modo Tabular ou SharePoint.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_STORAGE_TABLES** contém as colunas a seguir.  
  
|**Nome da coluna**|**Indicador de tipo**|**Comprimento**|**Description**|  
|---------------------|------------------------|----------------|---------------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**||Especifica o nome do banco de dados que contém as tabelas.<br /><br /> É possível restringir o conjunto de linhas **DISCOVER_STORAGE_TABLES** usando esta coluna. Se esta coluna não for usada para restringir o conjunto de linhas, o banco de dados atual será usado.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||Especifica o cubo ou modelo que contém as tabelas.<br /><br /> É possível restringir o conjunto de linhas **DISCOVER_STORAGE_TABLES** usando esta coluna.|  
|**NOME_GRUPO_MEDIDAS**|**DBTYPE_WSTR**||O nome do grupo de medidas.|  
|**NOME DA PARTIÇÃO**|**DBTYPE_WSTR**||O nome da partição.|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||O nome da dimensão.|  
|**TABLE_ID**|**DBTYPE_WSTR**||A ID da tabela que é usada para armazenar os atributos de tabela.|  
|**TABLE_PARTITIONS_COUNT**|**DBTYPE _ WSTR**||A contagem de partições da tabela.|  
|**HINT_TABLE_TYPE**|**DBTYPE _ WSTR**||A dica do tipo de tabela.|  
|**ROWS_COUNT**|**DBTYPE_UI4**||O número de linhas na partição.|  
|**RIVIOLATION_COUNT**|**DBTYPE_UI4**||O número de linhas com violações de integridade referencial.|  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **DISCOVER_STORAGE_TABLES** pode ser restringido nas colunas listadas na tabela a seguir.  
  
|**Nome da coluna**|**Indicador de tipo**|**Estado de restrição**|  
|---------------------|------------------------|---------------------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Opcional.|  
|**NOME_GRUPO_MEDIDAS**|**DBTYPE_WSTR**|Opcional|  
|**NOME DA PARTIÇÃO**|**DBTYPE_WSTR**|Opcional|  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir retorna uma lista das tabelas de armazenamento e o número de linhas em cada uma, a partir do banco de dados padrão na conexão atual.  
  
```  
SELECT TABLE_ID, ROWS_COUNT  
FROM $system.DISCOVER_STORAGE_TABLES  
ORDER BY TABLE_ID DESC  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas do esquema do Analysis Services](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  

