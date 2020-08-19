---
description: Objetos do ADO MD
title: Objetos de ADO MD | Microsoft Docs
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 54e7eae0aaab754dbc57f1001263ea20c0bd8999
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441348"
---
# <a name="ado-md-objects"></a>Objetos do ADO MD

|Objeto|Descrição|  
|-|-|  
|[Axis](../../../ado/reference/ado-md-api/axis-object-ado-md.md)|Representa um eixo de posição ou de filtro de um células, que contém os membros selecionados de uma ou mais dimensões.|  
|[Catálogo](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)|Contém informações de esquema multidimensional (ou seja, cubos e dimensões subjacentes, hierarquias, níveis e membros) específicas para um provedor de dados multidimensional (MDP).|  
|[Célula](../../../ado/reference/ado-md-api/cell-object-ado-md.md)|Representa os dados na interseção de coordenadas de eixo, contidas em um células.|  
|[Células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)|Representa os resultados de uma consulta multidimensional. É uma coleção de células selecionadas de cubos ou outros células.|  
|[CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md)|Representa um cubo de um esquema multidimensional que contém um conjunto de dimensões relacionadas.|  
|[Dimensão](../../../ado/reference/ado-md-api/dimension-object-ado-md.md)|Representa uma das dimensões de um cubo multidimensional que contém uma ou mais hierarquias de membros.|  
|[Hierarquia](../../../ado/reference/ado-md-api/hierarchy-object-ado-md.md)|Representa uma maneira na qual os membros de uma dimensão podem ser agregados ou "acumulados". Uma dimensão pode ser agregada ao longo de uma ou mais hierarquias.|  
|[Level](../../../ado/reference/ado-md-api/level-object-ado-md.md)|Contém um conjunto de membros, cada um dos quais tem a mesma classificação em uma hierarquia.|  
|[Membro](../../../ado/reference/ado-md-api/member-object-ado-md.md)|Representa um membro de um nível em um cubo, os filhos de um membro de um nível ou um membro de uma posição ao longo de um eixo de um células.|  
|[Posição](../../../ado/reference/ado-md-api/position-object-ado-md.md)|Representa um conjunto de um ou mais membros de dimensões diferentes que define um ponto ao longo de um eixo.|  
  
 Além disso, o objeto de **Catálogo** está conectado a um objeto de **conexão** ADO, que está incluído na biblioteca padrão do ADO:  
  
|Objeto|Descrição|  
|------------|-----------------|  
|[Conexão](../../../ado/reference/ado-api/connection-object-ado.md)|Representa uma conexão aberta com uma fonte de dados.|  
  
 As relações entre esses objetos são ilustradas no [modelo de objeto ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md).  
  
 Muitos objetos ADO MD podem estar contidos em uma coleção correspondente. Por exemplo, um objeto [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) pode estar contido em uma coleção [CubeDefs](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md) de um **Catálogo**. Para obter mais informações, consulte [coleções de ADO MD](../../../ado/reference/ado-md-api/ado-md-collections.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Referência de API de ADO MD](../../../ado/reference/ado-md-api/ado-md-api-reference.md)   
 [Exemplos de código de ADO MD](../../../ado/reference/ado-md-api/ado-md-code-examples.md)   
 [ADO MD coleções](../../../ado/reference/ado-md-api/ado-md-collections.md)   
 [ADO MD constantes enumeradas](../../../ado/reference/ado-md-api/ado-md-enumerated-constants.md)   
 [Métodos de ADO MD](../../../ado/reference/ado-md-api/ado-md-methods.md)   
 [Modelo de objeto ADO MD](../../../ado/reference/ado-md-api/ado-md-object-model.md)   
 [Propriedades do ADO MD](../../../ado/reference/ado-md-api/ado-md-properties.md)
