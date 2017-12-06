---
title: "Renderizando itens de relatório (Construtor de Relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 99ebb4dc-41cc-42ac-82dd-a2b0e31155a0
caps.latest.revision: "7"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 2a54547fe33ecf99952ab4ee9f3d25cbcdb091f3
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="rendering-report-items-report-builder-and-ssrs"></a>Renderizando itens de relatório (Construtor de Relatórios e SSRS)
  O número, o tamanho e o local de itens de relatório afetam a maneira como os renderizadores paginam o corpo de relatório. A seguir uma descrição de como vários itens de relatório são renderizados.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="overlapping-report-items"></a>Sobrepondo itens de relatório  
 Os itens de relatório sobrepostos não têm suporte no HTML, MHTML, Word, Excel, na Visualização, nem no Visualizador de Relatórios. Se itens sobrepostos existirem, eles são removidos. As regras a seguir se aplicam aos itens de relatório sobrepostos:  
  
-   Se a sobreposição vertical de itens de relatório for maior, um dos itens de sobreposição é removido para a direita. O item mais a esquerda permanece onde é posicionado.  
  
-   Se a sobreposição horizontal de itens de relatório for maior, um dos itens de sobreposição é removido para baixo. O item mais no topo permanece onde é posicionado.  
  
-   Se as sobreposições vertical e horizontal forem iguais, um dos itens sobreposto é removido para a direita. O item mais a esquerda permanece onde é posicionado.  
  
-   Se um item deve ser movido para corrigir a sobreposição, os itens de relatório adjacentes são removidos para baixo e/ou para a direita para manter um espaço mínimo entre o item e os itens de relatório que terminam acima e/ou à sua esquerda. Por exemplo, suponha que dois itens de relatório se sobreponham verticalmente e um terceiro item de relatório esteja 2 polegadas à direita deles. Quando o item de relatório sobreposto for movido para a direita, o terceiro item de relatório também será movido para a direita a fim de manter as 2 polegadas entre ele mesmo e o item de relatório à sua esquerda.  
  
 Os itens de relatórios sobrepostos têm suporte nos formatos de quebra de página não flexíveis, inclusive na impressão.  
  
## <a name="visibility-and-report-items"></a>Visibilidade e itens de relatório  
 Itens de relatório podem ser ocultados ou exibidos por padrão ou ocultados e exibidos condicionalmente usando expressões. Opcionalmente, a visibilidade pode ser trocada clicando em outro item de relatório.  
  
 As regras de visibilidade a seguir se aplicam quando à renderização de itens de relatórios:  
  
-   Se um item de relatório e seu conteúdo estiverem sempre ocultos (não é oculto com base em uma expressão ou sua visibilidade não pode ser alternada clicando em outro item de relatório) então outros itens de relatório à direita ou abaixo do mesmo não se movem para preencher o espaço vazio. Por exemplo, se um retângulo e a imagem incluída no mesmo estão ocultos, o item de relatório que se inicia à direita do retângulo não será removido para a esquerda para preencher o que aparece ser um espaço vazio. O espaço ocupado pelo retângulo é preservado.  
  
-   Se um item de relatório e seu conteúdo estiverem condicionalmente ocultos (é oculto com base em uma expressão ou sua visibilidade não pode ser alternada clicando em outro item de relatório) então outros itens de relatório à direita ou abaixo do mesmo se movam para a esquerda para preencher o espaço vazio quando o item é oculto.  
  
-   Se a visibilidade de um item de relatório e seu conteúdo puder ser alternada clicando em outro item de relatório, então a paginação muda para acomodar o item de relatório e seu conteúdo somente quando ele é inicialmente exibido.  
  
## <a name="keeping-report-items-together-on-a-single-page"></a>Mantendo unidos itens de relatório em uma única página  
 Vários itens de relatório dentro de um relatório podem ser mantidos unidos em uma única página, implicitamente ou explicitamente configurando as propriedades de manutenção com o grupo ou manutenção de união. Os itens de relatório são sempre renderizados na mesma página se o item de relatório não tiver qualquer quebra de página lógica e for menor em tamanho de que a área utilizável da página. Se um item de relatório não couber totalmente na página na qual ele deveria iniciar normalmente, uma quebra de página não flexível é inserida antes do item de relatório, forçando-o para a página seguinte. Para os processadores de quebra de página flexível, esta página é estendida para acomodar o item de relatório.  
  
 Quando o item de relatório for sempre oculto, as regras para manter os itens unidos são ignoradas.  
  
 Os itens a seguir estão sempre mantidos unidos:  
  
-   Imagens.  
  
-   Linhas.  
  
-   Gráficos, medidores e mapas.  
  
-   Uma única linha em uma região de dados que aparece separadamente em outra página, selecionando a manutenção com a opção de grupo. Isto irá manter implicitamente unida à única linha com no mínimo uma instância do grupo para que a linha não fique órfã. Você pode definir esta opção em uma região de dados ou grupo.  
  
-   Área de cabeçalho de uma região de dados.  
  
-   Área de cabeçalho de uma região de dados e a primeira linha de dados.  
  
-   Itens de relatórios podem ser alternados em uma região de dados tablix.  
  
### <a name="priority-order"></a>Ordem de prioridade  
 Devido às limitações no tamanho de página, conflitos podem surgir entre as regras para manter unidos itens de relatório. Quando conflitos ocorrerem, a ordem de prioridade a seguir é usada para manter os itens unidos durante a renderização:  
  
-   Linhas, gráficos e imagens.  
  
-   Controle de viúva e órfão.  
  
-   Cabeçalhos de coluna e cabeçalhos de linha repetidos.  
  
     Os cabeçalhos têm prioridade sobre os rodapés. Grupos repetidos internos têm prioridade sobre os grupos externos. Itens onde a propriedade **RepeatWith** é definida que estejam mais perto da região de dados de destino têm prioridade sobre os itens que estão mais longe da região de dados.  
  
-   Itens pequenos de relatório, como caixas de texto ou retângulos, com uma propriedade KeepTogether explícita definida como **true**.  
  
-   Itens grandes de relatório, como sub-relatórios ou um membro Tablix não interno, com uma propriedade KeepTogether explícita definida como **true**.  
  
-   Regiões de dados Tablix com uma propriedade KeepTogether explícita definida como **true**.  
  
### <a name="subreports"></a>Sub-relatórios  
 Um sub-relatório renderiza como um retângulo que contém outro relatório definido em um arquivo .rdl de relatório separado. O arquivo de sub-relatório deve ser publicado a um servidor de relatório antes de poder ser acessado pelo relatório pai.  
  
 As regras a seguir se aplicam quando renderizar sub-relatórios:  
  
-   Sub-relatórios podem aumentar até o tamanho do corpo definido no arquivo .rdl que define o sub-relatório. Por exemplo, se o RDL para o sub-relatório indicar que o corpo do sub-relatório tem uma largura de 5 polegadas, então o sub-relatório terá uma largura de 5 polegadas dentro do relatório pai.  
  
-   Sub-relatórios herdam as configurações de coluna do relatório pai. As configurações de colunas definidas no RDL original são sempre ignoradas.  
  
-   Apenas o corpo do sub-relatório é renderizado. As seções de cabeçalho e rodapé definidos no arquivo .rdl do sub-relatório não são renderizadas quando o sub-relatório é renderizado no relatório pai.  
  
-   Os sub-relatórios têm uma propriedade KeepTogether explícita. Quando definida para **true**, todos os itens no sub-relatório serão mantidos unidos em uma página quando possível.  
  
-   Se um sub-relatório não puder executar, ele será exibido no relatório como uma caixa de texto com uma mensagem de erro. As propriedades de estilo aplicadas ao sub-relatório são aplicadas no lugar na caixa de texto.  
  
-   Se o sub-relatório estiver dividido por quebra de página, a definição **Omitir borda na quebra de página** controlará se as bordas no sub-relatórios estão ou não fechadas ou abertas.  
  
 Para obter mais informações sobre sub-relatórios, consulte [Sub-relatórios &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/subreports-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Paginação no Reporting Services &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Comportamentos de renderização &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/rendering-behaviors-report-builder-and-ssrs.md)   
 [Funcionalidade interativa para extensões de renderização de relatório diferentes &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-builder/interactive-functionality-different-report-rendering-extensions.md)   
 [Tabelas, matrizes e listas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-matrices-and-lists-report-builder-and-ssrs.md)  
  
  
