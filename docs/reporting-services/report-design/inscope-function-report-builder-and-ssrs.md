---
title: "Fun&#231;&#227;o InScope (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/29/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a8cd209a-e5d3-4dce-ab2d-f271f6c54955
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# Fun&#231;&#227;o InScope (Construtor de Relat&#243;rios e SSRS)
  Indica se a instância atual de um item está no escopo especificado.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Sintaxe  
  
```  
InScope(scope)  
```  
  
#### Parâmetros  
 *escopo*  
 (**String**) O nome de um conjunto de dados, região de dados ou grupo que especifica um escopo.  
  
## Tipo de retorno  
 Retorna um **Booliano**.  
  
## Comentários  
 A função **InScope** testa o escopo da instância atual de um item de relatório para a associação no escopo especificado pelo parâmetro *scope*.  
  
 O*Scope* não pode ser uma expressão.  
  
 Um uso típico da função **InScope** é em regiões de dados que têm escopo dinâmico. Por exemplo, **InScope** pode ser usada em um link de drillthrough em células de uma região de dados para fornecer um nome de relatório diferente e conjuntos de parâmetros diferentes, dependendo da célula clicada. Um exemplo disso é o seguinte:  
  
-   A expressão a seguir, usada como o nome do relatório em um link de drillthrough, abrirá o relatório `ProductDetail`, se a célula clicada estiver no grupo `Month`, e o relatório `ProductSummary` se não estiver.  
  
    ```  
    =Iif(InScope("Month"), "ProductDetail", "ProductSummary")  
    ```  
  
-   A expressão a seguir, usada na propriedade **Omit** de um parâmetro de relatório de drillthrough, passará o parâmetro para o relatório de destino somente se a célula clicada estiver no grupo `Product`.  
  
    ```  
    =Not(InScope("Product"))  
    ```  
  
 Para obter mais informações, consulte [Referência de funções agregadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/aggregate-functions-reference-report-builder-and-ssrs.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md).  
  
## Exemplo  
 O exemplo de código a seguir indica se a instância atual do item está no conjunto de dados, região de dados ou escopo do grupo `Product`.  
  
```  
=InScope("Product")  
```  
  
## Consulte também  
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md)  
  
  