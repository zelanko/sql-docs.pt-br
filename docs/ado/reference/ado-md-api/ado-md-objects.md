---
title: Objetos do ADO MD | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO MD, objects
- objects [ADO MD]
ms.assetid: 2a32e873-3282-4520-a7ed-89493f1da80e
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 4a0fa75a3b03b2cb5f2a31ed3bdf3756e1c64b01
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="ado-md-objects"></a>Objetos do ADO MD
|||  
|-|-|  
|[Axis](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|Representa uma posição ou o eixo do filtro de um conjunto de células que contém os membros selecionados de uma ou mais dimensões.|  
|[Catálogo](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|Contém multidimensional informações de esquema (ou seja, cubos e subjacente dimensões, hierarquias, níveis e membros) específicas para um provedor de dados multidimensionais (MDP).|  
|[Célula](../../../ado/reference/ado-md-api/cell-object-ado-md.md)|Representa os dados na interseção de coordenadas de eixo, contido em um conjunto de células.|  
|[Conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|Representa os resultados de uma consulta multidimensional. É uma coleção de células selecionadas de cubos ou outros conjuntos de células.|  
|[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|Representa um cubo de um esquema multidimensional, que contém um conjunto de dimensões relacionadas.|  
|[Dimension](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|Representa uma das dimensões de um cubo multidimensional, que contém uma ou mais hierarquias de membros.|  
|[Hierarchy](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|Representa uma forma em que os membros de uma dimensão podem ser agregados ou "acumulados". Uma dimensão pode ser agregada a uma ou mais hierarquias.|  
|[Level](../../../ado/reference/ado-md-api/level-object-ado-md.md)|Contém um conjunto de membros, cada um deles tem a mesma classificação dentro de uma hierarquia.|  
|[Membro](../../../ado/reference/ado-md-api/member-object-ado-md.md)|Representa um membro de um nível em um cubo, os filhos de um membro de um nível ou membro de uma posição em um eixo de um conjunto de células.|  
|[Posição](../../../ado/reference/ado-md-api/position-object-ado-md.md)|Representa um conjunto de um ou mais membros de diferentes dimensões que define um ponto em um eixo.|  
  
 Além disso, o **catálogo** objeto está conectado a um ADO **Conexão** objeto, que é incluído com a biblioteca do ADO padrão:  
  
|Objeto|Description|  
|------------|-----------------|  
|[Conexão](../../../ado/reference/ado-api/connection-object-ado.md)|Representa uma conexão aberta com uma fonte de dados.|  
  
 As relações entre esses objetos estão ilustradas no [modelo de objeto ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md).  
  
 Muitos objetos ADO MD podem estar contidos em uma coleção correspondente. Por exemplo, um [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) objeto pode estar contido em um [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) coleção de um **catálogo**. Para obter mais informações, consulte [ADO MD coleções](../../../ado/reference/ado-md-api/ado-md-collections.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API do ADO MD](../../../ado/reference/ado-md-api/ado-md-api-reference.md)   
 [Exemplos de código do ADO MD](../../../ado/reference/ado-md-api/ado-md-code-examples.md)   
 [Coleções do ADO MD](../../../ado/reference/ado-md-api/ado-md-collections.md)   
 [Constantes enumeradas do ADO MD](../../../ado/reference/ado-md-api/ado-md-enumerated-constants.md)   
 [Métodos do ADO MD](../../../ado/reference/ado-md-api/ado-md-methods.md)   
 [Modelo de objeto ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [Propriedades do ADO MD](../../../ado/reference/ado-md-api/ado-md-properties.md)
