---
description: Objeto CubeDef (ADO MD)
title: Objeto CubeDef (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- CubeDef
helpviewer_keywords:
- CubeDef object [ADO MD]
ms.assetid: feb2581c-fc41-471c-bb69-29f8a55fda70
author: rothja
ms.author: jroth
ms.openlocfilehash: f2a25f9a964e6a8e9644eb737897dd15e3948974
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778255"
---
# <a name="cubedef-object-ado-md"></a>Objeto CubeDef (ADO MD)
Representa um cubo de um esquema multidimensional que contém um conjunto de dimensões relacionadas.  
  
## <a name="remarks"></a>Comentários  
 Com as coleções e propriedades de um objeto **CubeDef** , você pode fazer o seguinte:  
  
-   Identifique um **CubeDef** com a propriedade [Name](./name-property-ado-md.md) .  
  
-   Retornar uma cadeia de caracteres que descreve o cubo com a propriedade [Description](./description-property-ado-md.md) .  
  
-   Retorne as dimensões que compõem o cubo com a coleção [Dimensions](./dimensions-collection-ado-md.md) .  
  
-   Obtenha informações adicionais sobre o **CubeDef** com a coleção de [Propriedades](../ado-api/properties-collection-ado.md) padrão do ADO.  
  
 A coleção **Properties** contém propriedades fornecidas pelo provedor. A tabela a seguir lista as propriedades que podem estar disponíveis. A lista de propriedades real pode diferir dependendo da implementação do provedor. Consulte a documentação do seu provedor para obter uma lista mais completa das propriedades disponíveis.  
  
|Nome|Descrição|  
|----------|-----------------|  
|CatalogName|O nome do catálogo ao qual este cubo pertence.|  
|CreatedOn|Data e hora da criação do cubo.|  
|CubeGUID|GUID do cubo.|  
|CubeName|O nome do cubo.|  
|CubeType|O tipo do cubo.|  
|DataUpdatedBy|ID de usuário da pessoa que está fazendo a última atualização de dados.|  
|Descrição|Uma descrição significativa do cubo.|  
|LastSchemaUpdate|Data e hora da última atualização do esquema.|  
|SchemaName|O nome do esquema ao qual este cubo pertence.|  
|SchemaUpdatedBy|ID de usuário da pessoa que está fazendo a última atualização de esquema.|  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](./cubedef-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de CubeDef (VBScript)](./cubedef-example-vbscript.md)   
 [Objeto de catálogo (ADO MD)](./catalog-object-ado-md.md)   
 [Coleção CubeDefs (ADO MD)](./cubedefs-collection-ado-md.md)   
 [Coleção Dimensions (ADO MD)](./dimensions-collection-ado-md.md)   
 [Coleção Properties (ADO)](../ado-api/properties-collection-ado.md)