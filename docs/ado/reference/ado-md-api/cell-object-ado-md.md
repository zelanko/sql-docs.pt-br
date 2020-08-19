---
description: Objeto Cell (ADO MD)
title: Objeto Cell (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cell
helpviewer_keywords:
- Cell object [ADO MD]
ms.assetid: dcc2f044-b785-4a29-9bc5-b673f66eedf9
author: rothja
ms.author: jroth
ms.openlocfilehash: a6cb4d32a4a527cce7bc69eb39f8829bbf5cf58a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88441238"
---
# <a name="cell-object-ado-md"></a>Objeto Cell (ADO MD)
Representa os dados na interseção de coordenadas de eixo contidas em um células.  
  
## <a name="remarks"></a>Comentários  
 Um objeto **Cell** é retornado pela propriedade [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) de um objeto [células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) .  
  
 Com as coleções e propriedades de um objeto **Cell** , você pode fazer o seguinte:  
  
-   Retorne os dados na **célula** com a propriedade [Value](../../../ado/reference/ado-md-api/value-property-ado-md.md) .  
  
-   Retorne a cadeia de caracteres que representa a exibição formatada da propriedade **Value** com a propriedade [FormattedValue](../../../ado/reference/ado-md-api/formattedvalue-property-ado-md.md) .  
  
-   Retorna o valor ordinal da **célula** dentro do **células** com a propriedade [ordinal](../../../ado/reference/ado-md-api/ordinal-property-ado-md-cell.md) .  
  
-   Determine a posição da **célula** dentro do [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) com a coleção [Positions](../../../ado/reference/ado-md-api/positions-collection-ado-md.md) .  
  
-   Recupere outras informações sobre a **célula** com a coleção de [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) padrão do ADO.  
  
 A coleção **Properties** contém propriedades fornecidas pelo provedor. A tabela a seguir lista as propriedades que podem estar disponíveis. A lista de propriedades real pode diferir dependendo da implementação do provedor. Consulte a documentação do seu provedor para obter uma lista mais completa das propriedades disponíveis.  
  
|Nome|Descrição|  
|----------|-----------------|  
|BackColor|Cor da tela de fundo usada ao exibir a célula.|  
|FontFlags|Bitmask detalhando efeitos na fonte.|  
|FontName|Fonte usada para exibir o valor da célula.|  
|FontSize|Tamanho da fonte usado para exibir o valor da célula.|  
|ForeColor|Cor de primeiro plano usada ao exibir a célula.|  
|FormatString|Valor em uma cadeia de caracteres formatada.|  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/cell-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de eixo (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Objeto células (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Coleção Positions (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
