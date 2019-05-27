---
title: Caixa de diálogo expressão (construtor de relatórios) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10040"
helpviewer_keywords:
- expressions
ms.assetid: e89c4d97-5d41-4b55-8695-79329edac15d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c6f12a39c1456c179187654445947de9ee7d87a9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66109151"
---
# <a name="expression-dialog-box-report-builder"></a>Caixa de diálogo Expressão (Construtor de Relatórios)
  Use a caixa de diálogo **Expressão** para escrever expressões do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] para propriedades de itens de relatório. É possível usar expressões para definir muitas propriedades, incluindo cor, fonte e bordas. Em tempo de execução, o processador de relatório avalia as expressões e substitui o resultado do valor da propriedade.  
  
 A caixa de diálogo **Expressão** inclui uma janela de código, uma árvore de categoria, itens de categoria, um painel de descrição e um painel de exemplo. A caixa de diálogo **Expressão** é sensível ao contexto. Os itens e descrições de categoria são alterados em resposta à categoria da expressão com a qual você está trabalhando. Para obter mais informações, consulte [exemplos de expressões &#40;construtor de relatórios e SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md), [expressões &#40;construtor de relatórios e SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)  
  
## <a name="expression-constructs"></a>Construções de expressões  
 As expressões começam com um sinal de igual (=) e podem incluir constantes, literais, operadores e referências a campos internos, coleções internas, funções internas, funções da biblioteca em tempo de execução do [!INCLUDE[vbprvb](../includes/vbprvb-md.md)], classes do common language runtime do [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] e funções personalizadas. A lista a seguir descreve as categorias e os valores que podem ser adicionados a uma expressão.  
  
 **Definir expressão para:**  _\<PropertyName>_  
 O nome da propriedade para a qual você está definindo uma expressão. Também é possível definir essa propriedade por nome, no painel Propriedades.  
  
 **Constantes**  
 Fornece uma lista de valores predefinidos válidos para essa propriedade para propriedades baseadas em constantes. Por exemplo, uma propriedade baseada em cor mostra nomes de cores válidos. Para uma propriedade do tipo de dados booliano, os valores são `True` e `False`.  
  
 Nem todos os itens que oferecem suporte às expressões podem ser definidos como uma constante. Se uma propriedade não puder ser definida como valor de constante, o painel de descrição fornecerá essas informações.  
  
 **Campos internos**  
 Fornece uma lista de itens na coleção global que podem ser usados em uma expressão. Algumas coleções recebem suporte somente após a publicação do relatório no servidor. Para obter mais informações, consulte [Coleções internas em expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/built-in-collections-in-expressions-report-builder.md).  
  
 **Parâmetros**  
 Fornece uma lista de parâmetros de relatório.  
  
 **Campos (**  _\<conjunto de dados selecionado >_ **)**  
 Exibe a lista de campos para o conjunto de dados selecionado na categoria Conjuntos de dados. Clique duas vezes em um campo para copiá-lo na caixa **Expressão** .  
  
 **Conjuntos de dados**  
 Fornece uma lista de conjuntos de dados disponíveis e mostra os campos que são membros do conjunto de dados.  
  
 **Variáveis**  
 Exibe uma lista de variáveis de relatório. Para obter mais informações, consulte [Referências de coleções de variáveis de grupo e de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-design/built-in-collections-report-and-group-variables-references-report-builder.md).  
  
 **Operadores**  
 Exibe os operadores que podem ser incluídos em uma manipulação de cálculo ou de cadeia de caracteres. Para obter mais informações, consulte [Operadores em Expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/operators-in-expressions-report-builder-and-ssrs.md).  
  
 **Funções comuns**  
 Exibe funções comuns, agrupadas por tipo. Ao selecionar uma função no painel Item, uma descrição e exemplo são exibidos.  
  
 Funções comuns incluem relatório interno e funções de agregação [!INCLUDE[vbprvb](../includes/vbprvb-md.md)] funções de biblioteca de tempo de execução, e [!INCLUDE[dnprdnshort](../includes/dnprdnshort-md.md)] classes common language runtime (CLR) na <xref:System.Math> e <xref:System.Convert> namespace. Também é possível adicionar referências às classes CLR e aos assemblies externos que não são exibidos na lista de categorias. Para obter mais informações, consulte [Referências a código personalizado e assemblies em expressões no Designer de Relatórios &#40;SSRS&#41;](report-design/custom-code-and-assembly-references-in-expressions-in-report-designer-ssrs.md).  
  
## <a name="options"></a>Opções  
 Janela de código  
 Use a janela de código no painel superior para digitar uma expressão. Ao abrir a caixa de diálogo **Expressão** , a janela de código contém a expressão. É possível substituir ou revisar a expressão. É possível adicionar chamadas de função, operadores, constantes, campos, parâmetros, itens das coleções globais e referências ao código personalizado. A janela de código exibe as alterações conforme elas são feitas.  
  
 Um sublinhado vermelho ondulado indica um erro de sintaxe. Focalize o texto sublinhado para ver a mensagem de erro.  
  
 Ao digitar os termos da coleção global seguidos por um separador de pontuação, você vê uma lista suspensa de membros ou propriedades disponíveis. Na lista suspensa, digite os primeiros caracteres seguidos por um caractere de tabulação para preencher automaticamente a seleção.  
  
 Ao digitar o nome de uma função seguido por um parênteses à esquerda, você vê uma dica de ferramenta que fornece informações sobre os parâmetros e os valores de retorno da função.  
  
 **Categoria**  
 Exibe categorias de expressões. A escolha de uma categoria estabelece um contexto para a criação de uma expressão e altera a lista de valores válidos no painel Item. Por exemplo, para uma expressão de valor de uma caixa de texto, expanda as funções comuns e selecione as funções de agregação para exibir `Avg`, `Count`e outras funções na **Item** painel.  
  
 **Item**  
 Exibe a lista de valores válidos para a categoria selecionada. Clique duas vezes em um item para adicionar o texto da expressão a esse item no ponto de inserção da janela de código.  
  
 **Valores**  
 Dependendo da categoria e do item selecionados, o terceiro painel conterá uma descrição, uma expressão de exemplo ou uma lista de valores válidos. Arraste a borda da caixa de diálogo para alargar a área de exemplo.  
  
## <a name="see-also"></a>Consulte também  
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/expressions-report-builder-and-ssrs.md)   
 [Formatando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-report-items-report-builder-and-ssrs.md)   
 [Formatando números e datas &#40;Construtor de Relatórios e SSRS&#41;](report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Referências de coleção de parâmetros &#40;Construtor de Relatórios e SSRS&#41;](report-design/built-in-collections-parameters-collection-references-report-builder.md)   
 [Exemplos de expressões de grupo &#40;Construtor de Relatórios e SSRS&#41;](report-design/group-expression-examples-report-builder-and-ssrs.md)   
 [Exemplos de equações de filtro &#40;Construtor de Relatórios e SSRS&#41;](report-design/filter-equation-examples-report-builder-and-ssrs.md)   
 [Referências de coleção de campos do conjunto de dados &#40;relatórios e SSRS&#41;](report-design/built-in-collections-dataset-fields-collection-references-report-builder.md)   
 [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](report-design/report-builder-functions-aggregate-functions-reference.md)   
 [Tipos de dados em expressões &#40;Construtor de Relatórios e SSRS&#41;](report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [Selecione a caixa de diálogo de cor &#40;relatórios e SSRS&#41;](../../2014/reporting-services/select-color-dialog-box-report-builder-and-ssrs.md)  
  
  
