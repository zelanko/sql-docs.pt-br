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
ms.openlocfilehash: 28058d792b0525aafe8850158a71afcc4423b38f
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88778325"
---
# <a name="cell-object-ado-md"></a>Objeto Cell (ADO MD)
Representa os dados na interseção de coordenadas de eixo contidas em um células.  
  
## <a name="remarks"></a>Comentários  
 Um objeto **Cell** é retornado pela propriedade [Item](./item-property-ado-md-cellset.md) de um objeto [células](./cellset-object-ado-md.md) .  
  
 Com as coleções e propriedades de um objeto **Cell** , você pode fazer o seguinte:  
  
-   Retorne os dados na **célula** com a propriedade [Value](./value-property-ado-md.md) .  
  
-   Retorne a cadeia de caracteres que representa a exibição formatada da propriedade **Value** com a propriedade [FormattedValue](./formattedvalue-property-ado-md.md) .  
  
-   Retorna o valor ordinal da **célula** dentro do **células** com a propriedade [ordinal](./ordinal-property-ado-md-cell.md) .  
  
-   Determine a posição da **célula** dentro do [CubeDef](./cubedef-object-ado-md.md) com a coleção [Positions](./positions-collection-ado-md.md) .  
  
-   Recupere outras informações sobre a **célula** com a coleção de [Propriedades](../ado-api/properties-collection-ado.md) padrão do ADO.  
  
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
  
-   [Propriedades, métodos e eventos](./cell-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de eixo (VBScript)](./axis-example-vbscript.md)   
 [Objeto células (ADO MD)](./cellset-object-ado-md.md)   
 [Coleção Positions (ADO MD)](./positions-collection-ado-md.md)   
 [Coleção Properties (ADO)](../ado-api/properties-collection-ado.md)