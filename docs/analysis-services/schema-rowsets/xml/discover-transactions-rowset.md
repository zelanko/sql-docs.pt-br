---
title: Conjunto de linhas DISCOVER_TRANSACTIONS | Microsoft Docs
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
ms.assetid: 85789177-c5df-4336-a90c-c20d69277ab4
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0b287af43de1284c727a64d27d55b3ccf75c5d87
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="discovertransactions-rowset"></a>Conjunto de linhas DISCOVER_TRANSACTIONS
  Retorna o conjunto atual de transações pendentes no sistema.  
  
 **Aplica-se a:** modelos de tabela, modelos multidimensionais  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 O conjunto de linhas **DISCOVER_TRANSACTIONS** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Description|  
|-----------------|--------------------|-----------------|  
|**TRANSACTION_ID**|**DBTYPE_WSTR**|O identificador exclusivo da transação, como um GUID.|  
|**TRANSACTION_SESSION_ID**|**DBTYPE_WSTR**|O identificador exclusivo da sessão de transação, como um GUID.|  
|**TRANSACTION_START_TIME**|**DBTYPE_DBTIMESTAMP**|A data e a hora UTC do servidor em que a transação foi iniciada.|  
|**TRANSACTION_ELAPSED_TIME_MS**|**DBTYPE_I8**|O tempo decorrido, em milissegundos, desde o início da transação.|  
|**TRANSACTION_CPU_TIME_MS**|**DBTYPE_I8**|O tempo de CPU, em milissegundos, consumido por todas as solicitações desde o início da transação.|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **DISCOVER_TRANSACTIONS** pode ser restringido nas colunas listadas na tabela a seguir.  
  
|**Nome da coluna**|**Indicador de tipo**|**Estado de restrição**|  
|---------------------|------------------------|---------------------------|  
|**ID**|**DBTYPE_WSTR**|Opcional.|  
|**SESSION_ID**|**DBTYPE_WSTR**|Opcional.|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usando ADOMD.NET para retornar o conjunto de linhas  
 Ao usar ADOMD.NET e o conjunto de linhas de esquema para recuperar metadados, você pode usar o GUID ou a cadeia de caracteres para referenciar um objeto de conjunto de linhas de esquema no método GetSchemaDataSet. Para obter mais informações, consulte [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md).  
  
 A tabela a seguir fornece os valores de GUID e de cadeia de caracteres que identificam este conjunto de linhas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd28-8148-11d0-87bb-00c04fc33942|  
|String|DISCOVER_TRANSACTIONS|  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
