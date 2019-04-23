---
title: Usos de expressão em relatórios (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- expressions [Reporting Services], about expressions
ms.assetid: 76b9ed31-5aec-40fc-bb88-a1c1b0ab3fc3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e6f77a2ecf9ed5a985efa4a36f18b9f495c7091f
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59954462"
---
# <a name="expression-uses-in-reports-report-builder-and-ssrs"></a>Uso de expressões em relatórios (Construtor de Relatórios e SSRS)
  As expressões são usadas em toda a definição de relatório para especificar ou calcular valores para parâmetros, consultas, filtros, propriedades de itens de relatório, definições de classificação e grupo, propriedades de caixa de texto, indicadores, mapas do documento, conteúdo de cabeçalho e rodapé de página dinâmica, imagens e definições de fonte de dados dinâmica. Este tópico contém exemplos dos muitos lugares em que você pode usar expressões para variar o conteúdo ou a aparência de um relatório. Esta lista não é completa. Defina uma expressão para qualquer propriedade em uma caixa de diálogo que exibe o botão de expressão (**fx**) ou em uma lista suspensa que exibe **\<Expression...>**.  
  
 As expressões podem ser simples ou complexas. As*expressões simples* contêm uma referência a um único campo de conjunto de dados, parâmetro ou campo interno. As expressões complexas podem conter várias referências internas, operadores e chamadas de função. Por exemplo, uma expressão complexa pode incluir a função Sum aplicada ao campo Sales.  
  
 As expressões são gravadas no [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)]. Uma expressão começa com um sinal de igual (=) seguido por uma combinação de referências a coleções internas, como campos de conjunto de dados e parâmetros, constantes, funções e operadores.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Simple"></a> Usando expressões simples  
 As expressões simples aparecem na superfície de design e em caixas de diálogo entre colchetes. Por exemplo, um campo de conjunto de dados é exibido como `[ProductID]`. As expressões simples são criadas automaticamente quando você arrasta um campo de um conjunto de dados até uma caixa de texto. É criado um espaço reservado, e a expressão define o valor subjacente. Você também pode digitar expressões diretamente em uma célula da região de dados ou em uma caixa de texto, ambas na superfície de design ou em uma caixa de diálogo (por exemplo, `[ProductID]`).  
  
 A tabela a seguir lista exemplos de como usar expressões simples. A tabela descreve a funcionalidade, a propriedade a ser definida, a caixa de diálogo que você costuma usar para defini-la e o valor da propriedade. É possível digitar a expressão simples diretamente na superfície de design, em uma caixa de diálogo ou no painel Propriedades, ou ainda editá-la na caixa de diálogo Expressão, exatamente como você faria com qualquer expressão.  
  
|Funcionalidade|Propriedade, contexto e caixa de diálogo|Valor da propriedade|  
|-------------------|---------------------------------------|--------------------|  
|Especifique um campo de conjunto de dados a ser exibido em uma caixa de texto.|Propriedade Value de um espaço reservado dentro de uma caixa de texto. Use **Caixa de Diálogo de Propriedades de Espaço Reservado, Geral**.|`[Sales]`|  
|Agregue valores de um grupo.|Propriedade Value de um espaço reservado dentro de uma linha associada a um grupo Tablix. Use **Caixa de Diálogo de Propriedades de Caixa de Texto**.|`[Sum(Sales)]`|  
|Inclua um número de página.|Propriedade Value de um espaço reservado dentro de uma caixa de texto que é colocada em um cabeçalho de página. Use **Caixa de Diálogo Propriedades de Caixa de Texto, Geral**.|`[&PageNumber]`|  
|Exiba um valor de parâmetro selecionado.|Propriedade Value de um espaço reservado dentro de uma caixa de texto na superfície de design. Use **Caixa de Diálogo Propriedades de Caixa de Texto, Geral**.|`[@SalesThreshold]`|  
|Especifique uma definição de grupo para uma região de dados.|Expressão de grupo no grupo Tablix. Use **Caixa de Diálogo de Propriedades de Grupo Tablix, Geral**.|`[Category]`|  
|Exclua de uma tabela um valor de campo específico.|Equação de filtro no tablix. Use **Caixa de Diálogo de Propriedades de Grupo Tablix, Filtros**.|Para tipo de dados, selecione **Inteiro**.<br /><br /> `[Quantity]`<br /><br /> `>`<br /><br /> `100`|  
|Inclua somente um valor específico para um filtro de grupo.|Equação de filtro no grupo tablix. Use **Caixa de Diálogo de Propriedades de Grupo Tablix, Filtros**.|`[Category]`<br /><br /> `=`<br /><br /> `Clothing`|  
|Exclua de um conjunto de dados valores específicos de mais de um campo.|Equação de filtro para um grupo em um tablix. Use **Caixa de Diálogo de Propriedades de Grupo Tablix, Filtros**.|`=[Color]`<br /><br /> `<>`<br /><br /> `Red`<br /><br /> `=[Color]`<br /><br /> `<>`<br /><br /> `Blue`|  
|Especifique a ordem de classificação com base em um campo existente em uma tabela.|Expressão de classificação no tablix. Use **Caixa de Diálogo de Propriedades Tablix, Classificação**.|`[SizeSortOrder]`|  
|Vincule um parâmetro de consulta a um parâmetro de relatório.|Coleção de parâmetros no conjunto de dados. Use **Caixa de Diálogo Propriedades de Conjunto de Dados, Parâmetros**.|`[@Category]`<br /><br /> `[@Category]`|  
|Passe um parâmetro de um relatório principal para um sub-relatório.|Coleção de parâmetros no sub-relatório. Use **Caixa de Diálogo Propriedades de Sub-relatório, Parâmetros**.|`[@Category]`<br /><br /> `[@Category]`|  
  
 
  
##  <a name="Complex"></a> Usando expressões complexas  
 As expressões complexas podem conter várias referências internas, operadores e chamadas de função e são exibidas na superfície de design como `<<Expr>>`. Para ver ou alterar o texto da expressão, abra a caixa de diálogo **Expressão** ou digite diretamente no painel Propriedades. A tabela a seguir lista maneiras comuns de usar uma expressão complexa para exibir ou organizar dados ou alterar a aparência de um relatório, inclusive a propriedade a ser definida, a caixa de diálogo que você costuma usar para defini-la e o valor da propriedade. Você pode digitar uma expressão diretamente em uma caixa de diálogo, na superfície de design ou no painel Propriedades.  
  
|Funcionalidade|Propriedade, contexto e caixa de diálogo|Valor da propriedade|  
|-------------------|---------------------------------------|--------------------|  
|Calcule valores de agregação para um conjunto de dados.|Propriedade Value de um espaço reservado dentro de uma caixa de texto. Use **Caixa de Diálogo de Propriedades de Espaço Reservado, Geral**.|`=First(Fields!Sales.Value,"DataSet1")`|  
|Concatene texto e expressões na mesma caixa de texto.|Valor de um espaço reservado dentro de uma caixa de texto que é colocada em um cabeçalho ou rodapé de página. Use **Caixa de Diálogo de Propriedades de Espaço Reservado, Geral**.|`="This report began processing at " & Globals!ExecutionTime`|  
|Calcule um valor de agregação para um conjunto de dados em outro escopo.|Valor de um espaço reservado dentro de uma caixa de texto que é colocada em um grupo tablix. Use **Caixa de Diálogo de Propriedades de Espaço Reservado, Geral**.|`=Max(Fields!Total.Value,"DataSet2)`|  
|Formate os dados de uma caixa de texto de acordo com o valor.|Cor de um espaço reservado dentro de uma caixa de texto na linha de detalhes de um tablix. Use **Caixa de Diálogo Propriedades de Caixa de Texto, Fonte**.|`=IIF(Fields!TotalDue.Value < 10000,"Red","Black")`|  
|Calcule um valor uma única vez para fazer referência a ele em todo o relatório.|Valor de uma variável de relatório. Use **Caixa de Diálogo Propriedades de Relatório, Variáveis**.|`=Variables!MyCalculation.Value`|  
|Inclua valores específicos de mais de um campo de um conjunto de dados.|Equação de filtro para um grupo em um tablix. Use **Caixa de Diálogo de Propriedades de Grupo Tablix, Filtros**.|Para o tipo de dados, selecione **Booliano**.<br /><br /> `=IIF(InStr(Fields!Subcat.Value,"Shorts")=0 AND (Fields!Size.Value="M" OR Fields!Size.Value="S"),TRUE, FALSE)`<br /><br /> `=`<br /><br /> `TRUE`|  
|Oculte uma caixa de texto na superfície de design que pode ser alternada pelo usuário através de um parâmetro booliano denominado *Show*.|Propriedade oculta em uma caixa de texto. Use **Caixa de Diálogo de Propriedades de Caixa de Texto, Visibilidade**.|`=Not Parameters!` *Mostrar \<parâmetro booleano>* `.Value`|  
|Especifique um cabeçalho de página dinâmico ou o conteúdo de um rodapé.|Valor de um espaço reservado dentro de uma caixa de texto que é colocada no cabeçalho ou rodapé de uma página.|`="Page " & Globals!PageNumber & " of "  & Globals!TotalPages`|  
|Especifique uma fonte de dados dinamicamente usando um parâmetro.|Cadeia de conexão na Fonte de dados. Use **Caixa de Diálogo de Propriedades de Fonte de Dados, Geral**.|`="Data Source=" & Parameters!ServerName.Value & ";initial catalog=AdventureWorks2012"`|  
|Identifique todos os valores para um parâmetro multivalor escolhido pelo usuário.|Valor de um espaço reservado dentro de uma caixa de texto. Use **Caixa de Diálogo de Propriedades de Grupo Tablix, Filtros**.|`=Join(Parameters!MyMultivalueParameter.Value,", ")`|  
|Especifique quebras de página para cada 20 linhas em um tablix sem nenhum outro grupo.|Expressão de grupo para um grupo em um tablix. Use **Caixa de Diálogo de Propriedades de Grupo, Quebras de Páginas**. Selecione a opção **Entre cada instância de um grupo**.|`=Ceiling(RowNumber(Nothing)/20)`|  
|Especifique a visibilidade condicional com base em um parâmetro.|Propriedade oculta de um tablix. Use **Caixa de Diálogo de Propriedades Tablix, Visibilidade**.|`=Not Parameters!<` *parâmetro booliano* `>.Value`|  
|Especifique uma data formatada para uma determinada cultura.|Valor de um espaço reservado dentro de uma caixa de texto em uma região de dados. Use **Caixa de Diálogo Propriedades de Caixa de Texto, Geral**.|`=Fields!OrderDate.Value.ToString(System.Globalization.CultureInfo.CreateSpecificCulture("de-DE"))`|  
|Concatene uma cadeia de caracteres e um número formatado como porcentagem com duas casas decimais.|Valor de um espaço reservado dentro de uma caixa de texto em uma região de dados. Use **Caixa de Diálogo Propriedades de Caixa de Texto, Geral**.|`="Growth Percent: " & Format(Fields!Growth.Value,"p2")`|  
  
 
  
## <a name="see-also"></a>Consulte também  
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](expression-examples-report-builder-and-ssrs.md)   
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](report-parameters-report-builder-and-report-designer.md)   
 [Exemplos de equações de filtro &#40;Construtor de Relatórios e SSRS&#41;](filter-equation-examples-report-builder-and-ssrs.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Cabeçalhos e rodapés de página &#40;Construtor de Relatórios e SSRS&#41;](page-headers-and-footers-report-builder-and-ssrs.md)   
 [Formatando texto e espaços reservados &#40;Construtor de Relatórios e SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Ocultar um item &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/hide-an-item-report-builder-and-ssrs.md)  
  
  
