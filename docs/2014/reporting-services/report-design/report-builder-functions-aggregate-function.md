---
title: Função de agregação (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 16ce643f-bbb3-40a5-ba78-7aed73156f3e
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 3d05f8d71c3ce12722f139429e48a2a48e8efd8e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115849"
---
# <a name="aggregate-function-report-builder-and-ssrs"></a>Função de agregação (Construtor de Relatórios e SSRS)
  Retorna uma agregação personalizada da expressão especificada, conforme definido pelo provedor de dados.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
Aggregate(expression, scope)  
```  
  
#### <a name="parameters"></a>Parâmetros  
 *Expressão*  
 A expressão na qual executar a agregação. A expressão deve ser uma referência de campo simples.  
  
 *escopo*  
 (`String`) O nome de um conjunto de dados, grupo ou região de dados que contém o relatório itens ao qual aplicar a função de agregação. *Scope* deve ser uma constante de cadeia de caracteres e não pode ser uma expressão. Se *scope* não estiver especificado, será usado o escopo atual.  
  
## <a name="return-type"></a>Tipo de retorno  
 O tipo de retorno é determinado pelo provedor de dados. Retorna `Nothing` se o provedor de dados não oferece suporte a essa função ou dados não estão disponíveis.  
  
## <a name="remarks"></a>Remarks  
 A função `Aggregate` fornece um método para usar agregações que são calculadas na fonte de dados externa. O suporte para esse recurso é determinado pela extensão de dados. Por exemplo, a extensão de processamento de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] recupera conjuntos de linhas simples de uma consulta MDX. Algumas linhas no conjunto de resultados podem conter valores de agregação calculados no servidor de fonte de dados. Eles são conhecidos como *agregações do servidor*. Para exibir as agregações do servidor no designer de consultas gráficas para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], é possível usar o botão **Mostrar Agregação** na barra de ferramentas. Para obter mais informações, consulte [Interface do usuário do Designer de Consultas MDX do Analysis Services &#40;Construtor de Relatórios&#41;](../analysis-services-mdx-query-designer-user-interface-report-builder.md).  
  
 Ao exibir a combinação de valores de agregação e do conjunto de dados de detalhes nas linhas de detalhes de uma região de dados Tablix, normalmente as agregações do servidor não são incluídas porque não são dados de detalhes. No entanto, talvez você queira exibir todos os valores recuperados para o conjunto de dados e personalizar a maneira como os dados de agregação são calculados e exibidos.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] detecta o uso do `Aggregate` função nas expressões no relatório para determinar se deseja exibir as agregações do servidor nas linhas de detalhes. Se você incluir `Aggregate` em uma expressão em uma região de dados, agregações de servidor só podem aparecer no grupo total ou grand total de linhas, não nas linhas de detalhes. Para exibir as agregações do servidor nas linhas de detalhes, não use a função `Aggregate`.  
  
 É possível alterar este comportamento padrão, alterando o valor da opção **Interpretar subtotais como detalhes** na caixa de diálogo **Propriedades do Conjunto de Dados** . Quando esta opção está definida como `True`, todos os dados, incluindo agregações do servidor, são exibidos como dados de detalhes. Quando está definida como `False`, as agregações do servidor são exibidas como totais. A configuração desta propriedade afeta todas as regiões de dados vinculadas a este conjunto de dados.  
  
> [!NOTE]  
>  Todos os grupos contentores do item de relatório que faz referência à `Aggregate` devem ter referências de campos simples para suas expressões de grupos, por exemplo, `[FieldName]`. Não é possível usar `Aggregate` em uma região de dados que usa expressões de grupo complexas. Para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] extensão de processamento de dados, a consulta deve incluir os campos MDX do tipo `LevelProperty` (não `MemberProperty`) para dar suporte a agregação usando a `Aggregate`função.  
  
 *Expression* pode conter chamadas para funções de agregação aninhadas com as seguintes exceções e condições:  
  
-   *Scope* para agregações aninhadas deve ser igual ao escopo da agregação externa ou deve estar contido nela. Para todos os escopos distintos na expressão, um escopo deve estar em uma relação filho com todos os outros escopos.  
  
-   *Scope* para agregações aninhadas não pode ser o nome de um conjunto de dados.  
  
-   *Expressão* não deve conter `First`, `Last`, `Previous`, ou `RunningValue` funções.  
  
-   *Expression* não deve conter agregações aninhadas que especifiquem *recursive*.  
  
 Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md) e [Escopo das expressões para totais, agregações e coleções internas &#40;Construtor de Relatórios e SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md).  
  
 Para obter mais informações sobre agregações recursivas, consulte [Criando grupos de hierarquias recursivas &#40;Construtor de Relatórios e SSRS&#41;](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md).  
  
## <a name="comparing-the-aggregate-and-sum-functions"></a>Comparando as funções Agregação e Soma  
 O `Aggregate` difere das funções de agregação numéricas como `Sum` em que o `Aggregate` função retorna um valor que é calculado com a extensão de processamento de dados ou provedor de dados. Funções de agregação numéricas, como `Sum` retorna um valor calculado pelo processador de relatório em um conjunto de dados do conjunto de dados que é determinado pelo *escopo* parâmetro. Para obter mais informações, consulte as funções de agregação listadas em [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="example"></a>Exemplo  
 O seguinte exemplo de código mostra uma expressão que recupera uma agregação do servidor para o campo `LineTotal`. A expressão é adicionada a uma célula em uma linha que pertence ao grupo `GroupbyOrder`.  
  
```  
=Aggregate(Fields!LineTotal.Value, "GroupbyOrder")  
```  
  
## <a name="see-also"></a>Consulte também  
 [Expressão usa relatórios de &#40;SSRS e construtor de relatórios&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Escopo das expressões para totais, agregações e coleções internas &#40;SSRS e construtor de relatórios&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  