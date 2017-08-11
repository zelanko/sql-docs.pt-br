---
title: "Solucionar problemas de relatórios: Mapear relatórios (construtor de relatórios e SSRS) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a690aec2-056b-40bc-8cab-c694bd2d6d62
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 488c17afabc7dc828ccf88ed1e058f1e13c7e0b2
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="troubleshoot-reports-map-reports-report-builder-and-ssrs"></a>Solução de problemas de relatórios: relatórios de mapa (Construtor de Relatórios e SSRS)
  Os problemas com mapas em um relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] podem ocorrer quando você adiciona um mapa ou camada do mapa ao relatório, quando você personaliza um mapa existente ou camada do mapa em seu relatório, quando visualiza um mapa em um relatório ou quando publica um relatório com um mapa. Use este tópico para ajudar a solucionar esses problemas.  
    
   ## <a name="need-more-help"></a>Precisa de mais ajuda?  
   
  Experimente:  
 *  Fórum do MSDN para [SQL Server 2016](https://social.msdn.microsoft.com/forums/sqlserver/en-us/home?forum=sqlserver2016)  
 * [SQL Server 2016](http://stackoverflow.com/questions/tagged/sql-server-2016) no Stack Overflow  
 * Registre um problema ou sugestão no [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback)  
  
##  <a name="Embedded"></a> Problemas de tamanho da definição de relatório  
 Use esta seção para ajudar a resolver problemas relacionados ao tamanho da definição do relatório.  
  
## <a name="how-do-i-reduce-the-report-definition-size"></a>Como eu reduzo o tamanho da definição de relatório?  
 Uma camada do mapa contém elementos do mapa que são criados com base em dados espaciais. Em alguns casos, os elementos do mapa são inseridos na definição de relatório. Isso acontece dos seguintes modos:  
  
-   Se a fonte de dados espaciais vier de um mapa na Galeria de Mapas ou de um Arquivo de Forma ESRI no computador local, elementos do mapa serão inseridos automaticamente na definição de relatório.  
  
     Se você publicar um relatório no servidor de relatório e houver uma referência de fonte de dados espaciais a um arquivo local, os dados espaciais não poderão ser recuperados em tempo de processamento de relatório. Para evitar esse problema, os dados são inseridos na definição do relatório.  
  
-   No assistente de Mapa ou assistente de Camada, se você selecionar a opção para inserir dados espaciais, elementos do mapa com base nos dados espaciais serão inseridos na camada do mapa na definição de relatório.  
  
-   No painel Mapa, se você clicar com o botão direito do mouse na camada e depois clicar em uma das opções **Inserir Dados Espaciais** , os elementos do mapa com base nos dados espaciais serão inseridos na camada do mapa na definição de relatório.  
  
-   Para remover dados inseridos com base em um Arquivo de Forma ESRI de uma definição de relatório, você deve fazer o seguinte:  
  
1.  Carregue ou publique os arquivos ESRI .shp e .dbf no servidor de relatório.  
  
2.  No relatório, no painel Mapa no modo Design, selecione a camada tem dados inseridos e abra as propriedades de **Dados da Camada** . Em **Usar dados espaciais de**, selecione **Link para Arquivo de Forma ESRI**e vá para a pasta no servidor de relatório que contém os Arquivos de Forma ESRI, selecione-a e clique em OK.  
  
3.  Salve o relatório. Os dados inseridos para a camada que você alterou foram removidos da definição de relatório.  
  
 Elementos do mapa de um relatório na Galeria de Mapas sempre serão inseridos em uma camada do mapa.  
  
##  <a name="Spatial"></a> Problemas de dados espaciais  
 Use esta seção para ajudar a resolver problemas relacionados a dados espaciais.  
  
## <a name="on-the-design-surface-i-see-sample-spatial-data"></a>Na superfície de design, eu vejo dados espaciais de exemplo  
 Em tempo de design, a superfície de design talvez mostre a mensagem sobre dados espaciais de exemplo pelos seguintes motivos:  
  
-   Os dados espaciais vêm de um arquivo ESRI .shp, mas o arquivo .dbf correspondente não está disponível. Os Arquivos de Formas ESRI geralmente incluem um arquivo .shp com dados espaciais e um arquivo .dbf de suporte. Verifique se o arquivo .dbf está no mesmo diretório do arquivo .shp.  
  
-   Os dados espaciais vêm de um conjunto de dados e a conexão de dados para a consulta não é válida ou as credenciais atuais não são válidas.  
  
-   A camada do mapa contém uma propriedade com uma expressão. As expressões não são avaliadas até a execução do relatório. Para visualizar o mapa, visualize o relatório.  
  
-   Os dados espaciais vêm de um conjunto de dados que tem um escopo específico. Por exemplo, quando um mapa é aninhado em uma região de dados tablix, ou o mapa usa o mesmo escopo de conjunto de dados para dados analíticos e dados espaciais, o escopo de dados somente é calculado após a execução do relatório.  
  
## <a name="when-i-set-an-offset-for-an-individual-map-element-a-cluster-of-map-elements-move"></a>Quando eu defino um deslocamento para um elemento do mapa individual, um cluster de elementos do mapa é movido  
 Os dados espaciais definem os elementos do mapa que são exibidos em cada camada do mapa. Um elemento de mapa pode se basear nos dados espaciais que constituem um único ponto, um conjunto de pontos, uma única linha, um conjunto de linhas, um único polígono ou um conjunto de polígonos. Cada elemento de mapa é uma unidade. Se um elemento de mapa contiver vários pontos, e você movê-lo, todos os pontos desse elemento de mapa serão movidos.  
  
 Os dados de cada elemento de mapa são determinados pelo formato dos dados espaciais da fonte externa. Por exemplo, quando uma consulta especifica dados espaciais de um banco de dados do SQL Server, cada linha no conjunto de resultados pode conter vários conjuntos de ponto ou linha ou coordenadas de polígono. Todos os elementos do mapa definidos por uma única linha no conjunto de resultados são tratados como uma unidade. Para variar a exibição de conjuntos de coordenadas específicos, siga um destes procedimentos:  
  
-   Altere a consulta para retornar os conjuntos de coordenadas como linhas separadas no conjunto de resultados.  
  
-   Selecione os elementos do mapa para variar e defina o ponto inserido correspondente, a linha ou as propriedades do polígono substituindo as propriedades de exibição padrão para o tipo de camada correspondente.  
  
## <a name="my-layer-that-uses-spatial-data-from-an-esri-shapefile-always-has-embedded-data"></a>Minha camada que usa dados espaciais de um Arquivo de Forma ESRI sempre tem dados inseridos.  
 Para assegurar que relatórios com mapas possam ser executados em um servidor de relatório, os Arquivos de Forma ESRI devem estar disponíveis como recursos no servidor de relatório. Se você adicionar uma camada a um mapa e especificar um Arquivo de Forma que esteja em seu sistema de arquivos local, os dados espaciais são inseridos automaticamente no relatório.  
  
 Para substituir os dados inseridos por um link para o Arquivo de Forma ESRI, carregue o arquivo ESRI .shp e seu arquivo .dbf correspondente no servidor de relatório e altere a fonte de dados espaciais da camada.  
  
## <a name="i-renamed-a-data-source-or-dataset-to-a-friendly-name-and-now-no-data-appears-in-my-map"></a>Eu renomeei uma fonte de dados ou um conjunto de dados com um nome amigável e agora nenhum dado aparece no meu mapa.  
 A definição de relatório não é atualizada automaticamente quando você altera o nome de qualquer item de relatório manualmente.  
  
 Quando você altera que o nome de um conjunto de dados, qualquer região de dados ou camada do mapa que se refira a esse conjunto de dados deve ser atualizada manualmente. Para reassociar um tablix, gráfico ou medidor a um conjunto de dados, selecione o item na superfície de design, abra as propriedades da região de dados e selecione o nome do conjunto de dados apropriado. Para reassociar uma camada do mapa a um conjunto de dados, selecione a camada, abra as propriedades da camada e selecione o nome do conjunto de dados apropriado.  
  
## <a name="my-spatial-data-contains-nulls-and-empty-strings"></a>Meus dados espaciais contêm cadeias de caracteres nulas e vazias.  
 Nos dados espaciais do item de relatório do mapa, cadeias de caracteres nulas são definidas como zero (0) e cadeias de caracteres vazias são definidas como em branco ("").  
  
 No caso de dados espaciais que vêm de um banco de dados do SQL Server, para alterar esse comportamento, você deve alterar a consulta que retorna os dados espaciais.  
  
## <a name="my-map-exceeds-the-maximum-number-of-spatial-elements"></a>Meu mapa excede o número máximo de elementos espaciais  
 Por padrão, um mapa pode ter 20.000 elementos do mapa ou 1.000.000 de pontos. Se seu mapa exceder esses limites, você poderá usar um dos seguintes métodos:  
  
-   Remover uma camada.  
  
-   Diminuir a resolução do mapa.  
  
-   Diminuir as coordenadas do visor do mapa para exibir uma área menor.  
  
-   Se os dados espaciais vierem de um conjunto de dados de relatório, defina um filtro para limitar os dados do conjunto de dados. O filtro deve ser definido em um campo que não seja do tipo de dados espacial.  
  
-   Se os dados espaciais vierem de um banco de dados do SQL Server, altere a consulta para usar funções espaciais para limitar os dados a uma área menor.  
  
##  <a name="Viewport"></a> Problemas de centralização e exibição do visor  
 Use esta seção para ajudar a resolver problemas relacionados às opções do visor.  
  
## <a name="i-cannot-set-the-center-and-view-on-an-embedded-map-element"></a>Eu não posso centralizar e exibir em um elemento de mapa inserido.  
 Para centralizar um visor em um elemento do mapa específico, você deve ter associado os dados espaciais em uma camada a dados analíticos.  
  
## <a name="i-set-the-map-center-and-view-in-my-report-when-i-reopen-the-report-why-isnt-the-map-view-the-same"></a>Eu defini o centro e a exibição do mapa em meu relatório. Quando reabro o relatório, por que a exibição do mapa não é igual?  
 Se as credenciais de usuário necessárias para a leitura de dados espaciais não estiverem disponíveis para o relatório quando você abri-lo, dados espaciais de espaço reservado serão usados. Dependendo das opções de centralização e zoom definidas para o visor do mapa, a exibição do mapa poderá ser centralizada em uma camada diferente.  
  
 Para recarregar os dados espaciais e usar o centro de exibição do mapa salvo no relatório, clique com o botão direito do mouse no visor do mapa e clique em **Recarregar**. Depois que você inserir as credenciais para a fonte de dados espaciais, a camada carregará os dados espaciais e a exibição do mapa será restaurada.  
  
## <a name="the-center-and-view-for-a-map-layer-option-does-not-work"></a>O centro e a exibição de uma opção de camada do mapa não funcionam.  
 Quando o visor está definido para centralizar nos dados espaciais de uma camada específica, e o centro da exibição não parece ser o centro da camada, provavelmente há pequenas ilhas ou áreas incluídas nos dados espaciais que são muito pequenas para visualização no visor. Por exemplo, os dados espaciais de um país podem incluir ilhas pequenas ou outros territórios pequenos como parte do território. O visor usa todos os dados espaciais para calcular o centro da camada.  
  
 Para substituir os cálculos da camada, faça o seguinte:  
  
-   Especifique um centro personalizado para o visor.  
  
-   Altere o nível de zoom do visor para eliminar os locais que você não deseja incluir.  
  
-   Insira os dados espaciais no relatório e exclua os locais que você não deseja incluir.  
  
##  <a name="Layers"></a> Problemas de camada  
 Use esta seção para ajudar a resolver problemas relacionados às opções de camada.  
  
## <a name="i-do-not-see-one-or-more-layers-in-my-map"></a>Não vejo uma ou mais camadas no meu mapa.  
 A exibição de uma camada do mapa em um relatório dependerá da disponibilidade dos dados espaciais, da relação entre os dados espaciais e os dados analíticos, do tipo de dados espaciais e do tipo de camada correspondente, da visibilidade e das opções de transparência na camada e da ordem de desenho da camada. Se você não vir dados de uma camada, verifique as seguintes opções:  
  
-   **Tipo de camada e tipo de dados espacial.** O tipo de camada exibe somente dados espaciais que correspondem ao tipo de camada. Por exemplo, se o tipo de camada for Ponto, mas os dados espaciais forem Linha, nenhum dado aparecerá.  
  
-   **Valores de campos de correspondência.** Os valores nos campos que você especifica para relacionar dados analíticos e dados espaciais devem identificar cada elemento do mapa exclusivamente. Os campos devem ter o mesmo tipo de dados. Os valores nos campos devem ser idênticos. Para obter mais informações, consulte [Problemas de legenda, escala de cores e escala de distância](#Legend).  
  
-   **Ordem da camada.** A ordem das camadas no painel Mapa é a ordem na qual as camadas são desenhadas no renderizador de relatório. Os dados espaciais nas camadas que são desenhadas primeiro podem ser substituídos pelos dados espaciais para camadas que são desenhadas depois. As camadas que aparecem na parte superior da lista são desenhadas primeiro. Quando altera a ordem das camadas na lista, você está alterando a ordem de desenho das camadas.  
  
-   **Transparência.** Você pode especificar a transparência de cada camada do mapa de modo independente. Os valores padrão de transparência são diferentes de acordo com o modo como você adiciona uma camada. Uma transparência de 0% significa que a camada é opaca e nenhum outro dado da camada será exibido através deste. Para permitir que outros dados apareçam através de uma camada existente, ajuste o valor para um percentual mais alto que apresente o efeito desejado.  
  
-   **Visibilidade.** A visibilidade de uma camada é definida como **Visível**, **Oculta**ou **ZoomBased**, com base no nível de zoom do visor do mapa. Os intervalos máximo e mínimo do nível de zoom também podem ser especificados. A visibilidade pode se basear em uma expressão que seja avaliada para um desses valores.  
  
    > [!TIP]  
    >  Você pode alternar a visibilidade de cada camada no painel Mapa. Quando você estiver criando cada camada, alterne todas as outras camadas para determinar se o problema vem de uma camada individual ou se decorre de problemas de transparência entre camadas.  
  
## <a name="i-set-a-filter-on-the-map-layer-and-it-has-no-effect"></a>Eu defini um filtro na camada do mapa e ele não tem nenhum efeito.  
 Para filtrar os dados de uma camada, o tipo de dados na expressão de filtro deve ser especificado. Verifique se você especificou os o tipo de dados subjacente correto de forma que a equação de filtro seja avaliada corretamente para a condição especificada. Para obter mais informações, consulte [Exemplos de equações de filtro &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-equation-examples-report-builder-and-ssrs.md).  
  
##  <a name="Legend"></a> Problemas de legenda, escala de cores e régua  
 Use esta seção para ajudar a resolver problemas relacionados às opções de regras, legendas e escala de cores.  
  
## <a name="how-do-i-control-the-values-in-the-map-legend"></a>Como eu controlo os valores na legenda do mapa?  
 Os valores da legenda são determinados automaticamente com base nas regras de tipo de elemento do mapa que você especifica para cada camada do mapa e pelas regras de distribuição especificadas para a legenda.  
  
 Por padrão, todos os itens gerados por todas as regras aparecem na primeira legenda. Os valores de todas as regras de polígono, linha e ponto de cada camada contribuem para o intervalo de legenda combinado. Para exibir itens em legendas diferentes, primeiro você deve criar várias legendas e depois, para cada regra, especificar qual legenda exibirá os itens relacionados.  
  
 Para associar uma regra a uma legenda específica, abra as propriedades da regra e, na página Legenda, selecione o nome da legenda a ser usado. Para remover os itens de uma legenda, nas opções de legenda, selecione a linha em branco do nome da legenda. Se renomear os elementos da legenda no relatório, você deverá associar cada camada manualmente ao item de legenda apropriado.  
  
 Para controlar o título e o conteúdo de cada legenda, use as propriedades da Legenda para a regra. Você pode especificar a quantidade de divisões a ser criada, alterar os cálculos que atribuem valores a cada divisão, definir os valores do intervalo mínimo e máximo e alterar o formato do texto da legenda.  
  
 Para obter mais informações, consulte [Alterar legendas de mapa, escala de cores e regras associadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md).  
  
## <a name="the-rules-that-i-set-do-not-give-the-results-that-i-expect"></a>As regras que eu defini não dão os resultados esperados.  
 As regras se aplicam aos dados analíticos associados aos elementos do mapa em uma camada. Use a lista seguinte para ajudar a identificar problemas com todas as regras de cores, regras de tamanho, regras de largura e regras de tipo de marcador:  
  
-   A precedência de aplicação do estilo a cada elemento do mapa (polígono, linha, ponto) é definida da mais baixa para a mais alta: propriedades de camadas; propriedades do elemento do mapa para todos os elementos de mapas na camada; regras que você especifica; e por fim, os valores especificados por você para elementos do mapa inseridos com a opção de substituição selecionada. Quando você seleciona a opção de substituição para um elemento inserido, as regras não se aplicam mais, mesmo que depois você altere os valores novamente para a configuração original.  
  
-   Problemas de campos de correspondência. Os campos de correspondência permitem a associação de dados entre elementos do mapa e dados analíticos. Os dados espaciais e os campos de dados analíticos que correspondem aos campos de correspondência devem ter o mesmo tipo de dados e o mesmo formato. Se o campo de correspondência não corresponder exatamente aos dados espaciais e aos dados analíticos, a regra não terá nenhum efeito. Por exemplo, se o campo de correspondência para dados espaciais tiver espaços em branco adicionais ou pontuação extra em comparação com o campo de correspondência para dados analíticos, nenhuma correspondência ocorrerá.  
  
-   Para obter mais informações, consulte [Variar a exibição de polígono, linha e ponto por regras e dados analíticos &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/vary-polygon-line-and-point-display-by-rules-and-analytical-data.md).  
  
## <a name="what-is-the-value-nan-on-the-color-scale"></a>O que é o valor NaN na escala de cores?  
 **NaN** significa Não é um Número. Os valores de escalas de cores devem ser numéricos. Verifique as configurações de distribuição e o valor de texto da legenda das regras associadas à escala de cores. Se você criou intervalos de distribuição personalizados, verifique se especificou o limite inferior no primeiro intervalo e o limite superior no último intervalo.  
  
## <a name="my-color-scale-does-not-appear-when-i-run-the-report"></a>Minha escala de cores não aparece quando eu executo o relatório.  
 A escala de cores exibe informações ao usuário quando uma camada do mapa especifica regras de cores para polígonos, linhas ou pontos para a camada inteira ou para elementos do mapa inseridos. Se nenhum elemento do mapa especificar uma regra de cor, ou se as regras de cores especificarem com o uso de uma legenda, em vez do mapa de cores, o mapa de cores não aparecerá no relatório renderizado.  
  
 Para exibir a escala de cores, especifique regras de cores para uma camada ou um elemento do mapa inserido. Para obter mais informações, consulte [Alterar legendas de mapa, escala de cores e regras associadas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md).  
  
##  <a name="Tile"></a> Problemas de peça  
 Use esta seção para ajudar a resolver problemas relacionados às opções de plano de fundo lado a lado.  
  
## <a name="i-cannot-see-the-bing-maps-tile-background"></a>Eu não consigo visualizar o plano de fundo de mapas do Bing lado a lado.  
 As configurações seguintes afetam se um plano de fundo de mapas do Bing lado a lado são exibidos na visualização local ou em um relatório executado a partir do servidor de relatório:  
  
-   A camada do mapa lado a lado deve existir. No assistente de Mapa ou no assistente de Camada, selecione **Adicionar um plano de fundo do Bing Maps a esta exibição de mapa**. Isso adicionará uma camada de peças ao centro e nível de zoom da exibição do visor do mapa. Você também pode adicionar uma camada de peças da barra de ferramentas do painel Mapa.  
  
-   O sistema de coordenadas do mapa do visor deve ser **Geográfico**, não **Planar**.  
  
-   A projeção do mapa deve ser **Mercator**.  
  
-   Para a visualização local, você deve ter acesso à Internet. Para um relatório executado a partir do servidor de relatório, o servidor de relatório deve ser configurado para dar suporte ao plano de fundo da peça. Para obter mais informações, consulte "Planejando o suporte ao mapa" na [documentação do Reporting Services](http://go.microsoft.com/fwlink/?linkid=121312) nos Manuais Online do SQL Server.  
  
 Para obter mais informações sobre a adição de uma camada lado a lado, consulte [Adicionar, alterar ou excluir um mapa ou uma camada do mapa &#40;Construtor de Relatórios e SSRSSSRS&#41;](../../reporting-services/report-design/add-change-or-delete-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
## <a name="how-do-i-control-the-text-on-a-tile-layer"></a>Como eu controlo o texto em uma camada de peças?  
 As exibições **Rodoviária** e **Híbrida** incluem texto. O texto faz parte das peças que vêm de Serviços Web Bing Maps.  
  
 Para incluir uma camada de peças sem texto, selecione a exibição **Aérea** .  
  
##  <a name="Tooltip"></a> Problemas de dica de ferramenta e rótulo  
 Use esta seção para ajudar a resolver problemas relacionados às opções de dica de rótulo ou dica de ferramenta.  
  
## <a name="i-get-an-expression-error-about-dataset-scope-when-i-set-a-label-or-tooltip-to-an-expression"></a>Eu recebo um erro de expressão sobre o escopo do conjunto de dados quando defino um rótulo ou Dica de Ferramenta como uma expressão.  
 Quando seus dados espaciais vierem de uma galeria de mapas ou um Arquivo de Forma ESRI, os dados associados não fazem parte de um conjunto de dados de relatório. Você não pode usar a sintaxe de expressão para uma referência de campo do conjunto de dados para especificar esses dados para um rótulo ou dica de ferramenta.  
  
 Para especificar dados relacionados a dados espaciais que não fazem parte de um conjunto de dados de relatório, você deve usar o símbolo #seguido por um rótulo que especifica o nome dos dados.  
  
## <a name="see-also"></a>Consulte também  
 [Mapas de &#40; Construtor de relatórios e SSRS &#41;](../../reporting-services/report-design/maps-report-builder-and-ssrs.md)   
 [Solucionar problemas de construtor de relatórios](http://msdn.microsoft.com/en-us/3806fc48-56f8-44d1-a3c1-df8c33cce0a3)  
  
  
