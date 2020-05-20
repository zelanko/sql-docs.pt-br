---
title: Objeto células (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Cellset
helpviewer_keywords:
- Cellset object [ADO MD]
ms.assetid: 5e2452c0-cac0-49b2-8099-836c35794d50
author: rothja
ms.author: jroth
ms.openlocfilehash: e50fb60fbde205171c066380a2c2023d485a5a09
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82761764"
---
# <a name="cellset-object-ado-md"></a>Objeto Cellset (ADO MD)
Representa os resultados de uma consulta multidimensional. É uma coleção de células selecionadas de cubos ou outros células.  
  
## <a name="remarks"></a>Comentários  
 Os dados em um **células** são recuperados usando acesso direto, semelhante à matriz. Você pode fazer uma busca detalhada em um membro específico para obter dados sobre esse membro. Por exemplo, o código a seguir retorna a legenda do primeiro membro na primeira posição no primeiro eixo de um células chamado `cst` :  
  
```  
cst.Axes(0).Positions(0).Members(0).Caption  
```  
  
## <a name="remarks"></a>Comentários  
 Não há nenhuma noção de uma célula atual em um células. Em vez disso, a propriedade [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) recupera um objeto [Cell](../../../ado/reference/ado-md-api/cell-object-ado-md.md) específico do células. Os argumentos da propriedade **Item** determinam qual célula é recuperada. Você pode especificar o valor ordinal exclusivo de uma célula. Você também pode recuperar células usando seus números de posição ao longo de cada eixo do células. Para obter mais informações sobre como recuperar células, consulte a propriedade [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) .  
  
 Com as coleções, métodos e propriedades de um objeto **células** , você pode fazer o seguinte:  
  
-   Associe uma conexão aberta a um objeto **células** definindo sua propriedade [ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md) .  
  
-   Execute e recupere os resultados de uma consulta multidimensional com o método [Open](../../../ado/reference/ado-md-api/open-method-ado-md.md) .  
  
-   Recupere uma **célula** do **células** com a propriedade [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) .  
  
-   Retornar os objetos de [eixo](../../../ado/reference/ado-md-api/axis-object-ado-md.md) que definem o **células** com a coleção de [eixos](../../../ado/reference/ado-md-api/axes-collection-ado-md.md) .  
  
-   Recupere informações sobre as dimensões usadas para filtrar os dados no **células** com a propriedade [FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md) .  
  
-   Retorne ou especifique a consulta usada para definir o **células** com a propriedade [Source](../../../ado/reference/ado-md-api/source-property-ado-md.md) .  
  
-   Retornar o estado atual do **células** (abrir, fechar, executar ou conectar) com a propriedade [State](../../../ado/reference/ado-md-api/state-property-ado-md.md) .  
  
-   Feche um **células** aberto com o método [Close](../../../ado/reference/ado-md-api/close-method-ado-md.md) .  
  
-   Recupere informações específicas do provedor sobre o **células** com a coleção de [Propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) padrão do ADO.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/cellset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de células (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Coleção Axes (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)   
 [Objeto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Objeto de conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
