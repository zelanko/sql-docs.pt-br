---
title: Criar um relatório móvel do Reporting Services | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.suite: pro-bi
ms.topic: conceptual
ms.assetid: e84dc855-aede-4fb4-b721-e6d8787961f4
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 8b8dc94bbea97be9740ae5d455d7103b0da70f3c
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43270398"
---
# <a name="create-a-reporting-services-mobile-report"></a>Criar um relatório móvel do Reporting Services
Com o Publicador de Relatórios Móveis do SQL Server, você pode criar relatórios móveis do SQL Server 2016 Reporting Services com rapidez que se ajustam à qualquer tamanho de tela, em uma superfície de design com colunas e linhas de grade ajustáveis e elementos flexíveis de relatório móvel.  
  
Na primeira vez que você criar um relatório móvel, instale o Publicador de Relatórios Móveis do SQL Server no computador local pelo portal da Web do Reporting Services. Ou então, você pode instalá-lo do [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=733527). Depois da primeira vez, você poderá iniciá-lo no portal da Web ou localmente.   
    
1. Na barra superior do portal da Web do Reporting Services, selecione **Novo** > **Relatório Móvel**.  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
     
2. Na guia **Layout** no Publicador de Relatórios Móveis, selecione um navegador, medidor, gráfico, mapa ou uma grade de dados e arraste-o para a grade de design.  
  
3. Pegue o canto inferior direito do elemento e arraste-o para o tamanho desejado.  
  
   ![SSMRP_ResizeChart](../../reporting-services/mobile-reports/media/ssmrp-resizechart.png)  
  
   Essa é a grade de design **mestra** , em que você pode criar os elementos desejados no relatório. Posteriormente, você poderá [definir o layout do relatório para um tablet ou telefone](../../reporting-services/mobile-reports/lay-out-a-reporting-services-mobile-report-for-phone-or-tablet.md).     
     
   Em **Propriedades Visuais** abaixo da grade de design, observe as várias propriedades que você pode definir.  
     
4. Selecione a guia **Dados** , no canto superior esquerdo, e você verá que o gráfico já tem dados simulados associados a ele.   
  
   ![SSMRP_SimTable](../../reporting-services/mobile-reports/media/ssmrp-simtable.png)  
  
5. Selecione **Adicionar Dados** no canto superior direito.  
  
6. Selecione **Excel Local** ou **Servidor de Relatórios**.  
  
   >**Dicas**: se você estiver adicionando dados do Excel, verifique se:  
    >* Você [preparou os dados do Excel](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md) para funcionarem em seu relatório móvel.  
    >* Você fechou o arquivo primeiro.  
7. Selecione as planilhas que quer e selecione **Importar**.   
   Você pode adicionar mais de uma planilha de uma pasta de trabalho por vez.  
    
     ![SSMRP_AddExcelData](../../reporting-services/mobile-reports/media/ssmrp-addexceldata.png)  
  
8. Ainda na guia **Dados** na caixa **Propriedades dos Dados** , selecione a tabela e o campo desejados no gráfico.  
  
   ![SSMRP_DataProps](../../reporting-services/mobile-reports/media/ssmrp-dataprops.png)  
  
9. De volta à guia **Layout** da caixa **Propriedades Visuais** , você pode definir propriedades, como **Título**, **Unidade de Tempo**, e **Formato de Número**.  
  
   ![SSMRP_ChartVizProps](../../reporting-services/mobile-reports/media/ssmrp-chartvizprops.png)  
    
10. Selecione **Visualização** no canto superior esquerdo para ver como o relatório está remodelado.  
  
11. Hora de salvar o relatório. Selecione o ícone Salvar no canto superior esquerdo e **Salvar Localmente** ou **Salvar no Servidor**.  
  
   Para salvá-lo em um servidor, você precisa ter acesso a um servidor de relatório do SQL Server 2016 Reporting Services.  
     
   ### <a name="see-also"></a>Confira também  
     
-   [Criar e publicar relatórios móveis com o Publicador de Relatórios Móveis do SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-   [Formatar um relatório móvel do Reporting Services para telefone ou tablet](../../reporting-services/mobile-reports/lay-out-a-reporting-services-mobile-report-for-phone-or-tablet.md)  
  
   
