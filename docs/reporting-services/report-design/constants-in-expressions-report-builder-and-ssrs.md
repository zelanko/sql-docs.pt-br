---
title: "Constantes em express&#245;es (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b8ae650b-0f46-4848-b62b-15f8a40751b8
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 8
---
# Constantes em express&#245;es (Construtor de Relat&#243;rios e SSRS)
  Uma constante consiste em texto literal ou texto predefinido. O processador de relatório tem acesso às constantes predefinidas; portanto, quando elas são incluídas em uma expressão, os valores que elas representam são substituídos na expressão antes de ela ser avaliada.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Texto literal  
 Em uma expressão, texto literal é o texto que está entre aspas duplas. Você também poderá digitar o texto diretamente em uma caixa de texto sem aspas duplas, se ele não fizer parte de uma expressão. Se o valor da caixa de texto não começar com um sinal de igual (=), o texto será tratado como texto literal. A tabela a seguir mostra vários exemplos de texto literal em uma expressão.  
  
|Constante|Texto de exibição|Texto de expressão|  
|--------------|------------------|---------------------|  
|Execução do relatório em:|<\<Expr>>|`="Report run at: " & Globals!ExecutionTime`|  
|Ciclos da Adventure Works|Ciclos da Adventure Works|Ciclos da Adventure Works|  
|[Texto de exibição entre colchetes]|\\[Texto de exibição entre colchetes\\]|[Texto de exibição entre colchetes]|  
  
## Constantes RDL  
 É possível usar constantes definidas em linguagem RDL (Report Definition Language) em uma expressão. Na caixa de diálogo **Expressão** , as constantes são exibidas quando você cria uma expressão para uma propriedade de relatório que aceita apenas determinados valores válidos, também conhecidos como tipos enumerados. A tabela a seguir mostra dois exemplos.  
  
|Propriedade|Description|Valores|  
|--------------|-----------------|------------|  
|TextAlign|Valores válidos para alinhamento de texto em uma caixa de texto.|Geral, À Esquerda, Centralizado, À Direita|  
|BorderStyle|Valores válidos para uma linha adicionada a um relatório.|Padrão, Nenhum, Pontilhado, Tracejado, Sólido, Duplo, TraçoPonto, TraçoPontoPonto|  
  
## Constantes do Visual Basic  
 É possível usar constantes definidas na biblioteca de tempo de execução [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] em uma expressão. Por exemplo, você pode usar a constante **DateInterval.Day**. A seguinte expressão para a data de 10 de janeiro de 2008 retorna o número 10:  
  
 `=DatePart("d",Globals!ExecutionTime)`  
  
## Constantes CLR  
 É possível usar constantes definidas nas classes CLR (Common Language Runtime) [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] em uma expressão. A tabela a seguir mostra um exemplo de uma cor definida pelo sistema.  
  
|Constante|Description|  
|--------------|-----------------|  
|MistyRose|Ao criar uma expressão para uma propriedade do relatório baseada na cor do plano de fundo, é possível especificar uma cor pelo nome. Os nomes válidos são listados na caixa de diálogo **Expressão** .|  
  
## Consulte também  
 [Caixa de diálogo Expressão](../Topic/Expression%20Dialog%20Box.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Caixa de diálogo Expressão &#40;Construtor de Relatórios&#41;](../Topic/Expression%20Dialog%20Box%20\(Report%20Builder\).md)  
  
  