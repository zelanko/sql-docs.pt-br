---
title: Conjunto de linhas DISCOVER_PARTITION_STAT | Microsoft Docs
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
ms.assetid: 20d339e2-f47f-437f-94d5-5b00b400356a
caps.latest.revision: 6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6711aa9d7a98fa635694cc76e98cc89507d524ca
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37197806"
---
# <a name="discoverpartitionstat-rowset"></a>Conjunto de linhas DISCOVER_PARTITION_STAT
  Retorna estatísticas sobre agregações em uma partição específica.  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O `DISCOVER_PARTITION_STAT` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Restrição|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|Obrigatório|O nome do banco de dados que contém a dimensão.<br /><br /> Esta coluna é obrigatória na lista de restrições.|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Obrigatório|O nome do cubo ou modelo de tabela que contém a partição.<br /><br /> Esta coluna é obrigatória na lista de restrições.|  
|`MEASURE_GROUP_NAME`|`DBTYPE_WSTR`|Obrigatório|O nome de um grupo de medidas da dimensão.<br /><br /> Esta coluna é obrigatória na lista de restrições.|  
|`PARTITION_NAME`|`DBTYPE_WSTR`|Obrigatório|O nome da partição.<br /><br /> Esta coluna é obrigatória na lista de restrições.|  
|`AGGREGATION_NAME`|`DBTYPE_WSTR`||O nome da agregação.|  
|`AGGREGATION_SIZE`|`DBTYPE_I8`||O tamanho da agregação.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd8f-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionStat|  
  
## <a name="see-also"></a>Consulte também  
 [Conjunto de linhas de esquema do XML](xml-for-analysis-schema-rowsets.md)  
  
  
