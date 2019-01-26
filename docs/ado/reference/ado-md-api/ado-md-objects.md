---
title: Objetos do ADO MD | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO MD, objects
- objects [ADO MD]
ms.assetid: 2a32e873-3282-4520-a7ed-89493f1da80e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 42b0aed3c63b1303e4d8743ea441348c351be822
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044909"
---
# <a name="ado-md-objects"></a>Objetos do ADO MD

|||  
|-|-|  
|[Axis](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|Representa um posicional ou eixo do filtro de um conjunto de células que contêm membros selecionados de uma ou mais dimensões.|  
|[Catálogo](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|Contém multidimensional informações de esquema (ou seja, cubos e subjacente dimensões, hierarquias, níveis e membros) específicas para um provedor de dados multidimensional (MDP).|  
|[Cell](../../../ado/reference/ado-md-api/cell-object-ado-md.md)|Representa os dados na interseção das coordenadas do eixo, contido em um conjunto de células.|  
|[Conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|Representa os resultados de uma consulta multidimensional. É uma coleção de células selecionadas de cubos ou outros conjuntos de células.|  
|[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|Representa um cubo de um esquema multidimensional, que contém um conjunto de dimensões relacionadas.|  
|[Dimension](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|Representa uma das dimensões de um cubo multidimensional, que contém uma ou mais hierarquias de membros.|  
|[Hierarchy](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|Representa uma forma em que os membros de uma dimensão podem ser agregados ou "acumulados". Uma dimensão pode ser agregada a uma ou mais hierarquias.|  
|[Level](../../../ado/reference/ado-md-api/level-object-ado-md.md)|Contém um conjunto de membros, cada um deles tem a mesma classificação dentro de uma hierarquia.|  
|[Membro](../../../ado/reference/ado-md-api/member-object-ado-md.md)|Representa um membro de um nível em um cubo, os filhos de um membro de um nível ou membro de uma posição ao longo do eixo de um conjunto de células.|  
|[Posição](../../../ado/reference/ado-md-api/position-object-ado-md.md)|Representa um conjunto de um ou mais membros de diferentes dimensões que define um ponto ao longo do eixo.|  
  
 Além disso, o **catálogo** objeto está conectado a um ADO **Conexão** objeto, que é incluído com a biblioteca do ADO padrão:  
  
|Object|Descrição|  
|------------|-----------------|  
|[Conexão](../../../ado/reference/ado-api/connection-object-ado.md)|Representa uma conexão aberta com uma fonte de dados.|  
  
 As relações entre esses objetos são ilustradas na [modelo de objeto do ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md).  
  
 Muitos objetos do ADO MD podem estar contidos em uma coleção correspondente. Por exemplo, uma [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) objeto pode estar contido em um [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) coleção de um **catálogo**. Para obter mais informações, consulte [coleções do ADO MD](../../../ado/reference/ado-md-api/ado-md-collections.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência de API do ADO MD](../../../ado/reference/ado-md-api/ado-md-api-reference.md)   
 [Exemplos de código do ADO MD](../../../ado/reference/ado-md-api/ado-md-code-examples.md)   
 [Coleções do ADO MD](../../../ado/reference/ado-md-api/ado-md-collections.md)   
 [Constantes enumeradas do ADO MD](../../../ado/reference/ado-md-api/ado-md-enumerated-constants.md)   
 [Métodos do ADO MD](../../../ado/reference/ado-md-api/ado-md-methods.md)   
 [Modelo de objeto do ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [Propriedades do ADO MD](../../../ado/reference/ado-md-api/ado-md-properties.md)
