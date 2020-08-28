---
description: Objeto Cellset (ADO MD)
title: Objeto células (ADO MD) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 411ed21d5fecf5c9791a5d96aac60724e7446958
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2020
ms.locfileid: "88987147"
---
# <a name="cellset-object-ado-md"></a>Objeto Cellset (ADO MD)
Representa os resultados de uma consulta multidimensional. É uma coleção de células selecionadas de cubos ou outros células.  
  
## <a name="remarks"></a>Comentários  
 Os dados em um **células** são recuperados usando acesso direto, semelhante à matriz. Você pode fazer uma busca detalhada em um membro específico para obter dados sobre esse membro. Por exemplo, o código a seguir retorna a legenda do primeiro membro na primeira posição no primeiro eixo de um células chamado `cst` :  
  
```  
cst.Axes(0).Positions(0).Members(0).Caption  
```  
  
 Não há nenhuma noção de uma célula atual em um células. Em vez disso, a propriedade [Item](./item-property-ado-md-cellset.md) recupera um objeto [Cell](./cell-object-ado-md.md) específico do células. Os argumentos da propriedade **Item** determinam qual célula é recuperada. Você pode especificar o valor ordinal exclusivo de uma célula. Você também pode recuperar células usando seus números de posição ao longo de cada eixo do células. Para obter mais informações sobre como recuperar células, consulte a propriedade [Item](./item-property-ado-md-cellset.md) .  
  
 Com as coleções, métodos e propriedades de um objeto **células** , você pode fazer o seguinte:  
  
-   Associe uma conexão aberta a um objeto **células** definindo sua propriedade [ActiveConnection](./activeconnection-property-ado-md.md) .  
  
-   Execute e recupere os resultados de uma consulta multidimensional com o método [Open](./open-method-ado-md.md) .  
  
-   Recupere uma **célula** do **células** com a propriedade [Item](./item-property-ado-md-cellset.md) .  
  
-   Retornar os objetos de [eixo](./axis-object-ado-md.md) que definem o **células** com a coleção de [eixos](./axes-collection-ado-md.md) .  
  
-   Recupere informações sobre as dimensões usadas para filtrar os dados no **células** com a propriedade [FilterAxis](./filteraxis-property-ado-md.md) .  
  
-   Retorne ou especifique a consulta usada para definir o **células** com a propriedade [Source](./source-property-ado-md.md) .  
  
-   Retornar o estado atual do **células** (abrir, fechar, executar ou conectar) com a propriedade [State](./state-property-ado-md.md) .  
  
-   Feche um **células** aberto com o método [Close](./close-method-ado-md.md) .  
  
-   Recupere informações específicas do provedor sobre o **células** com a coleção de [Propriedades](../ado-api/properties-collection-ado.md) padrão do ADO.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](./cellset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de células (VB)](./cellset-example-vb.md)   
 [Coleção Axes (ADO MD)](./axes-collection-ado-md.md)   
 [Objeto Cell (ADO MD)](./cell-object-ado-md.md)   
 [Objeto de conexão (ADO)](../ado-api/connection-object-ado.md)   
 [Coleção Properties (ADO)](../ado-api/properties-collection-ado.md)