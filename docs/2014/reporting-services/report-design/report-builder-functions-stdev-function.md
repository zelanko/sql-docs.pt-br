---
title: Função StDev (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: cb51e96e-a828-42f0-b67c-cee3f4d221e7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 1763b417f381293eb9f9535cc5ef317cff268588
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66105151"
---
# <a name="stdev-function-report-builder-and-ssrs"></a>Função StDev (Construtor de Relatórios e SSRS)
  Retorna o desvio padrão de todos os valores numéricos não nulos especificados pela expressão, avaliados no escopo fornecido.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
StDev(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *expressão*  
 (`Integer` ou `Float`) A expressão na qual executar a agregação.  
  
 *escopo*  
 (`String`) Opcional. O nome de um conjunto de dados, um grupo ou uma região de dados que contém os itens de relatório aos quais a função de agregação deve ser aplicada. Se *scope* não estiver especificado, será usado o escopo atual.  
  
 *recursivos*  
 (**Enumerated Type**) Opcional. 
  `Simple` (padrão) ou `RdlRecursive`. Especifica se a agregação deve ser executada recursivamente.  
  
## <a name="return-type"></a>Tipo de retorno  
 Retorna um `Decimal` para expressões decimais e um `Double` para todas as outras expressões.  
  
## <a name="remarks"></a>Comentários  
 O conjunto de dados especificado na expressão deve ter o mesmo tipo de dados. Para converter dados que têm vários tipos de dados numéricos no mesmo tipo de dados, use funções de conversão, como `CInt`, `CDbl` ou `CDec`. Para obter mais informações, consulte [Funções de conversão de tipo](https://go.microsoft.com/fwlink/?LinkId=96142).  
  
 O valor de *scope* deve ser uma constante de cadeia de caracteres e não pode ser uma expressão. Para agregações externas ou que não especificam outras agregações, *scope* deve se referir ao escopo atual ou a um escopo contentor. Para agregações de agregações, as agregações aninhadas podem especificar um escopo filho.  
  
 *Expression* pode conter chamadas para funções de agregação aninhadas com as seguintes exceções e condições:  
  
-   *Scope* para agregações aninhadas deve ser igual ao escopo da agregação externa ou deve estar contido nela. Para todos os escopos distintos na expressão, um escopo deve estar em uma relação filho com todos os outros escopos.  
  
-   *Scope* para agregações aninhadas não pode ser o nome de um conjunto de dados.  
  
-   A *expressão* não deve `First`conter `Last`funções `Previous`,, `RunningValue` ou.  
  
-   *Expression* não deve conter agregações aninhadas que especifiquem *recursive*.  
  
 Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para obter mais informações sobre agregações recursivas, consulte [Criando grupos de hierarquias recursivas &#40;Construtor de Relatórios e SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir fornece o desvio padrão de totais de itens de linhas no grupo de `Order` ou na região de dados.  
  
```  
=StDev(Fields!LineTotal.Value, "Order")  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
