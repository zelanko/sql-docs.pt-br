---
title: Conjunto de linhas DISCOVER_STORAGE_TABLES | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b87759d736044febc89099d493fb357d7e5153b9
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="discoverstoragetables-rowset"></a>Conjunto de linhas DISCOVER_STORAGE_TABLES
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Permite ao cliente determinar as tabelas que são incluídas em um banco de dados do Analysis Services executado no modo Tabular ou SharePoint.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_STORAGE_TABLES** contém as colunas a seguir.  
  
|**Nome da coluna**|**Indicador de tipo**|**Comprimento**|**Descrição**|  
|---------------------|------------------------|----------------|---------------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**||Especifica o nome do banco de dados que contém as tabelas.<br /><br /> É possível restringir o conjunto de linhas **DISCOVER_STORAGE_TABLES** usando esta coluna. Se esta coluna não for usada para restringir o conjunto de linhas, o banco de dados atual será usado.|  
|**CUBE_NAME**|**DBTYPE_WSTR**||Especifica o cubo ou modelo que contém as tabelas.<br /><br /> É possível restringir o conjunto de linhas **DISCOVER_STORAGE_TABLES** usando esta coluna.|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**||O nome do grupo de medidas.|  
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
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|Opcional|  
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
  
  
