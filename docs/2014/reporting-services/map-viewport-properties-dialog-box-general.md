---
title: Mapear a caixa de diálogo de propriedades do visor, geral | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.mapviewport.general.f1
- "10505"
ms.assetid: 6c9c773e-5c56-4571-95ed-8a157cfdfe52
author: maggiesmsft
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 62d20c36271bd6dd1bfa591edf606c3e295d1adb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48138619"
---
# <a name="map-viewport-properties-dialog-box-general"></a>Caixa de diálogo Propriedades do Visor do Mapa, Geral
  Selecione **Geral** na caixa de diálogo **Propriedades do Visor do Mapa** para alterar o sistema de coordenadas, a projeção e as opções de limite.  
  
## <a name="options"></a>Opções  
 **sistema de coordenadas**  
 Indique o tipo de sistema de coordenadas usado pelos dados do mapa.  
  
-   **Planar** Escolha esta opção quando os dados do mapa estiverem em coordenadas X e Y, por exemplo, para criar planos.  
  
-   **Geográfico** Escolha esta opção quando os dados do mapa estiverem em coordenadas de longitude e latitude, por exemplo, para locais de cidade.  
  
 **Projeção**  
 Especifique o método a ser usado para coordenadas geográficas de projeto em uma superfície bidimensional. Escolha uma projeção compatível com os dados visualizados. As quatro propriedades espaciais afetadas pela projeção são área, forma, distância e direção. Para exibições da terra, uma boa escolha de projeção depende da exibição central, dos limites de mapa e do fator de zoom.  
  
 Cada uma das seguintes projeções preserva uma ou mais dessas propriedades espaciais:  
  
-   **Equirretangular** Escolha esta opção para usar longitude e latitude como coordenadas retangulares.  
  
-   **Mercator** Escolha esta projeção popular para áreas pequenas, para obter menos distorção ao redor do equador, ou quando você quiser adicionar uma camada do mapa com uma camada lado a lado existente que use a projeção Mercator.  
  
-   **Robinson** Escolha esta opção para obter menos distorção de áreas grandes que vão do equador até os polos. Desenvolvida por Arthur H. Robinson em 1963.  
  
-   **Fahey** Escolha esta opção para obter menos distorção de áreas grandes que vão do equador até os polos. Desenvolvida por Lawrence Fahey em 1975.  
  
-   **Eckert1** Escolha esta opção para usar paralelos com espaçamento uniforme na latitude e linhas retas para os meridianos na longitude.  
  
-   **Eckert3** Escolha esta opção para usar paralelos com espaçamento uniforme na latitude e linhas curvas para os meridianos na longitude.  
  
-   **HammerAitoff** Escolha esta opção para mapas polares ou mundiais.  
  
-   **Wagner3** Escolha esta opção para mapas mundiais.  
  
-   **Bonne** Escolha esta opção para exibir o mundo da mesma forma que em um atlas.  
  
 **Opções de quebra de página**  
 Selecione as opções para indicar como o conteúdo se ajusta a uma página de relatório.  
  
 **Opções de limite**  
 Especifique os limites inferiores e superiores das coordenadas para controlar qual parte do mapa aparece no relatório.  
  
 **X mínimo**  
 Valor de X mais baixo. Disponível somente para **Planar** .  
  
 **X máximo**  
 Valor de X mais alto. Disponível somente para **Planar** .  
  
 **Y mínimo**  
 Valor de Y mais baixo. Disponível somente para **Planar** .  
  
 **Y máximo**  
 Valor de Y mais alto. Disponível somente para **Planar** .  
  
 **Longitude mínima**  
 Valor de longitude mais baixo. Disponível somente para **Geográfico** .  
  
 **Longitude máxima**  
 Valor de longitude mais alto. Disponível somente para **Geográfico** .  
  
 **Latitude mínima**  
 Valor de latitude mais baixo. Disponível somente para **Geográfico** .  
  
 **Latitude máxima**  
 Valor de latitude mais alto. Disponível somente para **Geográfico** .  
  
## <a name="see-also"></a>Consulte também  
 [Mapas &#40;Construtor de Relatórios e SSRS&#41;](report-design/maps-report-builder-and-ssrs.md)  
  
  
