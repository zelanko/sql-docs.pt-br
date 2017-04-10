---
title: "Fun&#231;&#227;o RunningValue (Construtor de Relat&#243;rios e SSRS) | Microsoft Docs"
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
ms.assetid: 6bee2f15-0e69-49c8-9689-b04544063b1d
caps.latest.revision: 8
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# Fun&#231;&#227;o RunningValue (Construtor de Relat&#243;rios e SSRS)
  Retorna uma agregação contínua de todos os valores numéricos não nulos especificados pela expressão, avaliados para o escopo fornecido.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## Sintaxe  
  
```  
  
RunningValue(expression, function, scope)  
```  
  
#### Parâmetros  
 *expressão*  
 A expressão na qual executar a agregação, por exemplo, `[Quantity]`.  
  
 *função*  
 (**Enum**) O nome da função de agregação a ser aplicado à expressão, por exemplo, **Sum**. Essa função não pode ser **RunningValue**, **RowNumber**ou **Aggregate**.  
  
 *escopo*  
 (**String**) Uma constante de cadeia de caracteres que é o nome de um conjunto de dados, região de dados, grupo ou nulo (**Nothing** no [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]), que especifica o contexto no qual avaliar a agregação. **Nothing** especifica o contexto mais externo, geralmente o conjunto de dados do relatório.  
  
## Tipo de retorno  
 Determinado pela função de agregação especificada no parâmetro *function* .  
  
## Comentários  
 O valor de **RunningValue** é redefinido como 0 para cada nova instância do escopo. Se um grupo for especificado, o valor em uso será redefinido quando a expressão de grupo for alterada. Se uma região de dados for especificada, o valor em uso será redefinido para cada nova instância da região de dados. Se um conjunto de dados for especificado, o valor em uso não será redefinido em todo o conjunto de dados.  
  
 **RunningValue** não pode ser usado em um filtro ou expressão de classificação.  
  
 O conjunto de dados para o qual o valor em execução é calculado deve ter o mesmo tipo de dados. Para converter dados que têm vários tipos de dados numéricos no mesmo tipo de dados, use funções de conversão, como **CInt**, **CDbl** ou **CDec**. Para obter mais informações, consulte [Funções de conversão de tipo](http://go.microsoft.com/fwlink/?LinkId=96142).  
  
 O*Scope* não pode ser uma expressão.  
  
 *Expression* pode conter chamadas para funções de agregação aninhadas com as seguintes exceções e condições:  
  
-   O escopo para agregações aninhadas deve ser igual ao escopo da agregação externa ou deve estar contido nela. Para todos os escopos distintos na expressão, um escopo deve estar em uma relação filho com todos os outros escopos.  
  
-   O escopo para agregações aninhadas não pode ser o nome de um conjunto de dados.  
  
-   *Expression* não deve conter a função **First**, **Last**, **Previous**ou **RunningValue** .  
  
-   *Expression* não deve conter agregações aninhadas que especifiquem *recursive*.  
  
 Para calcular o valor em uso do número de linhas, use **RowNumber**. Para obter mais informações, consulte [Função RowNumber &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rownumber-function-report-builder-and-ssrs.md).  
  
 Para obter mais informações, consulte [Referência de funções agregadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/aggregate-functions-reference-report-builder-and-ssrs.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md).  
  
 Para obter mais informações sobre agregações recursivas, consulte [Criando grupos de hierarquias recursivas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## Exemplos  
 O exemplo de código a seguir fornece uma soma parcial do campo denominado `Cost` no escopo mais externo que é o conjunto de dados.  
  
```  
=RunningValue(Fields!Cost.Value, Sum, Nothing)  
```  
  
 O exemplo de código a seguir fornece uma soma parcial do campo denominado `Score` no conjunto de dados denominado `DataSet1`.  
  
```  
=RunningValue(Fields!Score.Value,sum,"DataSet1")  
```  
  
 O exemplo de código a seguir fornece uma soma parcial do campo denominado `Traffic Charges` no escopo mais externo.  
  
```  
=RunningValue(Fields!Traffic Charges.Value, Sum, Nothing)  
```  
  
## Consulte também  
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md)  
  
  