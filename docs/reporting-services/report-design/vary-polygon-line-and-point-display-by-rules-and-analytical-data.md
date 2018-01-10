---
title: "Variar a exibição de polígono, linha e ponto por regras e dados analíticos | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: report-design
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- "10538"
- "10537"
- sql13.rtp.rptdesigner.mapembeddedpolygonlayerproperties.general.f1
- MICROSOFT.REPORTDESIGNER.MAPMARKER.MARKERSTYLE
- sql13.rtp.rptdesigner.mapembeddedlinelayerproperties.general.f1
- sql13.rtp.rptdesigner.mapembeddedpointlayerproperties.general.f1
- "10531"
- "10536"
- sql13.rtp.rptdesigner.maplinelayerproperties.widthrules.f1
ms.assetid: 7f1f5584-37b4-4fa2-ae44-8988c5f0c744
caps.latest.revision: "12"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 428f89c51b60f1e9f33170ab03cb43a87caf6a78
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="vary-polygon-line-and-point-display-by-rules-and-analytical-data"></a>Vary Polygon, Line, and Point Display by Rules and Analytical Data
  As opções de exibição para polígonos, linhas e pontos em uma camada do mapa são controladas pela definição de opções para a camada, estabelecendo regras para os elementos do mapa na camada ou substituindo opções para elementos de mapas inseridos específicos em uma camada.  
  
 As opções de exibição são aplicadas em uma precedência específica, listadas da precedência mais baixa para a mais alta:  
  
1.  As opções definidas em uma camada de polígono, uma camada de linha e uma camada de ponto se aplicam a todos os elementos do mapa nessa camada, quer os elementos do mapa sejam inseridos ou não na definição de relatório.  
  
2.  As opções definidas para regras se aplicam a todos os elementos do mapa em uma camada. Todas as opções de visualização de dados se aplicam apenas a elementos do mapa que são associados a dados espaciais. Uma opção de visualização de dados requer que você especifique um campo de dados no qual basear as variações de exibição. Você deve ter definido os campos de correspondência para os dados analíticos e espaciais antes de aplicar regras de visualização de dados. Para obter mais informações, consulte [Mapas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md).  
  
3.  Opções que você define para elementos do mapa inseridos selecionados. Observe que, quando você substitui as opções da camada, as alterações feitas na definição de relatório são permanentes. Você pode alterar os valores de campo de dados e substituir opções de exibição para personalizar a maneira como polígonos específicos, linhas e pontos aparecem em uma camada.  
  
 Além de controlar a exibição de elementos do mapa em uma camada, você pode controlar a transparência da camada para permitir que camadas desenhadas anteriormente apareçam através de camadas desenhadas posteriormente. Para obter mais informações sobre como alterar opções que afetam o mapa o toda a camada do mapa, consulte [Personalizar os dados e a exibição de um mapa ou de uma camada do mapa &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="Rules"></a> Compreendendo regras  
 Você pode definir quatro tipos de regras que o processador de relatório ajuste as propriedades de exibição automaticamente para elementos do mapa em uma camada. As regras variam de acordo com o tipo de elemento do mapa: polígonos, linhas ou pontos.  
  
-   **Polígonos.** Varie a cor do polígono.  
  
    -   **Pontos centrais de polígonos.** Para marcadores exibidos no ponto central de cada polígono, varie a cor, o tamanho e o tipo de marcador.  
  
-   **Linhas.** Varie a cor e a largura da linha.  
  
-   **Pontos.** Para marcadores exibidos para cada ponto, varie a cor, o tamanho e o tipo de marcador.  
  
##  <a name="Color"></a> Compreendendo regras de cor  
 As regras de cores se aplicam a cores de preenchimento para polígonos, linhas e marcadores que representam pontos ou pontos centrais de polígono.  
  
 As regras de cores oferecem suporte a quatro opções:  
  
-   Aplique o estilo do modelo. O tema que você escolheu no assistente define o estilo do modelo para a camada. O tema define o estilo da fonte, o estilo da borda e a paleta.  
  
-   Visualize os dados usando a paleta de cores. Especifique uma paleta pelo nome. O processador de relatório define a cor de cada elemento do mapa em uma camada percorrendo cada cor na paleta e aplicando sucessivamente tons mais claros de cada cor na paleta.  
  
-   Visualize os dados usando intervalos de cores. Especifique uma cor inicial, intermediária e final. Em seguida, especifique opções de distribuição. O processador de relatório usa os valores de opção de distribuição para criar um conjunto de cores que gera uma exibição semelhante para um mapa de calor. Uma mapa de calor exibe a cor em relação à temperatura. Por exemplo, em uma escala de 0 a 100, valores baixos são azuis para representar frio e valores altos são vermelhos para representar calor.  
  
-   Visualize os dados usando cores personalizadas. Especifique um conjunto de cores. O processador de relatório define a cor de cada elemento do mapa na camada percorrendo os valores especificados por você.  
  
 A paleta padrão incluir a cor branca. Para evitar o contraste forte entre o branco e as outras cores na paleta, especifique uma cor inicial que seja clara na paleta.  
  
 Para exibir elementos do mapa não associados a dados como incolores, defina **Sem Cor** como a cor padrão dos elementos de mapa na camada.  
  
### <a name="color-scale"></a>Escala de cores  
 Por padrão, todos os valores de regras de cores aparecem na escala de cores, além de aparecer na primeira legenda. A escala de cores é criada para exibir um intervalo de cores. Escolha os dados mais importantes a serem exibidos na escala de cores.  
  
 Para remover os valores que você não deseja na escala de cores, desmarque a opção de escala de cores de cada regra de cor em todas as camadas.  
  
##  <a name="Width"></a> Compreendendo regras de largura de linha  
 As regras de largura se aplicam a linhas. As regras de largura têm suporte para duas opções:  
  
-   Use uma largura de linha padrão. Especifique a largura da linha em pontos.  
  
-   Visualize dados usando a largura da linha. Defina as larguras mínima e máxima para a linha, especifique o campo de dados a ser usado para variar a largura e especifique as opções de distribuição a serem aplicadas aos dados.  
  
##  <a name="Size"></a> Compreendendo regras de tipo de tamanho de marcador  
 As regras de tamanho se aplicam a marcadores que representam pontos ou pontos centrais de polígono. As regras de tamanho têm suporte para duas opções:  
  
-   Use um tamanho de marcador padrão. Especifique o tamanho em pontos.  
  
-   Visualize dados usando tamanho. Defina os tamanhos mínimo e máximo para o marcador, especifique o campo de dados a ser usado para variar o tamanho e especifique as opções de distribuição a serem aplicadas aos dados.  
  
##  <a name="Marker"></a> Compreendendo regras de tipo de marcador  
 As regras de tipo de marcador se aplicam a marcadores que representam pontos ou pontos centrais de polígono. As regras de tipo de marcador têm suporte para duas opções:  
  
-   Use um tipo de marcador padrão. Você especifica um dos tipos de marcador disponíveis.  
  
-   Visualize dados usando marcadores. Você especifica um conjunto de marcadores e especifica a ordem na qual deseja que sejam usados. Os tipos de marcadores incluem **Círculo**, **Losango**, **Pentágono**, **Pino**, **Retângulo**, **Estrela**, **Triângulo**, **Trapézio**e **Borda**.  
  
##  <a name="Distribution"></a> Compreendendo opções de distribuição  
 Para criar uma distribuição de valores, você pode dividir os dados em intervalos. Especifique o tipo de distribuição, o número de subintervalos e os valores de intervalo mínimo e máximo.  
  
 Na lista a seguir, vamos supor que você tenha três elementos de mapa e seis valores analíticos relacionados que variam de 1 a 9999 com os valores seguintes: 1, 10, 200, 2000, 4777, 8999.  
  
-   **EqualInterval** . Crie intervalos que dividam os dados em intervalos iguais. Para o exemplo, os três intervalos seriam 0-2999, 3000-5999, 6000-8999. Subintervalo 1: 1, 10, 200, 500. Subintervalo 2: 4777. Subintervalo 3: 8999. Esse método não considera o modo como os dados são distribuídos. Valores muito grandes ou muito pequenos podem afetar os resultados da distribuição.  
  
-   **EqualDistribution.** Crie intervalos que dividam esses dados de forma que cada intervalo tenha um número de itens igual. Para os dados de exemplo, os três intervalos seriam 0-10, 11-500, 501-8999. Subintervalo 1: 1, 10. Subintervalo 2: 200, 500. Subintervalo 3: 4777, 8999. Este método pode afetar a distribuição criando divisões que abrangem intervalos muito grandes ou muito pequenos.  
  
-   **Ideal.** Crie intervalos que ajustem automaticamente a distribuição para criar subintervalos equilibrados. O número de subintervalos é determinado pelo algoritmo.  
  
-   **Personalizado.** Especifique seu próprio número de intervalos para controlar a distribuição de valores. Para os dados do exemplo, você pode especificar 3 intervalos: 1-2, 3-8, 9.  
  
 Os valores de distribuição são usados pelas regras para variar os valores de exibição do elemento do mapa.  
  
##  <a name="Legends"></a> Compreendendo legendas e itens de legenda  
 Os itens de legenda são criados automaticamente a partir das regras que você especifica para cada camada. As opções de regras controlam quantos itens são criados e em qual legenda aparecem. Por padrão, todos os itens de todas as regras são adicionados na primeira legenda. Para mover itens para fora da primeira legenda, crie tantas legendas adicionais quanto precisar e, para cada regra, especifique a legenda a ser usada para exibir os itens resultantes da regra. Para ocultar itens com base em uma regra, especifique um nome de legenda em branco.  
  
 Para controlar onde uma legenda aparece, use a caixa de diálogo Propriedades da Legenda para especificar uma posição relativa ao visor do mapa. Para obter mais informações, consulte [Alterar legendas de mapa, escala de cores e regras associadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md).  
  
 As legendas são expandidas automaticamente para exibir o título ou o texto da legenda. Para formatar o texto dos itens da legenda, use palavras-chave de legenda de mapa e formatos personalizados. Para obter mais informações, consulte [Para alterar o formato de conteúdo em uma legenda](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md#ChangeFormatItems).  
  
 As tabelas a seguir mostram exemplos de formatos diferentes que você pode usar.  
  
|Palavra-chave e formato|Description|Exemplo do que é exibido como texto na legenda|  
|------------------------|-----------------|---------------------------------------------------|  
|`#FROMVALUE {C0}`|Exibe a moeda do valor total sem casas decimais|$ 400|  
|`#FROMVALUE {C2}`|Exibe a moeda do valor total com até duas casas decimais.|$ 400,55|  
|`#TOVALUE`|Exibe o valor numérico real do campo de dados.|10000|  
|`#FROMVALUE{N0} - #TOVALUE{N0}`|Exibe os valores numéricos reais do início e do fim do intervalo.|10 - 790|  
  
## <a name="see-also"></a>Consulte Também  
 [Alterar legendas de mapa, escala de cores e regras associadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md)   
 [Mapas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Assistente de Mapa e Assistente de Camada do Mapa &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)  
  
  
