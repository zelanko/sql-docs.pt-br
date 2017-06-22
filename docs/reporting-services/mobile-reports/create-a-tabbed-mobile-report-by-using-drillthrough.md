---
title: "Criar um relatório móvel com guias usando o detalhamento | Relatórios do Reporting Services móveis | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c4d5d80d-370a-4a6d-8b76-698bd5ba5ba6
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6554f808c19540d2a3b7cbe3fdf4e86c5fe7a357
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="create-a-tabbed-mobile-report-by-using-drillthrough"></a>Criar um relatório móvel com guias usando o detalhamento
Saiba como criar um relatório móvel do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] com aparência e funcionamento de um relatório com guias usando detalhamento e parâmetros.

Por exemplo, neste relatório, os indicadores na parte superior funcionam como guias. Quando você clica no medidor Transporte, os dados no restante do gráfico são filtrados para exibir os dados de transporte.

![06-Mobile-Report-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/tabbed-mobile-report-web-viewer-transportation-complete.png)

Nos bastidores, isso é realmente um conjunto de cinco relatórios separados, cada um com um parâmetro diferente que filtra o relatório para corresponder ao medidor selecionado na parte superior do relatório. Criar todos os cinco relatórios pela primeira vez, e para cada um dos cinco relatórios, fazer os outros quatro medidores em drillthroughs quatro relatórios.

Aqui estão as etapas para este exemplo.

## <a name="create-the-basic-report"></a>Criar o relatório básico

1. Crie um relatório chamado Vendas com cinco medidores:

    * Sales
    * Transporte
    * Combustível
    * Armazenamento
    * Despesas diversas

   ![01-vendas---publicador de relatórios móveis](../../reporting-services/mobile-reports/media/01-sales-mobile-report-publisher.png)
    
2. Definir **acentos** para **em** para o indicador de vendas, portanto ele irá comparar com o restante do relatório – nesse caso, branco em preto.

    ![01a-Sales-Accent-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/01a-sales-accent-mobile-report-publisher.png)
    
3. Salvá-lo para um [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] servidor de relatório.

## <a name="make-copies-of-the-report"></a>Fazer cópias do relatório

1. Fazer quatro cópias do relatório de vendas e nomeá-los: 

    * Transporte
    * Combustível
    * Armazenamento
    * Despesas diversas

3. Salvá-los para o [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] servidor de relatório.

## <a name="set-the-gauge-as-a-drillthrough"></a>Definir o medidor como um detalhamento

Nesta seção, você pode definir cada medidor (que não seja o medidor de vendas) como um detalhamento para seu respectivo relatório.

1. No relatório de vendas, selecione o indicador de transporte.

    ![02-Sales-Create-DrillThrough-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/02-sales-create-drillthrough-mobile-report-publisher.png)

2. Com o **Layout** guia selecionada, o **propriedades visuais** painel, selecione **destino do detalhamento**.

3. Selecione **relatório móvel**.

4. Navegue até e selecione o relatório que será o destino para o detalhamento – nesse caso, "Finanças - transporte".

    ![03-Sales-Select-Dashboard-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/03-sales-select-dashboard-mobile-report-publisher.png)

5. Em **Configurar relatório de destino**, selecione o parâmetro para filtrar o relatório e selecione **aplicar**.

   ![04-Sales-Apply-Parameters-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/04-sales-apply-parameters-mobile-report-publisher.png)
   
6. Repita essas etapas para cada um dos outros medidores no relatório de vendas. 

## <a name="set-the-gauges-for-the-other-reports"></a>Definir os medidores em outros relatórios

1.  Abra o relatório de transporte, defina o indicador de vendas como um detalhamento para o relatório de vendas e os outros três medidores como drillthroughs a seus respectivos relatórios.

2. Ainda no relatório de transporte, defina **acentos** para o medidor de transporte **em**, compare com o restante do relatório.

3. Repita essas etapas para os relatórios de combustível, armazenamento e despesas diversas. 

## <a name="view-the-report-in-the-web-portal"></a>Exibir o relatório no portal da web

1. Vá para o [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] servidor de relatório e abra um dos relatórios. 

2. Observe que cada um dos medidores tem um ícone de detalhamento no canto superior direito.

    ![Web-Viewer-drillthrough-icon-mobile-report-builder](../../reporting-services/mobile-reports/media/web-viewer-drillthrough-icon-mobile-report-builder.png)

3. Selecione um dos indicadores para ir para o relatório filtrado para dados do medidor que.

   ![06-Mobile-Report-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/06-mobile-report-web-viewer-transportation.png)

### <a name="see-also"></a>Consulte também
    
* [Adicionar parâmetros a um relatório móvel](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)
* [Adicionar o detalhamento de um relatório móvel para outros relatórios móveis ou URLs](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)




  


