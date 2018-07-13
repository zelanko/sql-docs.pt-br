---
title: Função InScope (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: ebf90710587c73206408dfda1429a90b58f39621
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37228836"
---
# <a name="inscope-function-report-builder-and-ssrs"></a>Função InScope (Construtor de Relatórios e SSRS)
  Indica se a instância atual de um item está no escopo especificado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
InScope(scope)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *escopo*  
 (`String`) O nome de um conjunto de dados, região de dados ou grupo que especifica um escopo.  
  
## <a name="return-type"></a>Tipo de retorno  
 Retorna um `Boolean`.  
  
## <a name="remarks"></a>Remarks  
 O `InScope` função testa o escopo da instância atual de um item de relatório para a associação no escopo especificado o *escopo*parâmetro.  
  
 O*Scope* não pode ser uma expressão.  
  
 Um uso típico para o `InScope` função é em regiões de dados que têm dinâmico de escopo. Por exemplo, `InScope` pode ser usado em um link de detalhamento em células de uma região de dados para fornecer um relatório diferente nome e diferentes conjuntos de parâmetros dependendo de qual célula é clicada. Um exemplo disso é o seguinte:  
  
-   A expressão a seguir, usada como o nome do relatório em um link de drillthrough, abrirá o relatório `ProductDetail` , se a célula clicada estiver no grupo `Month` , e o relatório `ProductSummary` se não estiver.  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   A expressão a seguir, usada na `Omit` propriedade de um parâmetro de relatório de detalhamento, passará o parâmetro para o relatório de destino somente se a célula clicada estiver no `Product` grupo.  
  
    ```  
    =Not(InScope("Product"))  
    ```  
  
 Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir indica se a instância atual do item está no conjunto de dados, região de dados ou escopo do grupo `Product` .  
  
```  
=InScope("Product")  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usos de expressões em relatórios &#40;relatórios e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
