---
title: "Criar um relatório móvel com guias usando o detalhamento | Relatórios móveis do Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c4d5d80d-370a-4a6d-8b76-698bd5ba5ba6
caps.latest.revision: "9"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 9824bbc98ac886f8836b73ae8ca49cbdce93afaa
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/09/2018
---
# <a name="create-a-tabbed-mobile-report-by-using-drillthrough"></a>Criar um relatório móvel com guias usando o detalhamento
Saiba como criar um relatório móvel do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] com aparência e funcionamento de um relatório com guias usando detalhamento e parâmetros.

Por exemplo, neste relatório, os indicadores na parte superior funcionam como guias. Quando você clica no medidor Transporte, os dados no restante do gráfico são filtrados para exibir os dados de transporte.

![06-Mobile-Report-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/tabbed-mobile-report-web-viewer-transportation-complete.png)

Nos bastidores, isso é realmente um conjunto de cinco relatórios separados, cada um com um parâmetro diferente que filtra o relatório para corresponder ao medidor selecionado na parte superior do relatório. Você cria todos os cinco relatórios primeiro e, para cada um dos cinco relatórios, você transforma os outros quatro medidores em detalhamentos para os outros quatro relatórios.

Veja abaixo as etapas para este exemplo.

## <a name="create-the-basic-report"></a>Criar o relatório básico

1. Crie um relatório chamado Vendas com cinco medidores:

    * Sales
    * Transporte
    * Combustível
    * Armazenamento
    * Despesas diversas

   ![01-Sales-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/01-sales-mobile-report-publisher.png)
    
2. Defina **Ênfase** como **Ativado** para o medidor Vendas, de modo que ele seja destacado em relação ao restante do relatório – nesse caso, branco no preto.

    ![01a-Sales-Accent-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/01a-sales-accent-mobile-report-publisher.png)
    
3. Salve-o em um servidor de relatório do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)].

## <a name="make-copies-of-the-report"></a>Fazer cópias do relatório

1. Faça quatro cópias do relatório Vendas e nomeie-as: 

    * Transporte
    * Combustível
    * Armazenamento
    * Despesas diversas

3. Salve-as no servidor de relatório do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)].

## <a name="set-the-gauge-as-a-drillthrough"></a>Definir o medidor como um detalhamento

Nesta seção, você define cada medidor (que não seja o medidor de Vendas) como um detalhamento de seu respectivo relatório.

1. No relatório Vendas, selecione o medidor Transporte.

    ![02-Sales-Create-DrillThrough-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/02-sales-create-drillthrough-mobile-report-publisher.png)

2. Com a guia **Layout** selecionada, no painel **Propriedades visuais**, selecione **Destino de detalhamento**.

3. Selecione **Relatório móvel**.

4. Navegue para o relatório que será o destino do detalhamento e selecione-o – nesse caso, “Finanças – Transporte”.

    ![03-Sales-Select-Dashboard-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/03-sales-select-dashboard-mobile-report-publisher.png)

5. Em **Configurar relatório de destino**, selecione o parâmetro para filtrar o relatório e selecione **Aplicar**.

   ![04-Sales-Apply-Parameters-Mobile-Report-Publisher](../../reporting-services/mobile-reports/media/04-sales-apply-parameters-mobile-report-publisher.png)
   
6. Repita essas etapas para cada um dos outros medidores no relatório Vendas. 

## <a name="set-the-gauges-for-the-other-reports"></a>Definir os medidores para os outros relatórios

1.  Abra o relatório Transporte, defina o medidor Vendas como um detalhamento para o relatório Vendas e os outros três medidores como detalhamentos de seus respectivos relatórios.

2. Ainda no relatório Transporte, defina **Ênfase** do medidor Transporte como **Ativado**, para contrastar com o restante do relatório.

3. Repita essas etapas para os relatórios Combustível, Armazenamento e Despesas Diversas. 

## <a name="view-the-report-in-the-web-portal"></a>Exibir o relatório no portal da Web

1. Acesse o servidor do relatório do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] e abra um dos relatórios. 

2. Observe que cada um dos medidores tem um ícone de detalhamento no canto superior direito.

    ![Web-Viewer-drillthrough-icon-mobile-report-builder](../../reporting-services/mobile-reports/media/web-viewer-drillthrough-icon-mobile-report-builder.png)

3. Selecione um dos medidores para acessar o relatório filtrado para dados desse medidor.

   ![06-Mobile-Report-Web-Viewer-Transportation](../../reporting-services/mobile-reports/media/06-mobile-report-web-viewer-transportation.png)

### <a name="see-also"></a>Consulte também
    
* [Adicionar parâmetros a um relatório móvel](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)
* [Adicionar o detalhamento de um relatório móvel para outros relatórios móveis ou URLs](../../reporting-services/mobile-reports/add-drillthrough-from-a-mobile-report-to-other-mobile-reports-or-urls.md)




  

