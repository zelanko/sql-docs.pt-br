---
title: Mapas em relatórios móveis do Reporting Services | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 50658295-a71c-441e-8eba-e1ef066629c0
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 5b09c8aec100d877256f0d8d9b4b97530ecdf5c6
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "62683744"
---
# <a name="maps-in-reporting-services-mobile-reports"></a>Mapas nos relatórios móveis do Reporting Services
Os mapas são uma ótima maneira de visualizar dados geográficos. [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)] fornece três tipos diferentes de visualização do mapa e mapas internos para continentes e uma série de países individuais. Você também pode [carregar e usar mapas personalizados](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md).   
  
## <a name="types-of-maps"></a>Tipos de mapas  
  
Os relatórios móveis do SQL Server oferecem três tipos diferentes de mapas, os quais são úteis para diferentes circunstâncias.  
  
![SSMRP_MapsGallery](../../reporting-services/mobile-reports/media/ssmrp-mapsgallery.png)  
  
**Mapas de Calor Gradientes** O campo na propriedade Valores é exibido como tons de uma única cor preenchendo cada região de um mapa. Você pode definir se os maiores ou menores valores serão mais escuros na caixa **Direção de Valor** .  
  
**Mapa de Bolhas** A propriedade Valores determina o raio de visualização de uma bolha em exibição sobre a região associada. Você pode definir se todas as bolhas terão cores iguais ou diferentes.   
  
**Mapas de Calor de Parada de Intervalo** mostram um valor em relação a um destino. A propriedade **Destinos** determina o delta entre um campo Comparação e o campo Valores. O delta resultante determina a cor que preenche a região associada do mapa, de verde a amarelo a vermelho. Você pode definir se os maiores ou menores valores serão verdes na caixa **Direção de Valor** .  
  
## <a name="select-the-map-type-and-region"></a>Selecione o tipo de mapa e região  
  
1. Na guia **Layout** , selecione um tipo de mapa, arraste-o para a superfície de design e ajuste-o para o tamanho desejado.  
  
2. Na exibição **Layout** > painel **Propriedades Visuais** > **Mapa**, escolha a região específica do mapa que você precisa.  
  
   ![SSMRP_SelectMap](../../reporting-services/mobile-reports/media/ssmrp-selectmaps.png)  
  
3. Para mapas de calor de parada de intervalo e radiante, defina se os valores maiores ou menores são melhores na caixa **Direção de Valor** em **Propriedades Visuais**.  
  
7. Para mapas de bolhas, em **Propriedades Visuais** defina **Usar Cores Diferentes** como **Ativado** ou **Desativado** para que as bolhas fiquem todas da mesma cor ou todas de cores diferentes.  
  
## <a name="select-the-map-data"></a>Selecione os dados do mapa  
Quando você adiciona pela primeira vez um mapa ao relatório, [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] preenche-o com dados de geografia simulada.  
  
![SSMRP_MapsData](../../reporting-services/mobile-reports/media/ssmrp-mapsdata.png)  
  
Para exibir os dados reais no seu mapa, você precisa definir valores para pelo menos duas das propriedades de dados do mapa:   
* A propriedade **Chaves** conecta os dados a regiões específicas do mapa – estados nos EUA, por exemplo, ou países na África.  
* A propriedade **Valores** é um campo numérico na mesma tabela que o campo de chaves selecionadas. Esses valores são representados de maneira diferente em mapas diferentes. O **mapa de gradiente** usa esses valores para colorir cada região com tons diferentes com base no intervalo de valores. O **mapa de bolhas** baseia o tamanho de uma visualização de bolha em cada região na propriedade de valor.   
* Para mapas de calor de parada de intervalo, você também precisa definir a propriedade **Destinos** .  
  
### <a name="set-map-data-properties"></a>Defina as propriedades de dados do mapa  
  
1. Selecione a guia **Dados** no canto superior esquerdo.  
  
2. Selecione **Adicionar Dados**e, em seguida, **Excel Local** ou **Servidor SSRS**.  
  
   > **Dica**: verifique se os [dados estão em um formato que funciona para relatórios móveis](../../reporting-services/mobile-reports/prepare-data-for-reporting-services-mobile-reports.md).  
  
3. Selecione as planilhas que você deseja e selecione **Importar**.  
   Você verá seus dados em [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)].  
  
4. Nessa exibição de **Dados** > painel **Propriedades de Dados** > em **Chaves**, na caixa à esquerda, escolha a tabela que contém os dados do mapa e, na caixa da direita, escolha o campo-chave que corresponde às regiões do seu mapa.  
  
5. Em **Valores**, a mesma tabela já está na caixa à esquerda. Selecione o campo numérico cujos valores você deseja exibir no mapa.   
  
6. Se esse for um mapa de calor de parada de intervalo, na caixa **Destinos** a mesma tabela estará na caixa à esquerda. Na caixa à direita, selecione o campo numérico cujos valores você deseja que sejam o destino.   
  
   ![SSMRP_MapRangeHeatData](../../reporting-services/mobile-reports/media/ssmrp-maprangeheatdata.png)  
  
7. Selecione **Visualização** no canto superior esquerdo.  
  
   ![SSMRP_MapRangeHeatPreview](../../reporting-services/mobile-reports/media/ssmrp-maprangeheatpreview.png)  
     
8. Selecione o ícone **Salvar** no canto superior esquerdo e **Salvar Localmente** em seu computador ou **Salvar no Servidor**.  
  
### <a name="see-also"></a>Confira também  
-  [Custom maps in Reporting Services mobile reports](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md)  
- [Criar e publicar relatórios móveis com o Publicador de Relatórios Móveis do SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
  
  
