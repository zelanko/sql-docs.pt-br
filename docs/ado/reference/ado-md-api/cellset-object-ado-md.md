---
title: Objeto Cellset (ADO MD) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 57b570b93d4e8a6cf10d879659f0886e1c6f0c8e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47601664"
---
# <a name="cellset-object-ado-md"></a>Objeto Cellset (ADO MD)
Representa os resultados de uma consulta multidimensional. É uma coleção de células selecionadas de cubos ou outros conjuntos de células.  
  
## <a name="remarks"></a>Comentários  
 Dados dentro de um **conjunto de células** é recuperado usando o acesso direto, o tipo de matriz. Fazer drill down de um membro específico para obter dados sobre esse membro. Por exemplo, o código a seguir retorna a legenda do primeiro membro na primeira posição do primeiro eixo de um conjunto de células nomeado `cst`:  
  
```  
cst.Axes(0).Positions(0).Members(0).Caption  
```  
  
## <a name="remarks"></a>Comentários  
 Não há nenhuma noção de uma célula atual dentro de um conjunto de células. Em vez disso, o [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) propriedade recupera um determinado [célula](../../../ado/reference/ado-md-api/cell-object-ado-md.md) objeto do conjunto de células. Os argumentos do **Item** propriedade determinar qual célula é recuperada. Você pode especificar o valor ordinal exclusivo de uma célula. Você também pode recuperar as células usando seus números de posição de cada eixo do conjunto de células. Para obter mais informações sobre como recuperar as células, consulte o [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) propriedade.  
  
 Com as coleções, métodos e propriedades de um **conjunto de células** do objeto, você pode fazer o seguinte:  
  
-   Associar uma conexão aberta com um **Cellset** objeto definindo suas [ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md) propriedade.  
  
-   Executar e recuperar os resultados de uma consulta multidimensional com o [abrir](../../../ado/reference/ado-md-api/open-method-ado-md.md) método.  
  
-   Recuperar um **célula** da **conjunto de células** com o [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) propriedade.  
  
-   Retornar o [eixo](../../../ado/reference/ado-md-api/axis-object-ado-md.md) objetos que definem a **conjunto de células** com o [eixos](../../../ado/reference/ado-md-api/axes-collection-ado-md.md) coleção.  
  
-   Recuperar informações sobre as dimensões usadas para filtrar os dados de **conjunto de células** com o [FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md) propriedade.  
  
-   Retornar ou especificar a consulta usada para definir a **Cellset** com o [origem](../../../ado/reference/ado-md-api/source-property-ado-md.md) propriedade.  
  
-   Retornar o estado atual do **Cellset** (abertas, fechadas, executar ou conectar-se) com o [estado](../../../ado/reference/ado-md-api/state-property-ado-md.md) propriedade.  
  
-   Fechar um aberto **Cellset** com o [fechar](../../../ado/reference/ado-md-api/close-method-ado-md.md) método.  
  
-   Recuperar informações específicas do provedor sobre o **Cellset** com o padrão ADO [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/cellset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de conjunto de células (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Coleção Axes (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)   
 [Objeto Cell (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
