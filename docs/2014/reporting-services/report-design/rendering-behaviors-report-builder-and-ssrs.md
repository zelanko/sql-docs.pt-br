---
title: Comportamentos de renderização (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 8f873ef9-27a3-40e5-b58b-6774f8027a58
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 39fa21f9bb7af15885abdf1d8c78d2651e2fbdab
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079156"
---
# <a name="rendering-behaviors-report-builder--and-ssrs"></a>Comportamentos de renderização (Construtor de Relatórios e SSRS)
  Dependendo do renderizador selecionado, algumas regras são aplicadas ao corpo do relatório e ao seu conteúdo quando um relatório é renderizado. Como os itens de relatório são ajustados juntos em uma página é determinado pela combinação destes fatores:  
  
-   Renderizando regras.  
  
-   A largura e altura dos itens de relatório.  
  
-   O tamanho do corpo do relatório.  
  
-   A largura e altura da página.  
  
-   Suporte específico do renderizador para paginação.  
  
 Este tópico discute a regras gerais aplicadas pelo Reporting Services. Para obter mais informações, consulte [Renderizando itens de relatório &#40;Construtor de Relatórios e SSRS&#41;](rendering-report-items-report-builder-and-ssrs.md), [Renderizando regiões de dados &#40;Construtor de Relatórios e SSRS&#41;](rendering-data-regions-report-builder-and-ssrs.md) e [Renderizando dados &#40;Construtor de Relatórios e SSRS&#41;](rendering-data-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="general-behaviors-for-html-mhtml-word-and-excel-soft-page-break-renderers"></a>Comportamentos Gerais para HTML, MHTML, Word e Excel (Processadores de Quebra de Página Flexível)  
 Os relatórios exportados utilizando os formatos HTML e MHTML são otimizados para uma experiência baseada em telas de computador onde as páginas podem ter vários comprimentos. Quebras de páginas são inseridas verticalmente apenas em locais aproximados dentro do corpo do relatório. Esses locais aproximados são determinados pela configuração da altura interativa no painel Propriedades. Por exemplo, suponhamos que a altura interativa seja definida para 5 polegadas. Quando o relatório é renderizado, a altura da página será de aproximadamente 5 polegadas em comprimento. O Word e o Excel paginam baseado em quebras de páginas lógicas e ignoram a configuração da altura interativa.  
  
> [!NOTE]  
>  Para determinar como um relatório aparecerá em um processador de quebra de página flexível, use a Visualização do Relatório. O relatório aparece do mesmo modo em que estaria em formato HTML, MHTML, Word ou Excel.  
  
 Ao exportar um relatório para HTML, MHTML, Word ou Excel, as regras gerais a seguir deve ser aplicadas:  
  
-   Quebras de página lógicas, as quebras de página que você insere explicitamente, são aplicadas aos itens de relatório. Por exemplo, se você inserir uma quebra de página entre cada grupo, elas serão aplicadas quando o relatório for renderizado.  
  
-   Um layout aproximado que usa a altura de página e o número de horas que o item de relatório aparece é criado. Por exemplo, se uma caixa de texto tiver 0,5 polegadas em altura e se repete cinco vezes no relatório, 2,5 polegadas serão reservadas.  
  
-   Várias quebras de página flexíveis são inseridas com base na configuração da altura interativa. Para eliminar no HTML e os controles do ReportViewer e controlar a paginação apenas com quebras de páginas explícitas, configure o valor **altura interativa** como 0 ou um número muito grande.  
  
    > [!NOTE]  
    >  A configuração da largura interativa não é usada nos processadores de quebras de página flexíveis.  
  
-   As páginas do relatório podem aumentar para acomodar viúvas, órfãos e itens de relatório que precisam ser mantidos unidos. Isto significa que o relatório pode se estender além da largura de tela e pode ser exibido usando as barras deslizantes.  
  
-   A paginação é aplicada aos relatórios apenas verticalmente.  
  
-   Margens de página não são aplicadas.  
  
## <a name="general-behaviors-for-pdf-image-and-print-hard-page-break-renderers"></a>Comportamentos Gerais para PDF, Imagem e Impressão (Processadores de Quebras de Página não Flexíveis)  
 Os relatórios exportados usando o PDF e Imagem são otimizados para uma experiência impressa ou similar a um livro onde as páginas têm um tamanho consistente. As quebras de página são inseridas vertical e horizontalmente em locais específicos dentro do corpo do relatório. Estes locais específicos são determinados pela configuração da largura e altura da página.  
  
> [!NOTE]  
>  Para determinar como um relatório aparecerá em um processador de quebra de página não flexível, use a Visualização da Impressão. O relatório aparecerão como sendo em formato PDF ou Imagem.  
  
-   Páginas são numeradas consecutivamente da esquerda para a direita, em seguida, de cima para baixo.  
  
-   Quebras de página lógicas, as quebras de página que você insere explicitamente, são aplicadas aos itens de relatório. Estas quebras de página podem fazer com que os itens de relatório sejam empurrados para a página seguinte.  
  
-   Se uma quebra de página física ocorrer nos itens de relatório que devem permanecer unidos, esses itens são movidos para a página seguinte.  
  
-   Devido às restrições no tamanho da página, talvez não seja possível manter todos os itens unidos ou repetir os itens. Se isso ocorrer, o processador poderá ignorar algumas regras de repetição com outro item a fim de permitir que o item do relatório se encaixe na página.  
  
-   Se um item não puder ser mantido unido, por exemplo, uma caixa de texto cuja largura aumenta muito para encaixar na área da página utilizada na vertical, então o item será anexado ao limite da página física e continuará na página seguinte.  
  
-   A paginação se aplicada vertical e horizontalmente aos relatórios.  
  
    > [!NOTE]  
    >  A configuração da largura interativa não é usada nos renderizadores de quebra de página impressa.  
  
## <a name="minimum-spacing-between-report-items"></a>Espaçamento mínimo entre itens de relatório  
 Itens de relatório aumentam dentro do corpo do relatório para acomodar o seu conteúdo. Por exemplo, uma região de dados matriz, geralmente se expande na largura e comprimento da página quando o relatório é renderizado, e a altura de uma caixa de texto se ajusta dependendo dos dados retornados da expressão.  
  
 Os processadores mantêm um espaço mínimo entre os itens de relatório que você definir no layout do relatório. Ao colocar um item de relatório adjacente a outro no layout do relatório, a distância entre os itens de relatório torna-se uma distância mínimo que deve ser mantida conforme o relatório é aumentado horizontal e verticalmente. Por exemplo, se acrescentar uma região de dados matriz a um relatório e depois adicionar um retângulo de 0,25 polegadas à direita da matriz, esse espaço será mantidos enquanto a matriz aumenta. Cada item é movido para a direita para manter uma distância mínima dos itens que terminam à sua esquerda.  
  
## <a name="page-headers-and-footers"></a>Cabeçalhos e rodapés de página  
 Os cabeçalhos e rodapés de página aparecem nas partes superior e inferior de cada página renderizada. É possível formatar o cabeçalho e o rodapé da página para incluir uma borda colorida, um estilo de borda e uma largura de borda. Você pode também adicionar uma cor de fundo ou imagem em segundo plano. Essas opções de formatação são todas renderizadas, dependendo do formato escolhido.  
  
 As regras a seguir se aplicam aos cabeçalhos e rodapés das páginas quando renderizados em HTML ou no formato de renderização MHTM:  
  
> [!NOTE]  
>  Para obter informações sobre como o Excel renderiza cabeçalhos e rodapés, consulte [Exportando para o Microsoft Excel &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/exporting-to-microsoft-excel-report-builder-and-ssrs.md). Para obter informações sobre como o Word renderiza cabeçalhos e rodapés, consulte [Exportando para o Microsoft Word &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/exporting-to-microsoft-word-report-builder-and-ssrs.md).  
  
-   Quando presentes o cabeçalho e o rodapés são renderizados nas partes superior e inferior de cada página dentro de uma área utilizável da página.  
  
-   Nas páginas onde o cabeçalho ou o rodapé é oculto, suas alturas continuam reservadas dentro da área utilizável da página, mesmo se o cabeçalho ou o rodapé não estiverem renderizados.  
  
-   Se o conteúdo de um cabeçalho ou rodapé aumentar além dos limites do cabeçalho ou do rodapé, este cabeçalho ou rodapé aumentará para acomodar o conteúdo.  
  
 As regras a seguir se aplicam aos cabeçalhos e rodapés das páginas quando renderizados em PDF ou formato de renderização de Imagem:  
  
-   O cabeçalho ou o rodapé são renderizados nas partes superior e inferior de cada página dentro da área utilizável da página.  
  
-   Nas páginas onde o cabeçalho ou o rodapé é oculto, suas alturas continuam reservadas dentro da área utilizável da página, mesmo se o cabeçalho ou o rodapé não estiverem renderizados.  
  
-   O cabeçalho e o rodapé não aumentam nem encolhem. Eles são renderizados em cada página na altura especificada quando você criou o cabeçalho ou o rodapé.  
  
-   Independentemente o número de colunas dentro do relatório, existem apenas um cabeçalho e um rodapé por página.  
  
-   Se o conteúdo do cabeçalho ou rodapé aumentar além dos limites do cabeçalho ou do rodapé, o conteúdo será anexado.  
  
-   Os cabeçalhos e os rodapés definidos no arquivo RDL original não são renderizados quando o relatório é processado como um sub-relatório.  
  
## <a name="logical-page-breaks"></a>Quebras de página lógicas  
 As quebras de página lógicas são aquelas que você insere antes ou após os itens de relatório ou grupos. As quebras de página ajudam a determinar como o conteúdo é ajustado a uma página de relatório para exibição ideal ao ser renderizado ou exportado para o relatório.  
  
 As regras a seguir se aplicam quando renderizar quebras de página lógicas:  
  
-   As quebras de página lógicas são ignoradas para os itens de relatório que são sempre ocultas e para os itens de relatório onde a visibilidade é controlada pelo clicar de outro item de relatório.  
  
-   As quebras de página lógicas se aplicam condicionalmente a itens visíveis, caso eles estiverem visíveis no momento em que o relatório é renderizado.  
  
-   Um espaço é reservado entre o item de relatório com a quebra de página lógica e seus itens de relatórios de mesmo nível.  
  
-   Quebras de página lógicas que são inseridas antes de um item de relatório empurram o item para a página seguinte. O item de relatório é renderizado na parte superior da página seguinte.  
  
-   As quebras de página lógicas definidas em itens em células de tabela ou matriz não são mantidas. Isso não se aplica a itens em listas.  
  
## <a name="see-also"></a>Consulte também  
 [Funcionalidade interativa para extensões de renderização de relatório diferentes &#40;relatórios e SSRS&#41;](../report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Renderizando para HTML &#40;Construtor de Relatórios e SSRS&#41;](../report-builder/rendering-to-html-report-builder-and-ssrs.md)   
 [Layout de página e renderização &#40;relatórios e SSRS&#41;](page-layout-and-rendering-report-builder-and-ssrs.md)  
  
  
