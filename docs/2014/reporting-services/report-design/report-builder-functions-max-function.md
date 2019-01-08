---
title: Função Max (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 61c4d6ff-6435-456a-9cbd-5113d2113e8a
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 6ded4f239d7694c4b76829f9a5cc8b3beffb6578
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53365958"
---
# <a name="max-function-report-builder-and-ssrs"></a>Função Max (Construtor de Relatórios e SSRS)
  Retorna o valor máximo de todos os valores numéricos não nulos especificados pela expressão, no contexto do escopo fornecido.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Max(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Expressão*  
 (`Variant`) A expressão na qual a agregação será executada.  
  
 *escopo*  
 (`String`) Opcional. O nome de um conjunto de dados, um grupo ou uma região de dados que contém os itens de relatório aos quais a função de agregação deve ser aplicada. Se *scope* não estiver especificado, será usado o escopo atual.  
  
 *recursivos*  
 (**Enumerated Type**) Opcional. `Simple` (padrão) ou `RdlRecursive`. Especifica se a agregação deve ser executada recursivamente.  
  
## <a name="return-type"></a>Tipo de retorno  
 Determinado pelo tipo da expressão.  
  
## <a name="remarks"></a>Comentários  
 O conjunto de dados especificado na expressão deve ter o mesmo tipo de dados. Para converter dados que têm vários tipos de dados numéricos no mesmo tipo de dados, use funções de conversão, como `CInt`, `CDbl` ou `CDec`. Para obter mais informações, consulte [Funções de conversão de tipo](https://go.microsoft.com/fwlink/?LinkId=96142).  
  
 O valor de *scope* deve ser uma constante de cadeia de caracteres e não pode ser uma expressão. Para agregações externas ou que não especificam outras agregações, *scope* deve se referir ao escopo atual ou a um escopo contentor. Para agregações de agregações, as agregações aninhadas podem especificar um escopo filho.  
  
 *Expression* pode conter chamadas para funções de agregação aninhadas com as seguintes exceções e condições:  
  
-   *Scope* para agregações aninhadas deve ser igual ao escopo da agregação externa ou deve estar contido nela. Para todos os escopos distintos na expressão, um escopo deve estar em uma relação filho com todos os outros escopos.  
  
-   *Scope* para agregações aninhadas não pode ser o nome de um conjunto de dados.  
  
-   *Expressão* não deve conter `First`, `Last`, `Previous`, ou `RunningValue` funções.  
  
-   *Expression* não deve conter agregações aninhadas que especifiquem *recursive*.  
  
 Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para obter mais informações sobre agregações recursivas, consulte [Criando grupos de hierarquias recursivas &#40;Construtor de Relatórios e SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="example"></a>Exemplo  
 O exemplo de código a seguir fornece o total mais alto no grupo `Year` ou na região de dados.  
  
```  
=Max(Fields!OrderTotal.Value, "Year")  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usos de expressões em relatórios &#40;Construtor de Relatórios e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
