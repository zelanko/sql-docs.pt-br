---
title: Função Count (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 7b50b101-daf8-4fb0-ae04-57384755779f
caps.latest.revision: 7
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 3fc2b74413f2ecb7f0a1f72684494f85ecf82ca9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37152167"
---
# <a name="count-function-report-builder-and-ssrs"></a>função Count (Construtor de Relatórios e SSRS)
  Retorna uma contagem de valores não nulos especificados pela expressão, avaliados no contexto do escopo fornecido.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Count(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Expressão*  
 (`Variant` ou `Binary`) a expressão na qual executar a agregação, por exemplo, `=Fields!FieldName.Value`.  
  
 *escopo*  
 (`String`) O nome de um conjunto de dados, grupo ou região de dados que contém o relatório de itens ao qual deseja aplicar a função de agregação. Se *scope* não estiver especificado, será usado o escopo atual.  
  
 *recursivos*  
 (**Enumerated Type**) Opcional. `Simple` (padrão) ou `RdlRecursive`. Especifica se a agregação deve ser executada recursivamente.  
  
## <a name="return-type"></a>Tipo de retorno  
 Retorna um `Integer`.  
  
## <a name="remarks"></a>Remarks  
 O valor de *scope* deve ser uma constante de cadeia de caracteres e não pode ser uma expressão. Para agregações externas ou que não especificam outras agregações, *scope* deve se referir ao escopo atual ou a um escopo contentor. Para agregações de agregações, as agregações aninhadas podem especificar um escopo filho.  
  
 *Expression* pode conter chamadas para funções de agregação aninhadas com as seguintes exceções e condições:  
  
-   *Scope* para agregações aninhadas deve ser igual ao escopo da agregação externa ou deve estar contido nela. Para todos os escopos distintos na expressão, um escopo deve estar em uma relação filho com todos os outros escopos.  
  
-   *Scope* para agregações aninhadas não pode ser o nome de um conjunto de dados.  
  
-   *Expressão* não deve conter `First`, `Last`, `Previous`, ou `RunningValue` funções.  
  
-   *Expression* não deve conter agregações aninhadas que especifiquem *recursive*.  
  
 Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para obter mais informações sobre agregações recursivas, consulte [Criando grupos de hierarquias recursivas &#40;Construtor de Relatórios e SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
 Exemplo  
  
## <a name="description"></a>Description  
 O seguinte exemplo de código mostra uma expressão que calcula o número de valores não nulos de `Size` para o escopo padrão e para um escopo de grupo pai. A expressão é adicionada a uma célula em uma linha que pertence ao `GroupbySubcategory`do grupo filho. O grupo pai é `GroupbyCategory`. A expressão exibe os resultados de `GroupbySubcategory` (o escopo padrão) e de `GroupbyCategory` (o escopo do grupo pai).  
  
> [!NOTE]  
>  As expressões não devem conter retornos de carro reais e quebras de linha. Eles estão incluídos no exemplo para oferecer suporte a processadores de documentação. Se você copiar o seguinte exemplo, remova os retornos de carro de cada linha.  
  
## <a name="code"></a>Código  
  
```  
="Count (Subcategory): " & Count(Fields!Size.Value) &   
"Count (Category): " & Count(Fields!Size.Value,"GroupbyCategory")  
```  
  
## <a name="see-also"></a>Consulte também  
 [Usos de expressões em relatórios &#40;relatórios e SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  
