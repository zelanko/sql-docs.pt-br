---
title: Planejar um relatório de mapa (Construtor de Relatórios e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: dc0c27a4-7e31-4a15-a0bc-3a02479d5b02
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 37dfbbec68d525667d415cca852aded4aba8b747
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56288184"
---
# <a name="plan-a-map-report-report-builder-and-ssrs"></a>Planejar um relatório de mapa (Construtor de Relatórios e SSRS)
  Bons relatórios apresentam informações que levam a ações ou ideias. Para apresentar dados analíticos como totais de vendas ou dados demográficos em relação a um plano de fundo geográfico, você pode adicionar um mapa a seu relatório. Um mapa pode conter várias camadas, onde cada uma exibe elementos de mapas que são definidos por um tipo específico de dados espaciais: pontos que representam locais, linhas que representam rotas ou polígonos que representam áreas. Você pode associar seus dados analíticos a elementos de mapas em cada camada.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="MapPurpose"></a> Especificar a finalidade do mapa  
 O bom design de relatório fornece informações que ajudam os usuários a executarem ações para resolver problemas. Para criar uma exibição de mapa útil e fácil de entender, decida quais questões você deseja que o mapa ajude a responder. Por exemplo, em um mapa você pode visualizar os seguintes tipos de dados para identificar oportunidades de mercado:  
  
-   Vendas relativas para cada loja.  
  
-   Vendas categorizadas por demografia de cliente, com base no local do cliente em relação aos locais de loja.  
  
-   Vendas comparativas ou outros dados financeiros por território de vendas.  
  
-   Vendas comparativas para estratégias de desconto diferentes em várias lojas.  
  
 Depois que você identificar o propósito da exibição do mapa, analise os dados de que você precisa. Os dados analíticos vêm de conjuntos de dados de relatório. Os dados de local vêm de fontes de dados espaciais que você deve especificar.  
  
 
  
##  <a name="Data"></a> Especificar os dados espaciais e analíticos  
 Você deve especificar quais dados espaciais e analíticos são necessários.  
  
 Os dados analíticos vêm de um conjunto de dados de relatório, de dados de exemplo incluídos com um mapa da galeria de mapas ou de dados analíticos incluídos com dados espaciais em um arquivo de forma ESRI.  
  
 Os dados espaciais vêm em três formas: pontos, linhas e polígonos.  
  
-   **Pontos.** Os pontos especificam locais, por exemplo, uma cidade ou um endereço de uma loja, restaurante ou centro de convenções. Para todos locais que você deseja exibir em um mapa, forneça os dados espaciais deles. Depois que você adicionar pontos a um mapa, poderá exibir um marcador no local de ponto e variar o tipo de marcador, o tamanho e a cor.  
  
-   **Linhas.** As linhas especificam caminhos ou rotas, por exemplo, rotas de entrega ou trajetos de voo. Depois que você adicionar uma linha a um mapa, poderá variar a cor e a largura da linha.  
  
-   **Polígonos.** Os polígonos especificam áreas, por exemplo, regiões, territórios, países, estados, províncias, municípios, cidades ou áreas abrangidas por cidades, códigos postais, estações telefônicas ou distritos de censo. Depois que você adicionar polígonos a um mapa, além de exibir o contorno, poderá exibir um marcador no ponto central da área do polígono.  
  
 Depois que você identificar de quais dados espaciais precisa, localize uma fonte para eles.  
  
### <a name="find-a-source-for-spatial-data"></a>Localizar uma fonte para dados espaciais  
 Para localizar dados espaciais a serem usados em seu mapa, utilize as seguintes fontes:  
  
-   Arquivos de forma ESRI, inclusive os arquivos de forma publicamente disponíveis que podem ser pesquisados na Internet.  
  
-   Dados espaciais de fontes de dados espaciais do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Mapas de relatórios na Galeria de Mapas.  
  
-   Sites de terceiros que oferecem dados espaciais como shapefiles ESRI ou dados espaciais do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Peças de mapa do Bing que fornecem um plano de fundo para a exibição do mapa. Para exibir peças em um mapa, o servidor de relatório deve ser configurado para dar suporte aos Serviços Web Bing Maps.  
  
 Para obter mais informações, consulte "Onde posso obter arquivos de forma ESRI?" em [Assistente de Mapa e Assistente de Camada do Mapa &#40;Construtor de Relatórios e SSRS&#41;](map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md).  
  
 Os dados espaciais podem ser politicamente confidenciais e possivelmente protegidos por leis de direitos autorais. Verifique os termos de uso e as políticas de privacidade de fontes de dados espaciais para entender como você pode usar dados espaciais em seu relatório.  
  
 Depois que você localizar os dados desejados, poderá inserir os dados na definição de relatório ou recuperar os dados dinamicamente quando o relatório for processado. Para obter mais informações, consulte [Equilibrar o tamanho da definição de relatório e o tempo de processamento do relatório](#Embedding) posteriormente neste tópico.  
  
### <a name="determine-the-spatial-data-and-the-spatial-data-match-fields"></a>Determinar os dados espaciais e os campos de correspondência de dados espaciais  
 Para exibir dados analíticos em um mapa e variar o tamanho, a cor ou o tipo de marcador, você deve especificar campos que relacionam os dados espaciais e os dados analíticos.  
  
 Os dados espaciais devem conter os seguintes campos:  
  
-   **Spatial data.** Um campo de dados espaciais que tem os conjuntos de coordenadas que definem cada ponto, linha ou polígono.  
  
-   **Campos de correspondência.** Um ou mais campos que identificam exclusivamente cada campo de dados espacial. Por exemplo, para um ponto de local de loja, você pode usar o nome da loja. Se o nome da loja não for exclusivo nos dados espaciais, você poderá incluir o nome da cidade e a loja.  
  
 Os campos de correspondência são usados para relacionar os dados espaciais aos dados analíticos.  
  
### <a name="determine-the-analytical-data-and-the-analytical-data-match-fields"></a>Determinar os dados analíticos e os campos de correspondência de dados analíticos  
 Depois que você identificar os dados espaciais, identifique os dados analíticos. Os dados analíticos podem vir de uma das seguintes fontes:  
  
-   Um conjunto de dados de relatório existente. Os campos são especificados como expressões de campo simples, por exemplo, [Sales] ou =Fields!Sales.Value.  
  
-   Campos de dados fornecidos pela fonte de dados espacial. Os campos são especificados como palavras-chave que começam com # seguido pelo nome do campo da fonte de dados espaciais.  
  
 Você deve determinar os nomes dos campos de correspondência:  
  
-   Campos de correspondência. Um ou mais campos que especificam as mesmas informações dos campos de correspondência de dados espaciais para criar uma relação entre os dados espaciais e os dados analíticos. Os campos de correspondência devem corresponder ao tipo de dados e à formatação.  
  
 Depois que você identificar a fonte de dados espaciais, os dados espaciais, a fonte de dados analíticos, os dados analíticos e os campos de correspondência, estará pronto para decidir qual tipo de mapa deseja adicionar a um relatório.  
  

  
##  <a name="MapType"></a> Escolher um tipo de mapa  
 Quando você executa o assistente de Mapa, adiciona um mapa e a primeira camada do mapa ao relatório. O assistente o permite a você adicionar um dos seguintes tipos de mapas ao relatório:  
  
-   Um mapa básico que exibe locais sem dados analíticos associados.  
  
-   Um mapa que tem um valor analítico associado a cada elemento do mapa, por exemplo, total de vendas de cada local de loja.  
  
-   Um mapa que tem mais de um valor analítico associado a um elemento do mapa, por exemplo, número de clientes e total de vendas de cada local de loja.  
  
 A tabela a seguir descreve cada tipo de mapa. Todos os tipos de mapa permitem a você selecionar um tema que controle a paleta, o estilo da borda e a fonte para exibir rótulos.  
  
|Ícone de assistente|Estilo de camada|Tipo de camada|Descrição e opções|  
|-----------------|-----------------|----------------|-----------------------------|  
|![rs_MapType_Polygon_Basic](../media/rs-maptype-polygon-basic.gif "rs_MapType_Polygon_Basic")|Mapa Básico|Polygon|Um mapa que exibe apenas áreas, por exemplo, territórios de vendas.<br /><br /> Opções: varie a cor pela paleta ou use uma única cor. Uma paleta é um conjunto predefinido de cores. Quando todas as cores em uma paleta tiverem sido atribuídas, tons de cores serão atribuídos.|  
|![rs_MapType_Polygon_ColorAnalytical](../media/rs-maptype-polygon-coloranalytical.gif "rs_MapType_Polygon_ColorAnalytical")|Mapa Analítico de Cores|Polygon|Um mapa que exibe dados analíticos por cor variável, por exemplo, dados de vendas por área.|  
|![rs_MapType_Polygon_Bubble](../media/rs-maptype-polygon-bubble.gif "rs_MapType_Polygon_Bubble")|Mapa de Bolha|Polygon|Um mapa que exibe dados analíticos por tamanho de bolha variável centralizado nas áreas, por exemplo, dados de vendas por área.<br /><br /> Opções: Opções: varie as cores da área com base em um segundo campo analítico e especifique regras de cores.|  
|![rs_MapType_Line_Basic](../media/rs-maptype-line-basic.gif "rs_MapType_Line_Basic")|Mapa de Linha Básico|Linha|Um mapa que exibe apenas linhas, por exemplo, rotas de entrega.<br /><br /> Opções: varie a cor pela paleta ou use uma única cor.|  
|![rs_MapType_Line_Analytical](../media/rs-maptype-line-analytical.gif "rs_MapType_Line_Analytical")|Mapa de Linha Analítico|Linha|Um mapa que varia a cor e a largura da linha, por exemplo, número de pacotes entregues e métrica pontual por rota.<br /><br /> Opções: varie a largura da linha por um campo analítico, varie a cor da linha por um segundo campo analítico e especifique regras de cores.|  
|![rs_MapType_Marker_Basic](../media/rs-maptype-marker-basic.gif "rs_MapType_Marker_Basic")|Mapa de Marcador Básico|Ponto|Um mapa que exibe um marcador em cada local, por exemplo, cidades.<br /><br /> Opções: varie a cor pela paleta ou use uma única cor e altere o estilo do marcador.|  
|![rs_MapType_Marker_Bubble](../media/rs-maptype-marker-bubble.gif "rs_MapType_Marker_Bubble")|Mapa de Marcador de Bolha|Ponto|Um mapa que exibe uma bolha para cada local e varia o tamanho da bolha por um campo de dados analítico, por exemplo, dados de vendas por cidade.<br /><br /> Opções: varie a cor da bolha por um segundo campo analítico e especifique regras de cores.|  
|![rs_MapType_Marker_Analytical](../media/rs-maptype-marker-analytical.gif "rs_MapType_Marker_Analytical")|Mapa de Marcador Analítico|Ponto|Um mapa que exibe um marcador em cada local e varia a cor do marcador, o tamanho e o tipo com base nos dados analíticos, por exemplo, produtos mais vendidos, faixa de lucro e estratégia de desconto.<br /><br /> Opções: varie o tipo de marcador por um campo analítico, varie o tamanho do marcador por um segundo campo analítico, varie a cor do marcador por um terceiro campo analítico e especifique as regras de cores.|  
  
 Depois que você adicionar um mapa com o assistente de Mapa, poderá criar camadas adicionais ou alterar as opções para uma camada usando o assistente de Camada. Para obter mais informações sobre os assistentes, consulte [Assistente de Mapa e Assistente de Camada do Mapa &#40;Construtor de Relatórios e SSRS&#41;](map-wizard-and-map-layer-wizard-report-builder-and-ssrs.md).  
  
 Você pode personalizar a exibição ou as opções de dados para cada camada independentemente. Para obter mais informações sobre como personalizar um mapa após executar um assistente, consulte [Personalizar os dados e a exibição de um mapa ou de uma camada do mapa &#40;Construtor de Relatórios e SSRS&#41;](customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
 
  
##  <a name="Legend"></a> Planejar as legendas  
 Para ajudar os usuários a interpretarem um mapa, você pode adicionar várias legendas de mapas, uma escala de cores e uma escala de distância. Quando você criar um mapa, planeje o local em que deseja exibir as legendas. Você pode especificar as seguintes informações sobre cada legenda:  
  
-   **Local da legenda.** Por exemplo, as legendas podem ser exibidas dentro ou fora do visor, e em 12 locais discretos relativo ao visor.  
  
-   **Estilos de legenda**. Por exemplo, você pode especificar o estilo da fonte, o estilo da borda, a linha separadora e as propriedades de preenchimento.  
  
-   **Título da legenda.** Por exemplo, você pode especificar o texto do título e controlar independentemente se o título de uma legenda de mapa ou a escala de cores deve ser exibido.  
  
-   **Layout de legenda do mapa.** Por exemplo, as legendas de mapa podem ser exibidas como tabelas altas ou tabelas largas.  
  
 O conteúdo da legenda é criado automaticamente durante o processamento de relatório com base em opções de regra que você define para cada camada.  
  
 Por padrão, todas as camadas exibem os resultados de regras na primeira legenda do mapa. Você pode criar várias legendas e, para cada regra, atribuir qual legenda deve ser usada para exibir os resultados.  
  
 Para obter mais informações, consulte [Variar a exibição de polígono, linha e ponto por regras e dados analíticos &#40;Construtor de Relatórios e SSRS&#41;](vary-polygon-line-and-point-display-by-rules-and-analytical-data.md) e [Alterar legendas de mapa, escala de cores e regras associadas &#40;Construtor de Relatórios e SSRS&#41;](change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md).  
  

  
##  <a name="Embedding"></a> Equilibrar o tamanho da definição de relatório e o tempo de processamento do relatório  
 O bom design de relatório para mapas requer que você equilibre as opções que controlam o desempenho do relatório e o tamanho da definição do relatório. Os elementos do mapa que se baseiam nos dados espaciais ou em peças de mapas do Bing podem ser estáticos e inseridos na definição de relatório ou dinâmicos e criados toda vez que o relatório é processado. Você deve avaliar as desvantagens de dados de mapa estáticos ou dinâmicos e encontrar o equilíbrio que funciona para suas circunstâncias. Considere as seguintes informações para tomar esta decisão:  
  
-   Elementos de mapa inseridos podem aumentar significativamente o tamanho da definição do relatório, mas reduzem o tempo necessário para exibir o mapa no relatório. Seu servidor de relatório pode ter limites de tamanho com os quais você precisa trabalhar.  
  
-   A definição de relatório especifica limites para o número de pontos de dados espaciais que podem ser processados e um valor separado que especifica o número de elementos do mapa que podem ser incluídos na definição de relatório.  
  
-   Elementos de mapa dinâmico reduzem o tamanho da definição do relatório, mas aumentam o tempo necessário para processar e renderizar o mapa.  
  
-   Quando a fonte de dados espaciais está localizada no seu computador, os elementos do mapa sempre são inseridos na definição de relatório. Isso inclui dados espaciais da Galeria de Mapas ou arquivos de formas ESRI que foram instalados localmente.  
  
 Para usar dados espaciais dinâmicos, a fonte de dados espaciais deve estar no servidor de relatório. Quando os relatórios são criados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], as fontes de dados espaciais podem ser adicionadas a um projeto e publicadas no servidor de relatório junto com a definição de relatório. Se você estiver usando o Construtor de Relatórios para criar relatórios, deverá carregar os dados espaciais no servidor de relatório primeiro e, depois, no assistente ou nas propriedades da camada, especificar essa fonte de dados espaciais para a camada do mapa.  
  

  
## <a name="see-also"></a>Consulte também  
 [Personalizar os dados e a exibição de um mapa ou de uma camada do mapa &#40;Construtor de Relatórios e SSRS&#41;](customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md)   
 [Tutorial: Relatório de mapa &#40;construtor de relatórios&#41;](../tutorial-map-report-report-builder.md)   
 [Mapas &#40;Construtor de Relatórios e SSRS&#41;](maps-report-builder-and-ssrs.md)   
 [Solucionar problemas de relatórios: Mapear relatórios &#40;relatórios e SSRS&#41;](troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
  
  
