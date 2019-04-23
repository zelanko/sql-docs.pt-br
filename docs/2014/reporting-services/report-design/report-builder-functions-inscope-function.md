---
title: Função InScope (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ecb91bd2a4b570a1e625a013270e59a121e6430a
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59934772"
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
  
## <a name="remarks"></a>Comentários  
 O `InScope` função testa o escopo da instância atual de um item de relatório para a associação no escopo especificado o *escopo*parâmetro.  
  
 O*Scope* não pode ser uma expressão.  
  
 Um uso típico da função `InScope` é em regiões de dados que possuem escopo dinâmico. Por exemplo, `InScope` pode ser usada em um link de detalhamento em células de uma região de dados para fornecer um nome de relatório diferente e conjuntos de parâmetros diferentes, dependendo da célula clicada. Um exemplo disso é o seguinte:  
  
-   A expressão a seguir, usada como o nome do relatório em um link de drillthrough, abrirá o relatório `ProductDetail` , se a célula clicada estiver no grupo `Month` , e o relatório `ProductSummary` se não estiver.  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   A expressão a seguir, usada na propriedade `Omit` de um parâmetro de relatório detalhado, passará o parâmetro para o relatório de destino somente se a célula clicada estiver no grupo `Product`.  
  
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
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
