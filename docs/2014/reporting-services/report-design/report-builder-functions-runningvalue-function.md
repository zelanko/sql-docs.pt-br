---
title: Função RunningValue (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 6bee2f15-0e69-49c8-9689-b04544063b1d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a72673641fc0f67e22d88d5ea104089b273dedce
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66105157"
---
# <a name="runningvalue-function-report-builder-and-ssrs"></a>Função RunningValue (Construtor de Relatórios e SSRS)
  Retorna uma agregação contínua de todos os valores numéricos não nulos especificados pela expressão, avaliados para o escopo fornecido.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
RunningValue(expression, function, scope)  
```  
  
#### <a name="parameters"></a>parâmetros  
 *expressão*  
 A expressão na qual executar a agregação, por exemplo, `[Quantity]`.  
  
 *função*  
 (`Enum`) O nome da função de agregação a ser aplicado à expressão, por exemplo, `Sum`. Essa função não pode ser `RunningValue`, `RowNumber` ou `Aggregate`.  
  
 *escopo*  
 (`String`) Uma constante de cadeia de caracteres que é o nome de um conjunto de dados, região de dados ou grupo ou nulo (`Nothing` no [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]), que especifica o contexto no qual avaliar a agregação. `Nothing` especifica o contexto mais externo, geralmente o conjunto de dados do relatório.  
  
## <a name="return-type"></a>Tipo de retorno  
 Determinado pela função de agregação especificada no parâmetro *function* .  
  
## <a name="remarks"></a>Comentários  
 O valor de `RunningValue` é redefinido como 0 para cada nova instância do escopo. Se um grupo for especificado, o valor em uso será redefinido quando a expressão de grupo for alterada. Se uma região de dados for especificada, o valor em uso será redefinido para cada nova instância da região de dados. Se um conjunto de dados for especificado, o valor em uso não será redefinido em todo o conjunto de dados.  
  
 `RunningValue` não pode ser usado em um filtro ou expressão de classificação.  
  
 O conjunto de dados para o qual o valor em execução é calculado deve ter o mesmo tipo de dados. Para converter dados que têm vários tipos de dados numéricos no mesmo tipo de dados, use funções de conversão, como `CInt`, `CDbl` ou `CDec`. Para obter mais informações, consulte [Funções de conversão de tipo](https://go.microsoft.com/fwlink/?LinkId=96142).  
  
 O*Scope* não pode ser uma expressão.  
  
 *Expression* pode conter chamadas para funções de agregação aninhadas com as seguintes exceções e condições:  
  
-   O escopo para agregações aninhadas deve ser igual ao escopo da agregação externa ou deve estar contido nela. Para todos os escopos distintos na expressão, um escopo deve estar em uma relação filho com todos os outros escopos.  
  
-   O escopo para agregações aninhadas não pode ser o nome de um conjunto de dados.  
  
-   A *expressão* não deve `First`conter `Last`funções `Previous`,, `RunningValue` ou.  
  
-   *Expression* não deve conter agregações aninhadas que especifiquem *recursive*.  
  
 Para calcular o valor em uso do número de linhas, use `RowNumber`. Para obter mais informações, consulte [Função RowNumber &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-rownumber-function.md).  
  
 Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para obter mais informações sobre agregações recursivas, consulte [Criando grupos de hierarquias recursivas &#40;Construtor de Relatórios e SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="examples"></a>Exemplos  
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
  
## <a name="see-also"></a>Consulte Também  
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
