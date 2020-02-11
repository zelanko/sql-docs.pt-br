---
title: Caixa de diálogo Propriedades do visor do mapa, geral | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.mapviewport.general.f1
- "10505"
ms.assetid: 6c9c773e-5c56-4571-95ed-8a157cfdfe52
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8ec0aaa051ba317cd05a9784c80fb997f5fa19e6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108241"
---
# <a name="map-viewport-properties-dialog-box-general"></a>Caixa de diálogo Propriedades do Visor do Mapa, Geral
  Selecione **Geral** na caixa de diálogo **Propriedades do Visor do Mapa** para alterar o sistema de coordenadas, a projeção e as opções de limite.  
  
## <a name="options"></a>Opções  
 **Sistema de coordenadas**  
 Indique o tipo de sistema de coordenadas usado pelos dados do mapa.  
  
-   **Planar** Escolha esta opção quando os dados do mapa estiverem em coordenadas X e Y, por exemplo, para criar planos.  
  
-   **Geográfico** Escolha esta opção quando os dados do mapa estiverem em coordenadas de longitude e latitude, por exemplo, para locais de cidade.  
  
 **Projeção**  
 Especifique o método a ser usado para coordenadas geográficas de projeto em uma superfície bidimensional. Escolha uma projeção compatível com os dados visualizados. As quatro propriedades espaciais afetadas pela projeção são área, forma, distância e direção. Para exibições da terra, uma boa escolha de projeção depende da exibição central, dos limites de mapa e do fator de zoom.  
  
 Cada uma das seguintes projeções preserva uma ou mais dessas propriedades espaciais:  
  
-   **Cilíndrica equidistante** Escolha esta opção para usar a longitude e a latitude como coordenadas retangulares.  
  
-   **Mercator** Escolha essa projeção popular para áreas menores, para menos distorção em volta do Equador ou quando você quiser adicionar uma camada do mapa com uma camada de bloco existente que usa a projeção Mercator.  
  
-   **Robinson** Escolha essa opção para menos distorção de áreas grandes que se estendem do Equador até o polos. Desenvolvida por Arthur H. Robinson em 1963.  
  
-   **Fahey** Escolha essa opção para menos distorção de áreas grandes que se estendem do Equador até o polos. Desenvolvida por Lawrence Fahey em 1975.  
  
-   **Eckert1** Escolha esta opção para usar paralelos espaçados igualmente em latitude e linhas retas para meridianos em longitude.  
  
-   **Eckert3** Escolha esta opção para usar paralelos espaçados igualmente em linhas de latitude e curvas para meridianos em longitude.  
  
-   **HammerAitoff** Escolha esta opção para mapas polares ou mapas mundiais.  
  
-   **Wagner3** Escolha esta opção para mapas mundiais.  
  
-   **Bonne** Escolha esta opção para exibir o mundo como ele aparece em um Atlas.  
  
 **Opções de quebra de página**  
 Selecione as opções para indicar como o conteúdo se ajusta a uma página de relatório.  
  
 **Opções de limite**  
 Especifique os limites inferiores e superiores das coordenadas para controlar qual parte do mapa aparece no relatório.  
  
 **X Mínimo**  
 Valor de X mais baixo. Disponível somente para **Planar** .  
  
 **X Máximo**  
 Valor de X mais alto. Disponível somente para **Planar** .  
  
 **Y Mínimo**  
 Valor de Y mais baixo. Disponível somente para **Planar** .  
  
 **Y Máximo**  
 Valor de Y mais alto. Disponível somente para **Planar** .  
  
 **Longitude Mínima**  
 Valor de longitude mais baixo. Disponível somente para **Geográfico** .  
  
 **Longitude Máxima**  
 Valor de longitude mais alto. Disponível somente para **Geográfico** .  
  
 **Latitude Mínima**  
 Valor de latitude mais baixo. Disponível somente para **Geográfico** .  
  
 **Latitude Máxima**  
 Valor de latitude mais alto. Disponível somente para **Geográfico** .  
  
## <a name="see-also"></a>Consulte Também  
 [Mapas &#40;Construtor de Relatórios e SSRS&#41;](report-design/maps-report-builder-and-ssrs.md)  
  
  
