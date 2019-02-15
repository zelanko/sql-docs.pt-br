---
title: Mapear a caixa de diálogo de regras de cor, geral | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10541"
- sql12.rtp.rptdesigner.shared.mapcolorrulesgeneral.f1
ms.assetid: 14ff5fc1-4cf8-4a45-9d98-47a1bf1c52c4
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 7c21f95a8ace66b502de7128711acc1d840c4147
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2019
ms.locfileid: "56289664"
---
# <a name="map-color-rules-dialog-box-general"></a>Caixa de diálogo Regra de Cor do Mapa, Geral
  Selecione **Geral** na caixa de diálogo **Propriedades de Regras de Cor** para definir as opções de cor dos elementos de mapa nessa camada. Os elementos de mapa incluem polígonos, linhas e pontos. As regras de cor podem ser aplicadas quando você tiver criado uma relação entre os elementos do mapa com base em dados espaciais e dados analíticos de um campo de conjunto de dados ou de um campo de fonte de dados espacial.  
  
 Para exibir todos os elementos de mapa de uma camada especificando um gradiente decorativo com diferentes cores primárias e secundárias, use a página **Preenchimento** da caixa de diálogo Mapear Propriedades do Polígono. As regras de cor têm prioridade sobre as propriedades de vídeo de uma camada. Para obter mais informações, consulte [Personalizar os dados e a exibição de um mapa ou de uma camada do mapa &#40;Construtor de Relatórios e SSRS&#41;](report-design/customize-the-data-and-display-of-a-map-or-map-layer-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opções  
 **Aplicar estilo do modelo**  
 Selecione esta opção para usar a cor com base no tema que foi escolhido no assistente ou foi definido nas propriedades da camada do Polígono, da Linha ou do Ponto. Um tema define as opções padrão da cor, da fonte e das bordas do mapa. Nesta opção, nenhuma regra é aplicada para atribuir cores a cada elemento de mapa.  
  
 **Visualizar dados usando a paleta de cores**  
 Selecione esta opção para visualizar os dados analíticos usando cores de uma paleta de cores específica.  
  
 **Visualizar dados usando intervalos de cores**  
 Selecione esta opção para visualizar os dados analíticos usando um intervalo de cores para cada elemento de mapa. Por exemplo, quando você especificar Vermelho como uma cor inicial, Amarelo como uma cor intermediária e Verde como uma cor final, os valores do intervalo inferior serão Vermelho, os valores do intervalo intermediário serão Amarelo e os valores do intervalo superior serão Verde.  
  
 **Visualizar dados usando cores personalizadas**  
 Selecione esta opção para visualizar os dados analíticos especificando a sua própria lista de cores.  
  
 **Campo de dados**  
 Esta opção aparece quando você seleciona uma das opções **Visualizar dados** .  
  
 Selecione na lista suspensa o campo se dados analíticos a ser usado. Dependendo da fonte de dados espaciais, a lista exibe campos da fonte de dados espaciais e de um conjunto de dados de relatório que tem uma relação entre os dados espaciais e os dados analíticos. Para criar essa relação, defina as opções de dados na página Dados Analíticos da camada do mapa selecionada.  
  
 **Paleta**  
 Digite ou selecione o nome da paleta de cores.  
  
 **Cor inicial**  
 Especifique a cor a ser usada para os dados na extremidade inferior do intervalo de dados.  
  
 **Cor intermediária**  
 Especifique a cor a ser usada para os dados na parte intermediária do intervalo de dados. Selecione **Sem Cor** para remover esse intervalo.  
  
 **Cor final**  
 Especifique a cor a ser usada para os dados na extremidade superior do intervalo de dados.  
  
 **Adicionar**  
 Clique em **Adicionar** para especificar as suas próprias cores para a regra de cor.  
  
## <a name="see-also"></a>Consulte também  
 [Mapas &#40;Construtor de Relatórios e SSRS&#41;](report-design/maps-report-builder-and-ssrs.md)   
 [Alterar legendas de mapa, escala de cores e regras associadas &#40;Construtor de Relatórios e SSRS&#41;](report-design/change-map-legends-color-scale-and-associated-rules-report-builder-and-ssrs.md)  
  
  
