---
title: Referências de coleções de ReportItems (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.component: report-design
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: edc0c75f-0530-4e6d-85aa-3385301bfd00
caps.latest.revision: 8
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 0779913a4334a1142c8a5c8d7561aaa9ecd980cc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33020163"
---
# <a name="built-in-collections---reportitems-collection-references-report-builder"></a>Coleções internas – referências de coleções de ReportItems (Construtor de Relatórios)
  A coleção interna de **ReportItems** é o conjunto de caixas de texto de itens de relatório, como linhas de uma região de dados ou caixas de texto na superfície de design de relatório. A coleção de **ReportItems** inclui caixas de texto que estão no escopo atual de um cabeçalho de página, rodapé de página ou corpo de relatório. Essa coleção é determinada em tempo de execução pelo processador de relatório e pelo renderizador de relatório. O escopo atual é alterado conforme o processador de relatório combina dados de relatório e os elementos de layout do item de relatório sucessivamente conforme o usuário exibe páginas de um relatório. É possível usar a coleção interna de **ReportItems** para produzir cabeçalhos de páginas em estilo de dicionário que mostram o primeiro e o último item em cada página.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="using-the-reportitems-value-property"></a>Usando a propriedade Value de ReportItems  
 Itens dentro da coleção **ReportItems** têm apenas uma propriedade: Value. O valor para um item de **ReportItems** pode ser usado para exibir ou calcular dados de outro campo no relatório. Para acessar o valor da caixa de texto atual, é possível usar o Me.Value ou simplesmente o Value global interno de [!INCLUDE[vbprvb](../../includes/vbprvb-md.md)] . Em funções de relatório, como First e funções de agregação, use a sintaxe totalmente qualificada.  
  
 Por exemplo:  
  
-   Esta expressão, colocada em uma caixa de texto, exibe o valor de uma caixa de texto de um **ReportItem** denominado `Textbox1`:  
  
     `=ReportItems!Textbox1.Value`  
  
-   Essa expressão, colocada em uma propriedade Color da caixa de texto **ReportItem**, exibe o texto em preto quando o valor é > 0. Caso contrário, o valor é exibido em vermelho:  
  
     `=IIF(Me.Value > 0,"Black","Red")`  
  
-   Essa expressão, colocada em uma caixa de texto no cabeçalho ou no rodapé da página, exibe o primeiro valor por página do relatório renderizado, para uma caixa de texto denominada `LastName`:  
  
     `=First(ReportItems("LastName").Value)`  
  
## <a name="dictionary-style-page-header-expressions"></a>Expressões de cabeçalho de página em estilo de dicionário  
 É possível criar um cabeçalho de página para exibir o primeiro e o último cliente na página. Como a caixa de texto no cabeçalho da página pode referir-se apenas à coleção interna **ReportItems** uma vez em uma expressão, é necessário adicionar duas caixas de texto ao cabeçalho da página: uma para o nome do primeiro cliente (`=First(ReportItems!textboxLastName.Value`) e uma para o nome do último cliente (`=Last(ReportItems!textboxLastName.Value`).  
  
 Em uma seção do cabeçalho ou rodapé de página, apenas as caixas de texto na página atual estão disponíveis como um membro da coleção **ReportItems** . Por exemplo, se o `ReportItems!textboxLastName.Value` se referir a uma caixa de texto exibida apenas na primeira página de uma região de dados de várias páginas, você verá um valor para a primeira página, mas todas as outras páginas exibirão o **#Erro** para mostrar que não foi possível avaliar a expressão como foi gravada.  
  
## <a name="scope-for-the-reportitems-collection"></a>Escopo para a coleção ReportItems  
 Conforme o relatório é processado, cada caixa de texto no corpo do relatório ou em uma região de dados é avaliada no contexto de seu conjunto de dados, região de dados e associações de grupos. O escopo para um referência à coleção **ReportItems** é o escopo atual ou qualquer ponto superior ao escopo atual.  
  
 Por exemplo, uma caixa de texto em uma linha que está em um grupo pai não deve conter uma expressão que faça referência ao nome de uma caixa de texto em uma linha do grupo filho. Essa expressão não é resolvida como um valor no relatório porque a caixa de texto da linha filho está fora do escopo. Para obter mais informações, consulte [Referência de funções de agregação &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/report-builder-functions-aggregate-functions-reference.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Coleções internas em expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/built-in-collections-in-expressions-report-builder.md)   
 [Exemplos de expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
