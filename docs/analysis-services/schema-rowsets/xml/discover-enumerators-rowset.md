---
title: Conjunto de linhas DISCOVER_ENUMERATORS | Microsoft Docs
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3c67c7e2a87931aee05af6fcdadabb3263cf66a8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34028517"
---
# <a name="discoverenumerators-rowset"></a>Conjunto de linhas DISCOVER_ENUMERATORS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
  
