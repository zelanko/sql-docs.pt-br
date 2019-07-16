---
title: Objeto Hierarchy (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Hierarchy
helpviewer_keywords:
- Hierarchy object [ADO MD]
ms.assetid: 034af340-ac79-494e-ba5e-2b57da1cb9de
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 35e02e4823d0a3abf245e1885b95176d6350d712
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67949690"
---
# <a name="hierarchy-object-ado-md"></a>Objeto Hierarchy (ADO MD)
Representa uma forma em que os membros de um [dimensão](../../../ado/reference/ado-md-api/dimension-object-ado-md.md) podem ser agregados ou "acumulados". Uma dimensão pode ser agregada a uma ou mais hierarquias.  
  
## <a name="remarks"></a>Comentários  
 Com as coleções e propriedades de um **hierarquia** do objeto, você pode fazer o seguinte:  
  
-   Identificar o **hierarquia** com o [nome](../../../ado/reference/ado-md-api/name-property-ado-md.md) e [UniqueName](../../../ado/reference/ado-md-api/uniquename-property-ado-md.md) propriedades.  
  
-   Retornar uma cadeia de caracteres significativa que descreve o **hierarquia** com o [descrição](../../../ado/reference/ado-md-api/description-property-ado-md.md) propriedade.  
  
-   Retornar o [nível](../../../ado/reference/ado-md-api/level-object-ado-md.md) objetos que compõem o **hierarquia** com o [níveis](../../../ado/reference/ado-md-api/levels-collection-ado-md.md) coleção.  
  
-   Use o padrão ADO [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção para obter informações adicionais sobre o **hierarquia** objeto.  
  
 O **propriedades** coleção contém propriedades fornecidos pelo provedor. A tabela a seguir lista as propriedades que podem estar disponíveis. A lista de propriedades reais pode diferir dependendo após a implementação do provedor. Consulte a documentação do seu provedor para obter uma lista completa de propriedades disponíveis.  
  
|Name|Descrição|  
|----------|-----------------|  
|AllMember|O membro no nível mais alto na hierarquia do pacote cumulativo de atualizações.|  
|CatalogName|O nome do catálogo ao qual pertence este cubo.|  
|CubeName|O nome do cubo.|  
|DefaultMember|O nome exclusivo do membro padrão para essa hierarquia.|  
|Descrição|Uma descrição significativa da hierarquia.|  
|DimensionType|O tipo de dimensão à qual pertence essa hierarquia.|  
|DimensionUniqueName|O nome não ambíguo da dimensão.|  
|HierarchyCaption|Um rótulo ou legenda associada à hierarquia.|  
|HierarchyCardinality|O número de membros na hierarquia.|  
|HierarchyGUID|O GUID da hierarquia.|  
|HierarchyName|O nome da hierarquia.|  
|HierarchyUniqueName|O nome não ambíguo da hierarquia.|  
|SchemaName|O nome do esquema ao qual pertence este cubo.|  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/hierarchy-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Objeto de dimensão (ADO MD)](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)   
 [Coleção hierarquias (ADO MD)](../../../ado/reference/ado-md-api/hierarchies-collection-ado-md.md)   
 [Coleção Levels (ADO MD)](../../../ado/reference/ado-md-api/levels-collection-ado-md.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
