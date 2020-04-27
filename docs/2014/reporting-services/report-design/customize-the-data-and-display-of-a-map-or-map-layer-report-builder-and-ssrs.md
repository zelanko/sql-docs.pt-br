---
title: Personalizar os dados e a exibição de um mapa ou de uma camada do mapa (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10521"
- sql12.rtp.rptdesigner.shared.shadowdv.f1
- "10515"
- "10512"
- "10520"
- "10523"
- sql12.rtp.rptdesigner.mapgroupproperties.variables.f1
- sql12.rtp.rptdesigner.mapgroupproperties.filter.f1
- sql12.rtp.rptdesigner.shared.number.f1
- sql12.rtp.rptdesigner.shared.font.f1
- sql12.rtp.rptdesigner.mapgroupproperties.general.f1
- "10507"
ms.assetid: fdd9b994-d138-4990-a291-279b0249eb72
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3cc939ac63f1b53e2d2d24d70edc5fe0798bcc51
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66106103"
---
# <a name="customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs"></a>Personalizar os dados e a exibição de um mapa ou de uma camada do mapa (Construtor de Relatórios e SSRS)
  Depois de adicionar um mapa ou uma camada do mapa a um relatório usando um assistente, você poderá alterar a aparência do mapa no relatório. Você pode fazer melhorias considerando as seguintes ideias:  
  
-   Para ajudar os usuários a compreender como interpretar a exibição de dados em um mapa, você pode adicionar legendas e uma escala de cores, e adicionar rótulos e dicas de ferramentas.  
  
-   Para facilitar a leitura do mapa, altere o centro e o nível de zoom, adicione uma escala de distância e exiba uma grade em segundo plano.  
  
-   Para ajudar a controlar o tempo de desenho do mapa ao executar o relatório, você pode ajustar a resolução para simplificar os elementos do mapa.  
  
-   Você pode inserir elementos do mapa na definição de relatório e alterar a aparência de elementos individuais. Por exemplo, você pode exibir o principal local de escritório com um pino e outros locais de escritório com círculos.  
  
-   Você pode adicionar regiões personalizadas especificando suas próprias expressões de grupos de dados.  
  
-   Você pode adicionar um local personalizado em um ponto especificado de uma camada do mapa que possui pontos inseridos. Você pode definir o valor e exibir propriedades para pontos personalizados, sejam quais forem os outros pontos em uma camada de ponto.  
  
-   Para fornecer mais detalhes, você pode adicionar links a elementos do mapa em cada camada que um usuário pode clicar para abrir relatórios relacionados.  
  
 Para obter mais ideias sobre como aprimorar um relatório, consulte [Planejando um relatório &#40;Construtor de Relatórios&#41;](planning-a-report-report-builder.md).  
  
 Opções de exibição afetam o modo como um mapa ou as partes de um mapa aparecem quando você exibe o relatório. Algumas opções controlam a aparência do mapa, tais como as bordas e fontes ou a área representada no mapa. Outras opções controlam o conteúdo de cada camada, como tamanhos de bolha, tipos de marcador, rótulos ou dicas de ferramenta.  
  
 Um item de relatório de mapa inclui as seguintes partes: o mapa propriamente dito, um visor do mapa, um conjunto de títulos, um conjunto de legendas (legenda, escala de cores e escala de distância) um conjunto de camadas, um conjunto de elementos de mapa em cada camada (polígonos, linhas ou pontos). Use as informações nas seções a seguir para compreender qual caixa de diálogo de propriedade controla as opções de exibição para as diferentes partes de um mapa.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="change-options-for-the-map"></a><a name="Map"></a> Alterar as opções do mapa  
 Em um item de relatório de mapa, você pode controlar o seguinte:  
  
-   Adicionar vários títulos.  
  
-   Adicionar várias legendas. Para alterar o conteúdo de uma legenda, você precisa criar legendas adicionais e alterar as regras para especificar a legenda na qual inserirá os itens de legenda criados por cada regra.  
  
-   Adicionar mais camadas.  
  
-   Ocultar ou mostrar a escala de distância ou a escala de cores.  
  
-   Dê a ilusão de profundidade especificando uma sombra.  
  
 Para alterar essas opções, clique com o botão direito do mouse no mapa, clique em **Mapa**e altere as opções.  
  
 
  
##  <a name="change-options-for-the-viewport"></a><a name="Viewport"></a> Alterar as opções do visor  
 Use as opções do visor para alterar a exibição do mapa que aparece em seu relatório.  
  
 A origem de dados espaciais pode fornecer mais área do que você precisa para exibir no relatório. Você pode usar o visor para definir o centro, o nível de zoom, e cortar a área para o mapa.  
  
 As seguintes opções podem ser definidas para o visor:  
  
-   Escolha o sistema de coordenadas e, para um sistema geográfico de coordenadas, escolha a projeção.  
  
-   Escolha o centro do mapa.  
  
-   Corte a exibição do mapa.  
  
-   Define o nível de zoom.  
  
-   Resolução e simplificação. Escolha um equilíbrio entre o tempo de desenho e contornos detalhados para linhas e polígonos.  
  
 Para alterar estas opções, clique com o botão direito do mouse no visor do mapa, use a página [Caixa de diálogo Propriedades do Visor do Mapa, Geral](../map-viewport-properties-dialog-box-general.md) e as páginas relacionadas.  
  

  
##  <a name="change-options-for-the-legends"></a><a name="Legends"></a> Alterar as opções das legendas  
 As legendas ajudam os usuários a interpretar os dados em um mapa.  
  
 Por padrão, todas as regras especificadas para uma camada adicionam itens à primeira legenda. Além disso, todas as regras de cores exibem valores na escala de cores.  
  
-   Para alterar as opções de exibição da aparência da legenda, inclusive sua posição em relação ao visor, defina as opções na própria legenda.  
  
-   Para alterar o conteúdo ou o formato do conteúdo de uma legenda, altere as opções da legenda para as regras correspondentes de uma camada.  
  
 Para obter mais informações, consulte [Alterar legendas de mapa, escala de cores e regras associadas &#40;Construtor de Relatórios e SSRS&#41;](change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md).  
  

  
##  <a name="change-options-for-the-layer"></a><a name="Layer"></a> Alterar as opções da camada  
 Para exibir as camadas de um mapa, clique no mapa para selecioná-lo. O painel de Mapa aparece. Para alterar opções de uma camada, clique com o botão direito do mouse na camada e use o menu de atalho.  
  
 Uma camada pode ser de três tipos, dependendo dos dados espaciais que são retornados pela fonte de dados espaciais: uma camada de polígono, uma camada de linha ou uma camada de ponto.  
  
 As seguintes opções podem ser definidas para a camada:  
  
-   Os dados analíticos associados e campos correspondentes. A origem dos dados espaciais é listada no painel de Mapa sob o nome da camada. Quando a origem é inserida, os elementos do mapa da camada fazem parte da definição de relatório. Se a origem não for inserida, os dados espaciais serão recuperados em tempo de execução e o processador de relatório criará os elementos de mapas para a camada quando o relatório for processado. Para alterar opções de dados na camada, use a página Dados Analíticos na caixa de diálogo Camada do Mapa.  
  
-   Ordem de desenho de camada. A ordem em que as camadas estão listadas no painel de Mapa é a ordem inversa de desenho das camadas. A última camada da lista é desenhada primeiro. Por exemplo, para que os pontos de uma camada de ponto apareçam sobre os polígonos na camada de polígono, a camada de ponto deve ser a primeira e a camada de polígono deve ser a segunda.  
  
-   Visibilidade da camada, inclusive a transparência. Para poder enxergar uma camada sobre a outra, defina a transparência com um valor superior a 0. Um valor de 100% significa que a camada não é visível. Para trabalhar com uma camada individual, você pode facilmente mostrar ou ocultar cada camada separadamente usando o ícone de **Visibilidade** no painel de Mapa. Você também pode definir opções de nível de zoom para especificar quando elementos de mapas devem ser mostrados ou ocultados na camada com base no nível de zoom.  
  
-   Adicione uma camada lado a lado de mapa do Bing para o centro do visor atual e nível de zoom. Você não precisa especificar as coordenadas geográficas para uma camada lado a lado. As peças são carregadas automaticamente para corresponder à área de visor quando o sistema de coordenadas é Geográfico, a projeção é Mercator, os servidores de Bing Maps estão disponíveis, e quando o servidor de relatório está configurado para dar suporte a este recurso. Para cada relatório, você pode especificar se deseja usar uma conexão segura para recuperar peças.  
  
 Para obter mais informações sobre as camadas, consulte [Adicionar, alterar ou excluir um mapa ou uma camada do mapa &#40;Construtor de Relatórios e SSRS&#41;](add-change-or-delete-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
##  <a name="change-data-grouping-for-the-layer"></a><a name="DataGrouping"></a> Alterar agrupamento de dados para a camada  
 Você pode personalizar o modo de agregar dados espaciais para suas próprias formas. Para definir as propriedades do grupo de uma camada, selecione a camada no painel Mapa e, no painel Propriedades da camada, clique em **Grupo** e, em seguida, clique nas reticências (…) para abrir as propriedades do grupo. Nesta caixa de diálogo, você pode especificar expressões de grupo, criar variáveis de grupo e filtrar dados que são usados para agrupar.  
  
 A expressão de grupo especifica o modo como os dados analíticos que têm uma relação com dados espaciais são agregados para cada elemento do mapa na camada. Por padrão, a expressão de grupo é o conjunto de campos de correspondência especificado para a relação entre os dados espaciais e os dados analíticos. Por exemplo, para um mapa de bolhas que exibe locais de cidade e o tamanho da população de um país ou região, os campos de correspondência incluem o nome da cidade [Cidade] e o nome da região [Região], porque pode haver várias cidades com o mesmo nome. A expressão de grupo correspondente inclui dois campos: [Cidade] e [Região].  
  
 Para obter mais informações, consulte [Dicas de mapa: como importar arquivos de forma no SQL Server e agregar dados espaciais](https://go.microsoft.com/fwlink/?LinkID=214991).  
  
 
  
##  <a name="change-options-for-the-map-elements-on-the-layer"></a><a name="MapElements"></a> Alterar opções dos elementos de mapas na camada  
 Elementos de mapas são os pontos, linhas ou polígonos em uma camada que se baseiam nos dados espaciais. As opções a seguir podem ser definidas para elementos de mapas. Estas opções se aplicam a todos os elementos de mapas na camada, estejam eles inseridos ou não:  
  
-   Rótulos, visibilidade do rótulo, deslocamento do rótulo e formatação.  
  
-   Bordas e preenchimento.  
  
-   Ações de detalhamento.  
  
-   Opções de exibição.  
  
 As opções de exibição para elementos de mapas seguem uma ordem de precedência com base na camada, no elemento de mapa, nas regras do elemento de mapa e nas opções de substituição de elementos de mapas inseridos.  
  
 Para alterar estas opções, clique com o botão direito do mouse no elemento de mapa, use a caixa de diálogo de propriedades inserida. Por exemplo, para um polígono inserido, use a caixa de diálogo Mapear Propriedades de Polígono Inserido, página Geral e as páginas relacionadas.  
  

  
##  <a name="understanding-display-option-precedence"></a><a name="Precedence"></a> Compreendendo a precedência de opções de exibição  
 Para controlar a aparência de exibição de um ponto, uma linha ou um polígono em uma camada do mapa, é preciso compreender onde é possível definir as opções de exibição e quais delas têm maior precedência. As opções de exibição a seguir estão listadas da inferior à superior. Opções de exibição superior substituem opções de exibição inferior nesta lista:  
  
-   Opções de camada.  
  
-   Opções de Pontos, Linhas ou Polígonos em cada camada. Isto se aplica se os elementos de mapas são recuperados dinamicamente quando o relatório é processado ou se os elementos de mapas são inseridos na definição de relatório. Por exemplo, você especifica uma cor de preenchimento para todos os elementos de uma camada.  
  
-   Regras. Você pode estabelecer regras para controlar cor, tamanho, largura ou tipo de marcador para todos os elementos de mapas em uma camada. As regras que você pode definir dependem do tipo de elemento de mapa.  
  
    -   Regras de cores. Aplica-se a marcadores para pontos, linhas, polígonos e marcadores para pontos centrais do polígono.  
  
    -   Regras de tamanho. Aplique a marcadores para pontos e marcadores para pontos centrais do polígono.  
  
    -   Regras de largura. Aplica-se a larguras de linha.  
  
    -   Regras de tipo de marcador. Aplica-se a marcadores para pontos e marcadores para pontos centrais do polígono.  
  
-   Substituir opções para pontos inseridos individuais, linhas ou polígonos em uma camada. As alterações que você faz são permanentes. Para reverter estas alterações, recarregue os dados da camada.  
  
 Para obter mais informações, consulte [Variar a exibição de polígono, linha e ponto por regras e dados analíticos &#40;Construtor de Relatórios e SSRS&#41;](vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).  
  

  
## <a name="see-also"></a>Consulte Também  
 [Assistente de Mapa e Assistente de Camada do Mapa &#40;Construtor de Relatórios e SSRS&#41;](map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md)   
 [Mapas &#40;Construtor de Relatórios e SSRS&#41;](maps-report-builder-and-ssrs.md)  
  
  
