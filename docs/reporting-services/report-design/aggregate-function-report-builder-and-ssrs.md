---
title: "Fun&#231;&#227;o de agrega&#231;&#227;o (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 16ce643f-bbb3-40a5-ba78-7aed73156f3e
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# Fun&#231;&#227;o de agrega&#231;&#227;o (Construtor de Relat&#243;rios e SSRS)
  Retorna uma agregação personalizada da expressão especificada, conforme definido pelo provedor de dados.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Sintaxe  
  
```  
  
Aggregate(expression, scope)  
```  
  
#### Parâmetros  
 *expressão*  
 A expressão na qual executar a agregação. A expressão deve ser uma referência de campo simples.  
  
 *escopo*  
 (**String**) O nome de um conjunto de dados, um grupo ou uma região de dados que contém os itens de relatório aos quais a função de agregação deve ser aplicada. *Scope* deve ser uma constante de cadeia de caracteres e não pode ser uma expressão. Se *scope* não estiver especificado, será usado o escopo atual.  
  
## Tipo de retorno  
 O tipo de retorno é determinado pelo provedor de dados. Retornará **Nothing** se o provedor de dados não oferecer suporte a esta função ou se os dados não estiverem disponíveis.  
  
## Comentários  
 A função **Aggregate** fornece um método para usar agregações que são calculadas na fonte de dados externa. O suporte para esse recurso é determinado pela extensão de dados. Por exemplo, a extensão de processamento de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] recupera conjuntos de linhas simples de uma consulta MDX. Algumas linhas no conjunto de resultados podem conter valores de agregação calculados no servidor de fonte de dados. Eles são conhecidos como *agregações do servidor*. Para exibir as agregações do servidor no designer de consultas gráficas para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], é possível usar o botão **Mostrar Agregação** na barra de ferramentas. Para obter mais informações, consulte [Interface do usuário do Designer de Consultas MDX do Analysis Services &#40;Construtor de Relatórios&#41;](../Topic/Analysis%20Services%20MDX%20Query%20Designer%20User%20Interface%20\(Report%20Builder\).md).  
  
 Ao exibir a combinação de valores de agregação e do conjunto de dados de detalhes nas linhas de detalhes de uma região de dados Tablix, normalmente as agregações do servidor não são incluídas porque não são dados de detalhes. No entanto, talvez você queira exibir todos os valores recuperados para o conjunto de dados e personalizar a maneira como os dados de agregação são calculados e exibidos.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] detecta o uso da função **Aggregate** em expressões no relatório para determinar se as agregações do servidor devem ser exibidas nas linhas de detalhes. Se a **Aggregate** for incluída em uma expressão em uma região de dados, as agregações do servidor poderão ser exibidas apenas nas linhas do grupo total ou do total geral, não nas linhas de detalhes. Para exibir as agregações do servidor nas linhas de detalhes, não use a função **Aggregate** .  
  
 É possível alterar este comportamento padrão, alterando o valor da opção **Interpretar subtotais como detalhes** na caixa de diálogo **Propriedades do Conjunto de Dados** . Quando esta opção está definida como **True**, todos os dados, incluindo agregações do servidor, são exibidos como dados de detalhes. Quando está definida como **False**, as agregações do servidor são exibidas como totais. A configuração desta propriedade afeta todas as regiões de dados vinculadas a este conjunto de dados.  
  
> [!NOTE]  
>  Todos os grupos contentores do item de relatório que faz referência a **Aggregate** devem ter referências de campos simples para suas expressões de grupos, por exemplo, `[FieldName]`. Não é possível usar a **Aggregate** em uma região de dados que usa expressões de grupos complexas. Para a extensão de processamento de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], a consulta deve incluir campos MDX do tipo **LevelProperty** (não **MemberProperty**) para dar suporte à agregação com a função **Aggregate**.  
  
 *Expression* pode conter chamadas para funções de agregação aninhadas com as seguintes exceções e condições:  
  
-   *Scope* para agregações aninhadas deve ser igual ao escopo da agregação externa ou deve estar contido nela. Para todos os escopos distintos na expressão, um escopo deve estar em uma relação filho com todos os outros escopos.  
  
-   *Scope* para agregações aninhadas não pode ser o nome de um conjunto de dados.  
  
-   *Expression* não deve conter a função **First**, **Last**, **Previous**ou **RunningValue** .  
  
-   *Expression* não deve conter agregações aninhadas que especifiquem *recursive*.  
  
 Para obter mais informações, consulte [Referência de funções agregadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/aggregate-functions-reference-report-builder-and-ssrs.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md).  
  
 Para obter mais informações sobre agregações recursivas, consulte [Criando grupos de hierarquias recursivas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## Comparando as funções Agregação e Soma  
 A função de **Aggregate** difere das funções de agregação numéricas, como **Sum** , pelo fato de que a função de **Aggregate** retorna um valor calculado pelo provedor de dados ou pela extensão de processamento de dados. As funções de agregação numéricas, como **Sum** , retornam um valor calculado pelo processador de relatório em um conjunto de dados determinado pelo parâmetro *scope* . Para obter mais informações, consulte as funções de agregação listadas na [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/aggregate-functions-reference-report-builder-and-ssrs.md).  
  
## Exemplo  
 O seguinte exemplo de código mostra uma expressão que recupera uma agregação do servidor para o campo `LineTotal`. A expressão é adicionada a uma célula em uma linha que pertence ao grupo `GroupbyOrder`.  
  
```  
=Aggregate(Fields!LineTotal.Value, "GroupbyOrder")  
```  
  
## Consulte também  
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md)  
  
  