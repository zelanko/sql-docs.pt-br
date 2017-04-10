---
title: "Filtros comumente usados (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "parâmetros multivalor [Reporting Services]"
  - "parâmetros com valor simples [Reporting Services]"
  - "parâmetros [Reporting Services], de múltiplos valores"
  - "valores válidos [Reporting Services]"
ms.assetid: cb70d0cd-707b-4de5-b39f-e4eb57d316aa
caps.latest.revision: 36
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 36
---
# Filtros comumente usados (Construtor de Relat&#243;rios e SSRS)
  Para criar um filtro, é necessário especificar uma ou mais equações de filtro. As equações de filtro incluem uma expressão, um tipo de dados, um operador e um valor. Este tópico traz exemplos de filtros que são utilizados com frequência.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Exemplos de filtro  
 A tabela a seguir mostra exemplo de equações de filtro que usam diferentes tipos de dados e operadores. O escopo da comparação é determinado pelo item de relatório para o qual é definido um filtro. Por exemplo, no caso de um filtro definido em um conjunto de dados, **TOP % 10** representa os principais 10% de valores do conjunto de dados; no caso de um filtro definido em um grupo, **TOP % 10** são os principais 10% de valores do grupo.  
  
|Expressão simples|Tipo de Dados|Operador|Value|Description|  
|-----------------------|---------------|--------------|-----------|-----------------|  
|`[SUM(Quantity)]`|**Integer**|**>**|`7`|Inclui valores de dados maiores que 7.|  
|`[SUM(Quantity)]`|**Integer**|**TOP N**|`10`|Inclui os 10 principais valores de dados.|  
|`[SUM(Quantity)]`|**Integer**|**TOP %**|`20`|Inclui os principais 20% de valores de dados.|  
|`[Sales]`|**Texto**|**>**|`=CDec(100)`|Inclui todos os valores do tipo System.Decimal (tipos de dados “money” do SQL) maiores que $100.|  
|`[OrderDate]`|**DateTime**|**>**|`2088-01-01`|Inclui todas as datas, desde 1º de janeiro de 2008 até a presente data.|  
|`[OrderDate]`|**DateTime**|**BETWEEN**|`2008-01-01`<br /><br /> `2008-02-01`|Inclui as datas de 1o. de janeiro de 2008 até, e incluindo, 1º de fevereiro de 2008.|  
|`[Territory]`|**Texto**|**LIKE**|`*east`|Todos os nomes de território que terminam com "leste".|  
|`[Territory]`|**Texto**|**LIKE**|`%o%th*`|Todos os nomes de território que incluem Norte e Sul no início do nome.|  
|`=LEFT(Fields!Subcat.Value,1)`|**Texto**|**IN**|`B, C, T`|Todos os valores de subcategorias que começam com as letras B, C ou T.|  
  
## Exemplos com parâmetros de relatório  
 A tabela a seguir contém exemplos de expressão de filtro que inclui uma referência de parâmetro de um só valor ou multivalor.  
  
|Tipo de parâmetro|Expressão (filtro)|Operador|Value|Tipo de Dados|  
|--------------------|---------------------------|--------------|-----------|---------------|  
|Um único valor|`[EmployeeID]`|=|`[@EmployeeID]`|Integer|  
|Multivalor|`[EmployeeID]`|IN|`[@EmployeeID]`|Integer|  
  
## Consulte também  
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Adicionar filtros de conjunto de dados, de região de dados e de grupo &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/add dataset filters, data region filters, and group filters.md)   
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)  
  
  