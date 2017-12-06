---
title: "Adicionar navegadores a relatórios móveis do Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e141f50e-49a9-46c6-983c-f656013aa07c
caps.latest.revision: "12"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: d483e2dcafeb45beb00e32cfed7cf04ab41ca689
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="add-navigators-to-reporting-services-mobile-reports"></a>Add navigators to Reporting Services mobile reports
Em [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)], adicione os *navegadores* para filtrar os dados nas visualizações por hora ou por seleção. 

Navegadores são semelhantes às segmentações no Power BI e Tabelas Dinâmicas do Excel, mas os navegadores também têm algumas características exclusivas.

Os**navegadores baseados em tempo** filtram tabelas selecionando linhas que se enquadram no intervalo de tempo específico. 

Os**navegadores baseados em seleção** filtram tabelas selecionando linhas em que um valor de coluna específico corresponde ao valor de chave desejado; ou, em casos de árvores hierárquicas, em que um valor de coluna específico pertence à subárvore do valor de chave selecionado. Há dois tipos de navegadores de seleção:
* Listas de seleção são tabelas de coluna única que você pode usar para filtrar o relatório móvel, semelhante à segmentações no Power BI e Excel.
* Grades de scorecard filtram o relatório móvel e também podem conter 
  
## <a name="time-navigators"></a>Navegadores de tempo   
  
Como o nome sugere, o filtro de navegador por tempo para filtrar um intervalo de dados limitado por um intervalo de tempo.   
  
![SSMRP_TimeNav](../../reporting-services/mobile-reports/media/ssmrp-timenav.png)  
*Os gráficos de quatro linhas à esquerda são definidos nas Predefinições de Intervalo de Tempo. O gráfico de linha à direita é o filtro.*  
  
Ao exibir o relatório na Visualização ou no portal da Web do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , arraste as setas no navegador de tempo para filtrar o restante do relatório.  
  
![SSMRP_TimeNavPreview](../../reporting-services/mobile-reports/media/ssmrp-timenavpreview.png)  
  
Por padrão, o navegador de tempo filtra todos os elementos visuais no relatório que estão conectados a dados baseado em tempo. Se uma tabela contiver mais de uma coluna baseada em tempo, somente a primeira será usada para filtragem. A tabela de série orienta a visualização inserida e determina o intervalo de datas geral do relatório móvel.  
  
Você pode desconectar uma visualização do navegador de tempo.   
1. Selecione a visualização e a guia **Dados** .  
2. Em **Propriedades de Dados**, selecione **Opções**.  
3. Desmarque a caixa de seleção **Filtrado por** .  
  
   ![SSMRP_ClearTimeFilter](../../reporting-services/mobile-reports/media/ssmrp-cleartimefilter.png)  
  
## <a name="selection-lists"></a>Listas de seleção   
  
A lista de seleção filtra os dados em um relatório móvel correspondendo o valor selecionado na lista ao valor de uma coluna especificada de cada linha de uma tabela filtrada. 

1. Na guia **Layout** , arraste **Lista de seleção** para a superfície de design e redimensione-a como desejar.

2. Selecione a guia **Dados** e, no painel **Propriedades de dados** em **Chaves**, selecione a tabela e a coluna que será o filtro. 

3. Em **Rótulos**, selecione a coluna com o rótulo que será exibido. A coluna de chave e a coluna de rótulo podem ser as mesmas.  
  
   No caso de dados de árvore hierárquica, selecione uma coluna de chave pai.  
  
4. Depois de definir as propriedades de dados em **Tabelas Filtradas pela Lista de Seleção**, selecione as tabelas a serem filtrados e a coluna de filtragem. Essa coluna precisa corresponder os valores da coluna de chave da lista de seleção. 

Para cada visualização no relatório móvel que você deseja que a lista de seleção filtre:

1. Selecione a visualização, selecione a guia **Dados** e, no painel **Propriedades de dados** , selecione **Opções** ao lado do nome do campo.

   ![mobile-report-set-selection-list](../../reporting-services/mobile-reports/media/mobile-report-set-selection-list.png)

2. Em **Filtrado por**, escolha a lista de seleção.

Quando você exibe o relatório móvel na Visualização ou no portal da Web do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] e selecione um valor na lista de seleção, ele filtra as outras visualizações no relatório móvel.

![mobile-report-selection-list-filtering](../../reporting-services/mobile-reports/media/mobile-report-selection-list-filtering.png) 
     
## <a name="scorecard-grid"></a>Grade de scorecard  
  
As funções de filtro da grade de scorecard, assim como o filtro da lista de seleção, mas ele também exibe as colunas de valor e indicadores de pontuação, que são os mesmos que os indicadores em uma grade de dados do indicador. Depois de selecionar a chave, o rótulo e as colunas de chave pai opcionais, você deve selecionar uma coluna e tabela de entrada para fornecer dados ao scorecard. A coluna de dados de scorecard deve ser filtrada pela coluna de chave.  

1. Na guia **Layout** , arraste a **Guia de scorecard** para a superfície de design e redimensione-a como desejar.

2. Selecione a guia **Dados** e, no painel **Propriedades de dados** em **Chaves**, selecione a tabela e a coluna que será o filtro. 

3. Em **Rótulos**, selecione a coluna com o rótulo que será exibido. A coluna de chave e a coluna de rótulo podem ser as mesmas.  
  
4. Para adicionar um indicador de pontuação, no painel **Colunas de Dados** , selecione **Adicionar pontuação**.   
  
5. Nomeie o indicador de pontuação e selecione **Opções** para definir as mesmas propriedades que seriam definidas em um indicador em uma grade de dados:  
  
   * Tipo de medidor
   * Campo Valor
   * Campo de comparação
   * Direção de valor
  
6. Para adicionar um indicador de valor, no painel **Colunas de Dados** , selecione **Adicionar valor**.

7. Nomeie o indicador de valor conforme desejado, escolha sua coluna de origem na tabela e selecione como ele será formatado.  

   ![mobile-report-scorecard-grid-data-properties](../../reporting-services/mobile-reports/media/mobile-report-scorecard-grid-data-properties.png)

8. Depois de definir as propriedades de dados em **Tabelas Filtradas pela Lista de Seleção**, selecione as tabelas a serem filtrados e a coluna de filtragem. Essa coluna precisa corresponder os valores da coluna de chave da lista de seleção. 

Quando você exibe o relatório móvel na Visualização ou no portal da Web do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] e selecione um valor na grade de scorecard, ele filtra as outras visualizações no relatório móvel.

![mobile-report-scorecard-grid](../../reporting-services/mobile-reports/media/mobile-report-scorecard-grid.png)
    
## <a name="set-which-visualizations-are-filtered"></a>Definir quais visualizações são filtradas  
  
Os elementos da galeria são configurados para usar filtros clicando no botão de opções de uma entrada específica na exibição de dados. Os filtros são habilitados alternando a caixa de seleção apropriada.  

Você pode decidir quais visualizações no relatório móvel um navegador filtrará:

1. Selecione a visualização, selecione a guia **Dados** e, no painel **Propriedades de dados** , selecione **Opções** ao lado do nome do campo.

   ![mobile-report-set-selection-list](../../reporting-services/mobile-reports/media/mobile-report-set-selection-list.png)

2. Em **Filtrado por**, escolha o navegador. Cada visualização pode ser filtrada por vários navegadores.
  
## <a name="cascading-filters"></a>Filtros em cascata   
  
Os filtros também podem ser colocados em cascata para que o valor selecionado em um filtre os valores disponíveis em outro. Para colocar os filtros em cascata, aplique os filtros à coluna de chave, como faria em um elemento comum da galeria.  

### <a name="see-also"></a>Consulte também 
  
* [Mapas nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Visualizações nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Medidores nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)
* [Grades de dados nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md)  
