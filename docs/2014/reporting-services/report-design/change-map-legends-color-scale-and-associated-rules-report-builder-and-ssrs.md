---
title: Alterar legendas de mapa, escala de cores e regras (construtor de relatórios e SSRS) associadas | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.shared.maprulesdistribution.f1
- "10512"
- "10539"
- "10533"
- sql12.rtp.rptdesigner.mappointlayerproperties.typerules.f1
- "10534"
- sql12.rtp.rptdesigner.maplegendproperties.general.f1
- sql12.rtp.rptdesigner.mapdistancescaleproperties.general.f1
- "10516"
- sql12.rtp.rptdesigner.mapcolorscaleproperties.labels.f1
- sql12.rtp.rptdesigner.maplegendtitleproperties.general.f1
- "10514"
- sql12.rtp.rptdesigner.shared.mapruleslegend.f1
- sql12.rtp.rptdesigner.mapcolorscaleproperties.general.f1
- sql12.rtp.rptdesigner.shared.embeddedlabels.f1
- "10513"
- sql12.rtp.rptdesigner.mappointlayerproperties.sizerules.f1
- sql12.rtp.rptdesigner.mapcolorscaletitleproperties.general.f1
- "10510"
- "10509"
- "10540"
- "10517"
ms.assetid: a1d691b2-c5ae-420f-af60-b7c54a7385a4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 35ea86d2e03c903736a5900da3da5c10986a3f9f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66106362"
---
# <a name="change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs"></a>Alterar legendas de mapa, escala de cores e regras associadas (Construtor de Relatórios e SSRS)
  Um mapa pode conter legendas de mapa, uma escala de cores e uma escala de distância. Essas partes de um mapa ajudam os usuários a interpretar a visualização de dados no mapa.  
  
 As legendas incluem as seguintes partes de um mapa:  
  
-   **Legenda de mapa** Exibe um guia para ajudar a interpretar os dados analíticos que variam na exibição de elementos de mapas em uma camada do mapa. Um mapa pode ter várias legendas. Para cada camada do mapa, especifique qual legenda deve ser usada. Uma legenda pode fornecer um guia para mais de uma camada do mapa.  
  
-   **Escala de cores** Exibe um guia para ajudar a interpretar as cores no mapa. Um mapa tem uma escala de cores. Várias camadas podem fornecer os dados para a escala de cores.  
  
-   **Escala de distância** Exibe um guia para ajudar a interpretar a escala do mapa. Um mapa tem uma escala de distância. O valor de zoom do visor do mapa atual determina a escala de distância.  
  
 ![rs_MapElements](../media/rs-mapelements.gif "rs_MapElements")  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Viewport"></a> Para alterar a posição de uma legenda em relação ao visor  
  
#### <a name="to-change-the-position-of-a-legend-relative-to-the-viewport"></a>Para alterar a posição de uma legenda em relação ao visor  
  
1.  No modo Design, clique com botão direito na legenda e abra o  _\<relatório de item ->_ **propriedades** página.  
  
2.  Em **Posição**, clique no local que especifica onde exibir a legenda em relação ao visor.  
  
3.  Para exibir a legenda fora do visor, selecione **Mostrar \<item de relatório> fora do visor**.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  Na visualização, as legendas de mapa e a escala de cores aparecem somente quando há resultados de regras relacionadas a essa legenda. Se não houver nenhum item para exibição, a legenda não aparecerá no relatório renderizado.  
  
  
  
##  <a name="MapLegend"></a> Para alterar o layout de uma legenda de mapa  
  
#### <a name="to-change-the-layout-of-a-map-legend"></a>Para alterar o layout de uma legenda de mapa  
  
1.  No modo de exibição de Design, clique com o botão direito do mouse na legenda e abra a página **Propriedades da Legenda** .  
  
2.  Em **Layout da legenda**, clique no layout de tabela que você deseja usar para a legenda. À medida que você clica em opções diferentes, o layout na superfície de design é alterado.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="MapLegendTitle"></a> Para mostrar ou ocultar um título de legenda de mapa  
  
#### <a name="to-show-or-hide-a-map-legend-title"></a>Para mostrar ou ocultar um título de legenda de mapa  
  
-   Clique com o botão direito do mouse na legenda do mapa na superfície de design e clique em **Mostrar Título da Legenda**.  
  
  
  
##  <a name="ColorScaleTitle"></a> Para mostrar ou ocultar um título de escala de cores  
  
#### <a name="to-show-or-hide-a-color-scale-title"></a>Para mostrar ou ocultar um título de escala de cores  
  
-   Clique com o botão direito do mouse na escala de cores na superfície de design e clique em **Mostrar Título da Escala de Cores**.  
  
  
  
##  <a name="MoveItems"></a> Para remover itens da primeira legenda  
 Crie quantas legendas adicionais forem necessárias e atualize as regras de cada camada do mapa, especificando em qual legenda devem ser exibidos os resultados de regras.  
  
#### <a name="to-create-a-new-legend"></a>Para criar uma nova legenda  
  
-   No modo de exibição de Design, clique com o botão direito do mouse no mapa fora do visor do mapa e clique em **Adicionar Legenda**.  
  
     Uma nova legenda será exibida no mapa.  
  
#### <a name="to-display-rule-results-in-a-legend"></a>Para exibir resultados de regra em uma legenda  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com botão direito na camada que tem os dados que você deseja e, em seguida, clique em  _\<tipo de elemento do mapa\>_ **regra de cor**.  
  
3.  Clique em **Legenda**.  
  
4.  Na lista suspensa **Mostrar nesta legenda** , clique no nome da legenda na qual devem ser exibidos os resultados da regra.  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="TemplateStyle"></a> Para variar cores do elemento do mapa com base em um estilo de modelo  
  
#### <a name="to-vary-map-element-colors-based-on-a-template-style"></a>Para variar cores do elemento do mapa com base em um estilo de modelo  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com botão direito na camada que tem os dados que você deseja e, em seguida, clique em  _\<tipo de elemento do mapa\>_ **regra de cor**.  
  
3.  Clique em **Aplicar estilo do modelo**.  
  
     Um estilo de modelo especifica uma fonte, um estilo de borda e uma paleta de cores. Cada elemento do mapa recebe uma cor diferente da paleta de cores para o tema que foi especificado no Assistente de Mapa ou no Assistente de Camada do Mapa. Essa é a única opção que se aplica a camadas que não têm dados analíticos associados.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="ColorPalette"></a> Para variar as cores do elemento do mapa com base em uma paleta de cores  
  
#### <a name="to-vary-map-element-colors-based-on-color-palette"></a>Para variar as cores do elemento do mapa com base em uma paleta de cores  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com botão direito na camada que tem os dados que você deseja e, em seguida, clique em  _\<tipo de elemento do mapa\>_ **regra de cor**.  
  
3.  Clique em **Visualizar dados usando a paleta de cores**.  
  
     Essa opção usa uma paleta interna ou personalizada que você especifica. Com base nos dados analíticos relacionados, cada elemento do mapa recebe uma cor diferente ou tom de cor da paleta.  
  
4.  Em **Campo de dados**, digite o nome do campo que contém os dados analíticos que você deseja visualizar por cor.  
  
5.  Em **Paleta**, na lista suspensa, selecione o nome da paleta a ser usada.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="ColorRanges"></a> Para variar as cores do elemento do mapa com base em intervalos de cores  
  
#### <a name="to-vary-map-element-colors-based-on-color-ranges"></a>Para variar as cores do elemento do mapa com base em intervalos de cores  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com botão direito na camada que tem os dados que você deseja e, em seguida, clique em  _\<tipo de elemento do mapa\>_ **regra de cor**.  
  
3.  Clique em **Visualizar dados usando intervalos de cores**.  
  
     Essa opção, aliada às cores inicial, intermediária e final que você especifica nessa página e as opções especificadas na página **Distribuição** , divide os dados analíticos relacionados em intervalos. O processador de relatório atribui a cor apropriada a cada elemento do mapa com base nos dados associados e no intervalo em que se enquadra.  
  
4.  Em **Campo de dados**, digite o nome do campo que contém os dados analíticos que você deseja visualizar por cor.  
  
5.  Em **Cor inicial**, especifique a cor a ser usada para o intervalo mais baixo.  
  
6.  Em **Cor Intermediária**, especifique a cor a ser usada para o intervalo intermediário.  
  
7.  Em **Cor final**, especifique a cor a ser usada para o intervalo mais alto.  
  
8.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="CustomColors"></a> Para variar as cores do elemento do mapa com base em cores personalizadas  
  
#### <a name="to-vary-map-element-colors-based-on-custom-colors"></a>Para variar as cores do elemento do mapa com base em cores personalizadas  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com botão direito na camada que tem os dados que você deseja e, em seguida, clique em  _\<tipo de elemento do mapa\>_ **regra de cor**.  
  
3.  Clique em **Visualizar dados usando cores personalizadas**.  
  
     Essa opção usa a lista de cores especificada por você. Com base nos dados analíticos relacionados, cada elemento do mapa recebe uma cor da lista. Se houver mais elementos do mapa do que cores, nenhuma cor será atribuída.  
  
4.  Em **Campo de dados**, digite o nome do campo que contém os dados analíticos que você deseja visualizar por cor.  
  
5.  Em **Cores personalizadas**, clique em **Adicionar** para especificar cada cor personalizada.  
  
6.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="DistributionOptions"></a> Para definir as opções de distribuição de uma legenda  
  
#### <a name="to-set-distribution-options-for-a-legend"></a>Para definir as opções de distribuição de uma legenda  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com botão direito na camada que tem os dados que você deseja e, em seguida, clique em  _\<tipo de elemento do mapa\>_ **regra de cor**.  
  
3.  Selecione o **visualizar dados usando** \<tipo de regra\> opção. Para usar as opções de distribuição, você deve criar intervalos na página **Distribuição** com base nos dados analíticos associados à camada.  
  
4.  Clique em **Distribuição**.  
  
5.  Selecione um dos seguintes tipos de distribuição:  
  
    -   **EqualInterval**. Especifica intervalos que dividem os dados em intervalos iguais.  
  
    -   **EqualDistribution**. Especifica intervalos que dividem esses dados de forma que cada intervalo tenha um número de itens igual.  
  
    -   **Ideal**. Especifica os intervalos que ajustam automaticamente a distribuição para criar subintervalos equilibrados.  
  
    -   **Personalizar**. Especifique seu próprio número de intervalos para controlar a distribuição de valores.  
  
     Para obter mais informações sobre as opções de distribuição, consulte [Variar a exibição de polígono, linha e ponto por regras e dados analíticos &#40;Construtor de Relatórios e SSRS&#41;](vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).  
  
6.  Em **Número de subintervalos**, digite o número de subintervalos a ser usado. Quando o tipo de distribuição for **Ideal**, o número de subintervalos será calculado automaticamente.  
  
7.  Em **Início do intervalo**, digite um valor de intervalo mínimo. Todos os valores menores do que esse número são iguais ao intervalo mínimo.  
  
8.  Em **Fim do intervalo**, digite um valor de intervalo máximo. Todos os valores maiores do que esse número são iguais ao intervalo máximo.  
  
9. [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="RuleLegend"></a> Para alterar o conteúdo de uma legenda de regras  
  
#### <a name="to-change-the-contents-of-a-color-size-width-or-marker-type-legend"></a>Para alterar o conteúdo da legenda de cor, tamanho, largura ou tipo de marcador  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com botão direito na camada que tem os dados que você deseja e, em seguida, clique em  _\<tipo de elemento do mapa\>_ **regra**.  
  
3.  Verifique se a opção **Visualizar dados usando** \<*tipo de regra*> está selecionada.  
  
4.  Em **Campo de dados**, verifique se os dados analíticos visualizados na camada estão selecionados.  
  
    > [!NOTE]  
    >  Se nenhum campo aparecer na lista suspensa, clique com o botão direito do mouse na camada e clique em **Dados da Camada** para abrir a caixa de diálogo Propriedades de Dados da Camada do Mapa, página Dados Analíticos e verificar se você especificou dados analíticos para essa camada.  
  
5.  Clique em **Legenda**.  
  
6.  Em **Mostrar nesta legenda**, selecione a legenda do mapa a ser usada para exibir os resultados da regra.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="ColorScale"></a> Para alterar o conteúdo da escala de cores  
  
#### <a name="to-change-the-contents-of-the-color-scale-or-a-color-legend"></a>Para alterar o conteúdo da escala de cores ou de uma legenda de cor  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com botão direito na camada que tem os dados que você deseja e, em seguida, clique em  _\<tipo de elemento do mapa\>_ **regra de cor**.  
  
3.  Selecione a opção de regra de cor a ser usada. Para exibir itens em uma legenda do mapa ou escala de cores, você deve selecionar uma das opções de **Visualizar dados usando** \<tipo de regra>.  
  
4.  Em **Campo de dados**, verifique se os dados analíticos visualizados na camada estão selecionados.  
  
    > [!NOTE]  
    >  Se nenhum campo aparecer na lista suspensa, clique com o botão direito do mouse na camada e clique em **Dados da Camada** para abrir a caixa de diálogo Propriedades de Dados da Camada do Mapa, página Dados Analíticos e verificar se você especificou dados analíticos para essa camada.  
  
5.  Clique em **Legenda**.  
  
6.  Em **Opções de escala de cores**, selecione **Mostrar na escala de cores** para exibir os resultados da regra na escala de cores. Você pode especificar esta opção para mais de uma regra de cor.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="HideItems"></a> Para remover todos os itens de uma legenda  
  
#### <a name="to-hide-items-based-on-a-rule"></a>Para ocultar itens com base em uma regra  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com botão direito na camada que tem os dados que você deseja e, em seguida, clique em  _\<tipo de elemento do mapa\>_ **regra**.  
  
3.  Clique em **Legenda**.  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
##  <a name="ChangeFormatItems"></a> Para alterar o formato de conteúdo em uma legenda  
 Defina as opções de legenda para a regra associada à legenda de mapa.  
  
#### <a name="to-change-the-format-of-content-in-a-legend"></a>Para alterar o formato de conteúdo em uma legenda  
  
1.  No modo Design, clique no mapa até que o painel Mapa seja exibido.  
  
2.  Clique com botão direito na camada que tem os dados que você deseja e, em seguida, clique em  _\<tipo de elemento do mapa\>_ **regra**.  
  
3.  Clique em **Legenda**.  
  
4.  O**Texto de legenda** exibe as palavras-chave que especificam quais dados são exibidos na legenda. Use as palavras-chave do mapa e os formatos personalizados para ajudar a controlar o formato do texto da legenda. Por exemplo, #FROMVALUE {C2} especifica um formato de moeda com duas casas decimais. Para obter mais informações, consulte [Variar a exibição de polígono, linha e ponto por regras e dados analíticos &#40;Construtor de Relatórios e SSRS&#41;](vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
  
  
## <a name="see-also"></a>Consulte também  
 [Mapas &#40;Construtor de Relatórios e SSRS&#41;](maps-report-builder-and-ssrs.md)   
 [Adicionar, alterar ou excluir um mapa ou uma camada do mapa &#40;Construtor de Relatórios e SSRS&#41;](add-change-or-delete-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [Personalizar os dados e a exibição de um mapa ou de uma camada do mapa &#40;Construtor de Relatórios e SSRS&#41;](customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [Solucionar problemas de relatórios: Mapear relatórios &#40;Construtor de Relatórios e SSRS&#41;](troubleshoot-reports-map-reports-report-builder-and-ssrs.md)   
 [Assistente de Mapa e Assistente de Camada do Mapa &#40;Construtor de Relatórios e SSRS&#41;](map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
  
  
