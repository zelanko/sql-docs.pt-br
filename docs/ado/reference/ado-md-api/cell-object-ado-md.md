---
title: Objeto (ADO MD) da célula | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bbf97a4095f2295b8851f87ba20ab083938e70ed
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947743"
---
# <a name="cell-object-ado-md"></a>Objeto Cell (ADO MD)
Representa os dados na interseção de coordenadas do eixo contidos em um conjunto de células.  
  
## <a name="remarks"></a>Comentários  
 Um **célula** objeto é retornado pela [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) propriedade de um [conjunto de células](../../../ado/reference/ado-md-api/cellset-object-ado-md.md) objeto.  
  
 Com as coleções e propriedades de um **célula** do objeto, você pode fazer o seguinte:  
  
-   Retornar os dados de **célula** com o [valor](../../../ado/reference/ado-md-api/value-property-ado-md.md) propriedade.  
  
-   Retornar a cadeia de caracteres que representa a exibição formatada dos **valor** propriedade com o [FormattedValue](../../../ado/reference/ado-md-api/formattedvalue-property-ado-md.md) propriedade.  
  
-   Retornar o valor ordinal do **célula** dentro de **conjunto de células** com o [Ordinal](../../../ado/reference/ado-md-api/ordinal-property-ado-md-cell.md) propriedade.  
  
-   Determinar a posição do **célula** dentro a [CubeDef](../../../ado/reference/ado-md-api/cubedef-object-ado-md.md) com o [posições](../../../ado/reference/ado-md-api/positions-collection-ado-md.md) coleção.  
  
-   Recuperar outras informações sobre o **célula** com o padrão ADO [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção.  
  
 O **propriedades** coleção contém propriedades fornecidos pelo provedor. A tabela a seguir lista as propriedades que podem estar disponíveis. A lista de propriedades reais pode diferir dependendo após a implementação do provedor. Consulte a documentação do seu provedor para obter uma lista completa de propriedades disponíveis.  
  
|Nome|Descrição|  
|----------|-----------------|  
|BackColor|Cor de plano de fundo usada ao exibir a célula.|  
|FontFlags|Bitmask que detalha os efeitos da fonte.|  
|FontName|Fonte usada para exibir o valor da célula.|  
|FontSize|Tamanho da fonte usado para exibir o valor da célula.|  
|ForeColor|Cor de primeiro plano usada ao exibir a célula.|  
|FormatString|Valor em uma cadeia de caracteres formatada.|  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/cell-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo Axis (VBScript)](../../../ado/reference/ado-md-api/axis-example-vbscript.md)   
 [Objeto Cellset (ADO MD)](../../../ado/reference/ado-md-api/cellset-object-ado-md.md)   
 [Coleção Positions (ADO MD)](../../../ado/reference/ado-md-api/positions-collection-ado-md.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
