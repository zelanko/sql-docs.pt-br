---
title: "O objeto de conjunto de células (ADO MD) | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Cellset
helpviewer_keywords: Cellset object [ADO MD]
ms.assetid: 5e2452c0-cac0-49b2-8099-836c35794d50
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 36bd85cb79d48590cb86a865cfd408db878a1b53
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="cellset-object-ado-md"></a>Objeto de conjunto de células (ADO MD)
Representa os resultados de uma consulta multidimensional. É uma coleção de células selecionadas de cubos ou outros conjuntos de células.  
  
## <a name="remarks"></a>Remarks  
 Dados dentro de um **conjunto de células** é recuperado usando o acesso direto, de matriz. Você pode analisar um membro específico para obter dados sobre esse membro. Por exemplo, o código a seguir retorna a legenda do primeiro membro na primeira posição do primeiro eixo de um conjunto de células nomeado `cst`:  
  
```  
cst.Axes(0).Positions(0).Members(0).Caption  
```  
  
## <a name="remarks"></a>Remarks  
 Não há nenhuma noção de uma célula atual em um conjunto de células. Em vez disso, o [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) propriedade recupera um determinado [célula](../../../ado/reference/ado-md-api/cell-object-ado-md.md) objeto do conjunto de células. Os argumentos do **Item** propriedade determinam qual célula é recuperada. Você pode especificar o valor ordinal exclusivo de uma célula. Você também pode recuperar células usando seus números de posição de cada eixo do conjunto de células. Para obter mais informações sobre a recuperação de células, consulte o [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) propriedade.  
  
 Com as coleções, métodos e propriedades de um **conjunto de células** do objeto, você pode fazer o seguinte:  
  
-   Associar uma conexão aberta com um **conjunto de células** objeto definindo seu [ActiveConnection](../../../ado/reference/ado-md-api/activeconnection-property-ado-md.md) propriedade.  
  
-   Executar e recuperar os resultados de uma consulta multidimensional com o [abrir](../../../ado/reference/ado-md-api/open-method-ado-md.md) método.  
  
-   Recuperar um **célula** do **conjunto de células** com o [Item](../../../ado/reference/ado-md-api/item-property-ado-md-cellset.md) propriedade.  
  
-   Retornar o [eixo](../../../ado/reference/ado-md-api/axis-object-ado-md.md) objetos que definem o **conjunto de células** com o [eixos](../../../ado/reference/ado-md-api/axes-collection-ado-md.md) coleção.  
  
-   Recuperar informações sobre dimensões usadas para filtrar os dados de **conjunto de células** com o [FilterAxis](../../../ado/reference/ado-md-api/filteraxis-property-ado-md.md) propriedade.  
  
-   Retornar ou especificar a consulta usada para definir o **conjunto de células** com o [fonte](../../../ado/reference/ado-md-api/source-property-ado-md.md) propriedade.  
  
-   Retorna o estado atual do **conjunto de células** (abertas, fechadas, executar ou conectar-se) com o [estado](../../../ado/reference/ado-md-api/state-property-ado-md.md) propriedade.  
  
-   Fechar um aberto **conjunto de células** com o [fechar](../../../ado/reference/ado-md-api/close-method-ado-md.md) método.  
  
-   Recuperar informações específicas do provedor sobre o **conjunto de células** com ADO padrão [propriedades](../../../ado/reference/ado-api/properties-collection-ado.md) coleção.  
  
 Esta seção contém o tópico a seguir.  
  
-   [Propriedades, métodos e eventos](../../../ado/reference/ado-md-api/cellset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de conjunto de células (VB)](../../../ado/reference/ado-md-api/cellset-example-vb.md)   
 [Coleção de eixos (ADO MD)](../../../ado/reference/ado-md-api/axes-collection-ado-md.md)   
 [Objeto de célula (ADO MD)](../../../ado/reference/ado-md-api/cell-object-ado-md.md)   
 [Objeto de Conexão (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Coleção Properties (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)
