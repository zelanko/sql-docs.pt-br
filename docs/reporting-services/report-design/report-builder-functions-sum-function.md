---
title: "Função Sum (Construtor de Relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2b45a024-398d-43b8-9948-b8b23fb674c9
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 5f5e5e3b11422c192b2939a1c43a0b4bccb7e549
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="report-builder-functions---sum-function"></a>Funções do Construtor de Relatórios – Função Sum
  Retorna a soma de todos os valores numéricos não nulos especificados pela expressão, avaliados no escopo fornecido.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Sum(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *expressão*  
 (**Integer** ou **Float**) A expressão na qual executar a agregação.  
  
 *escopo*  
 (**String**) Opcional. O nome de um conjunto de dados, um grupo ou uma região de dados que contém os itens de relatório aos quais a função de agregação deve ser aplicada. Se *scope* não estiver especificado, será usado o escopo atual.  
  
 *recursivos*  
 (**Enumerated Type**) Opcional. **Simple** (padrão) ou **RdlRecursive**. Especifica se a agregação deve ser executada recursivamente.  
  
## <a name="return-type"></a>Tipo de retorno  
 Retorna um **Decimal** para expressões decimais e um **Double** para todas as outras expressões.  
  
## <a name="remarks"></a>Remarks  
 O conjunto de dados especificado na expressão deve ter o mesmo tipo de dados. Para converter dados que têm vários tipos de dados numéricos no mesmo tipo de dados, use funções de conversão, como **CInt**, **CDbl** ou **CDec**. Para obter mais informações, consulte [Funções de conversão de tipo](http://go.microsoft.com/fwlink/?LinkId=96142).  
  
 O valor de *scope* deve ser uma constante de cadeia de caracteres e não pode ser uma expressão. Para agregações externas ou que não especificam outras agregações, *scope* deve se referir ao escopo atual ou a um escopo contentor. Para agregações de agregações, as agregações aninhadas podem especificar um escopo filho.  
  
 *Expression* pode conter chamadas para funções de agregação aninhadas com as seguintes exceções e condições:  
  
-   *Scope* para agregações aninhadas deve ser igual ao escopo da agregação externa ou deve estar contido nela. Para todos os escopos distintos na expressão, um escopo deve estar em uma relação filho com todos os outros escopos.  
  
-   *Scope* para agregações aninhadas não pode ser o nome de um conjunto de dados.  
  
-   *Expression* não deve conter a função **First**, **Last**, **Previous**ou **RunningValue** .  
  
-   *Expression* não deve conter agregações aninhadas que especifiquem *recursive*.  
  
 Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para obter mais informações sobre agregações recursivas, consulte [Criando grupos de hierarquias recursivas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Exemplo  
 Os dois exemplos de código a seguir fornecem uma soma dos totais de itens de linhas no grupo `Order` ou na região de dados:  
  
```  
=Sum(Fields!LineTotal.Value, "Order")  
' or   
=Sum(CDbl(Fields!LineTotal.Value), "Order")  
```  
  
## <a name="example"></a>Exemplo  
 Em uma região de dados de matriz com grupos de linhas aninhados Categoria e Subcategoria, e grupos de colunas aninhados Ano e Trimestre, em uma célula que pertence aos grupos de linhas e colunas mais internas, a seguinte expressão é avaliada para o valor máximo de todos os trimestres para todas as subcategorias.  
  
```  
=Max(Sum(Fields!Sales.Value))  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
