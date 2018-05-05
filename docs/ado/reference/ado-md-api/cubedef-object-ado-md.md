---
title: Objeto CubeDef (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CubeDef
helpviewer_keywords:
- CubeDef object [ADO MD]
ms.assetid: feb2581c-fc41-471c-bb69-29f8a55fda70
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 31e2bf587c19ab8088b0ab702be60fde54247aec
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="cubedef-object-ado-md"></a>Objeto CubeDef (ADO MD)
Representa um cubo de um esquema multidimensional, que contém um conjunto de dimensões relacionadas.  
  
## <a name="remarks"></a>Remarks  
 Com as coleções e propriedades de um **CubeDef** do objeto, você pode fazer o seguinte:  
  
-   Identificar um **CubeDef** com o [nome](../../../ado/reference/ado-md-api/name-property-ado-md.md) propriedade.  
  
-   Retorna uma cadeia de caracteres que descreve o cubo com o [descrição](../../../ado/reference/ado-md-api/description-property-ado-md.md) propriedade.  
  
-   Retornar as dimensões que compõem o cubo com o [dimensões](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md) coleção.  
  
-   Obter informações adicionais sobre o **CubeDef** com ADO padrão [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção.  
  
 O **propriedades** coleção contém propriedades fornecidos pelo provedor. A tabela a seguir lista as propriedades que podem estar disponíveis. A lista de propriedade real pode ser diferente dependendo da implementação do provedor. Consulte a documentação do provedor para obter uma lista mais completa de propriedades disponíveis.  
  
|Nome|Description|  
|----------|-----------------|  
|CatalogName|O nome do catálogo ao qual pertence este cubo.|  
|CreatedOn|Data e hora de criação de cubo.|  
|CubeGUID|GUID do cubo.|  
|CubeName|O nome do cubo.|  
|CubeType|O tipo do cubo.|  
|DataUpdatedBy|ID de usuário da pessoa que está fazendo a última atualização de dados.|  
|Description|Uma descrição significativa do cubo.|  
|LastSchemaUpdate|Data e hora da última atualização do esquema.|  
|SchemaName|O nome do esquema ao qual pertence este cubo.|  
|SchemaUpdatedBy|ID de usuário da pessoa que está fazendo a última atualização do esquema.|  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/cubedef-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de CubeDef (VBScript)](../../../ado/reference/ado-md-api/cubedef-example-vbscript.md)   
 [Objeto de catálogo (ADO MD)](../../../ado/reference/ado-md-api/catalog-object-ado-md.md)   
 [Coleção de CubeDefs (ADO MD)](../../../ado/reference/ado-md-api/cubedefs-collection-ado-md.md)   
 [Coleção de dimensões (ADO MD)](../../../ado/reference/ado-md-api/dimensions-collection-ado-md.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
