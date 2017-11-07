---
title: Conjunto de linhas DISCOVER_ENUMERATORS | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- DISCOVER_ENUMERATORS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_ENUMERATORS rowset
ms.assetid: ddc7b13c-3135-4419-8166-eddd459167da
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 66ad0a7e82cb1b74108a1275a9e0a7363183d051
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="discoverenumerators-rowset"></a>Conjunto de linhas DISCOVER_ENUMERATORS
  Retorna uma lista de nomes, tipos de dados e valores de enumeração dos enumeradores que recebem suporte do provedor do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) para uma fonte de dados específica. O provedor do XMLA publica todas as constantes de enumeração que reconhece.  
  
 Se você chamar o [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método com o **DISCOVER_ENUMERATORS** valor de enumeração no [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) elemento, o **Discover** método retorna o **DISCOVER_ENUMERATORS** de linhas de esquema.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 Para cada enumerador, há vários elementos, um para cada valor da enumeração. O conjunto de linhas que representa cada enumerador é plano e o nome do enumerador pode ser repetido para elementos que pertencem à mesma enumeração.  
  
 O conjunto de linhas **DISCOVER_ENUMERATORS** contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|**EnumName**|**DBTYPE_WSTR**||O nome do enumerador que contém um conjunto de valores.|  
|**EnumDescription**|**DBTYPE_WSTR**||Uma descrição localizável do enumerador. Pode ser **NULL**.|  
|**EnumType**|**DBTYPE_WSTR**||O tipo de dados dos valores da enumeração.|  
|**ElementName**|**DBTYPE_WSTR**||O nome de um dos elementos de valor no conjunto de enumeradores.<br /><br /> Exemplo: **TDP**|  
|**ElementDescription**|**DBTYPE_WSTR**||(Opcional) Uma descrição localizável do elemento. Pode ser **NULL**.|  
|**ElementValue**|**DBTYPE_WSTR**||O valor do elemento. Pode ser **NULL**.<br /><br /> Exemplo: **01**|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas **DISCOVER_ENUMERATORS** pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|**EnumName**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>Consulte também  
 [XML for Analysis conjuntos de linhas de esquema](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  

