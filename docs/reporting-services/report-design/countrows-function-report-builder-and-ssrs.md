---
title: "Fun&#231;&#227;o CountRows (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
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
ms.assetid: 5b1c403d-6afd-44c8-b5f6-5ecff2a29a45
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# Fun&#231;&#227;o CountRows (Construtor de Relat&#243;rios e SSRS)
  Retorna o número de linhas no escopo especificado, inclusive as linhas com valores nulos.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Sintaxe  
  
```  
  
CountRows(scope, recursive)  
```  
  
#### Parâmetros  
 *escopo*  
 (**String**) O nome de um conjunto de dados, região de dados ou grupo que contém os itens de relatório a serem contados.  
  
 *recursivos*  
 (**Enumerated Type**) Opcional. **Simple** (padrão) ou **RdlRecursive**. Especifica se a agregação deve ser executada recursivamente.  
  
## Tipo de retorno  
 Retorna um **Integer**.  
  
## Comentários  
 A função**CountRows** conta todas as linhas no escopo especificado incluindo linhas que possuem valores nulos.  
  
 O valor do *scope* não pode ser uma expressão e deve fazer referência ao escopo atual ou a um escopo contentor.  
  
 Para obter mais informações, consulte [Referência de funções agregadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/aggregate-functions-reference-report-builder-and-ssrs.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md).  
  
 Para obter mais informações sobre agregações recursivas, consulte [Criando grupos de hierarquias recursivas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## Exemplo  
 O exemplo de código a seguir mostra uma expressão que calcula o número de linhas em um grupo de linhas denominado `GroupbyCategory` (baseado na expressão `[Category]`).  
  
```  
="Number of rows: " & CountRows("GroupbyCategory")  
```  
  
## Consulte também  
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md)  
  
  