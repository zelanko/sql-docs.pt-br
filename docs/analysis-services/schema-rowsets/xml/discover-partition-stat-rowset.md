---
title: Conjunto de linhas DISCOVER_PARTITION_STAT | Microsoft Docs
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
ms.assetid: 20d339e2-f47f-437f-94d5-5b00b400356a
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0863c2f263cc13ff9673063ab1f49535cd2407a3
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="discoverpartitionstat-rowset"></a>Conjunto de linhas DISCOVER_PARTITION_STAT
  Retorna estatísticas sobre agregações em uma partição específica.  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_PARTITION_STAT** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Restrição|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|Required|O nome do banco de dados que contém a dimensão.<br /><br /> Esta coluna é obrigatória na lista de restrições.|  
|**CUBE_NAME**|**DBTYPE_WSTR**|Required|O nome do cubo ou modelo de tabela que contém a partição.<br /><br /> Esta coluna é obrigatória na lista de restrições.|  
|**NOME_GRUPO_MEDIDAS**|**DBTYPE_WSTR**|Required|O nome de um grupo de medidas da dimensão.<br /><br /> Esta coluna é obrigatória na lista de restrições.|  
|**NOME DA PARTIÇÃO**|**DBTYPE_WSTR**|Required|O nome da partição.<br /><br /> Esta coluna é obrigatória na lista de restrições.|  
|**AGGREGATION_NAME**|**DBTYPE_WSTR**||O nome da agregação.|  
|**AGGREGATION_SIZE**|**DBTYPE_I8**||O tamanho da agregação.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd8f-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionStat|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

