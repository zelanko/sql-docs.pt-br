---
title: Conjunto de linhas DISCOVER_ENUMERATORS | Microsoft Docs
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
api_name:
- DISCOVER_ENUMERATORS
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_ENUMERATORS rowset
ms.assetid: ddc7b13c-3135-4419-8166-eddd459167da
caps.latest.revision: 31
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 328d37a9d010388c0cb8d0e7e9d251601e35f949
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37302706"
---
# <a name="discoverenumerators-rowset"></a>Conjunto de linhas DISCOVER_ENUMERATORS
  Retorna uma lista de nomes, tipos de dados e valores de enumeração dos enumeradores que recebem suporte do provedor do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) para uma fonte de dados específica. O provedor do XMLA publica todas as constantes de enumeração que reconhece.  
  
 Se você chamar o [Discover](../../xmla/xml-elements-methods-discover.md) método com o `DISCOVER_ENUMERATORS` valor de enumeração no [RequestType](../../xmla/xml-elements-properties/type-element-xmla.md) elemento, o `Discover` método retorna o `DISCOVER_ENUMERATORS` de linhas de esquema.  
  
## <a name="rowset-columns"></a>Colunas do conjunto de linhas  
 Para cada enumerador, há vários elementos, um para cada valor da enumeração. O conjunto de linhas que representa cada enumerador é plano e o nome do enumerador pode ser repetido para elementos que pertencem à mesma enumeração.  
  
 O `DISCOVER_ENUMERATORS` linhas contém as colunas a seguir.  
  
|Nome da coluna|Indicador de tipo|Comprimento|Description|  
|-----------------|--------------------|------------|-----------------|  
|`EnumName`|`DBTYPE_WSTR`||O nome do enumerador que contém um conjunto de valores.|  
|`EnumDescription`|`DBTYPE_WSTR`||Uma descrição localizável do enumerador. Pode ser `NULL`.|  
|`EnumType`|`DBTYPE_WSTR`||O tipo de dados dos valores da enumeração.|  
|`ElementName`|`DBTYPE_WSTR`||O nome de um dos elementos de valor no conjunto de enumeradores.<br /><br /> Exemplo: `TDP`|  
|`ElementDescription`|`DBTYPE_WSTR`||(Opcional) Uma descrição localizável do elemento. Pode ser `NULL`.|  
|`ElementValue`|`DBTYPE_WSTR`||O valor do elemento. Pode ser `NULL`.<br /><br /> Exemplo: `01`|  
  
 Este conjunto de linhas do esquema não é classificado.  
  
## <a name="restriction-columns"></a>Colunas de restrição  
 O conjunto de linhas `DISCOVER_ENUMERATORS` pode ser restringido nas colunas listadas na tabela a seguir.  
  
|Nome da coluna|Indicador de tipo|Estado de restrição|  
|-----------------|--------------------|-----------------------|  
|`EnumName`|`DBTYPE_WSTR`||  
  
## <a name="see-also"></a>Consulte também  
 [Conjunto de linhas de esquema do XML](xml-for-analysis-schema-rowsets.md)  
  
  
