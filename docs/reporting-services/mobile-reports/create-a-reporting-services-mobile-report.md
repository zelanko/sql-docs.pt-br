---
title: "Criar um relat&#243;rio m&#243;vel do Reporting Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e84dc855-aede-4fb4-b721-e6d8787961f4
caps.latest.revision: 10
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 10
---
# Criar um relat&#243;rio m&#243;vel do Reporting Services
Com o [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)], você pode criar rapidamente relatórios móveis do [!INCLUDE[PRODUCT_NAME](../../includes/sscurrent.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)] que se ajustam bem a qualquer tamanho de tela, em uma superfície de design com linhas de grade e colunas ajustáveis e elementos de relatório móvel flexíveis.  
  
Na primeira vez que você cria um relatório móvel, poderá instalar o [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)] no computador local do portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)]. Ou então, você pode instalá-lo do [Centro de Download da Microsoft](http://go.microsoft.com/fwlink/?LinkID=733527). Depois da primeira vez, você poderá iniciá-lo no portal da Web ou localmente.   
    
1. Na barra superior do portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)], selecione **Novo** > **Relatório Móvel**.  
  
   ![PBI_SSMRP_NewMenu](../../reporting-services/mobile-reports/media/pbi-ssmrp-newmenu.png)  
     
2. Na guia **Layout** em [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-short.md)], selecione navegador, medidor, gráfico, mapa ou datagrid e arraste-o para a grade de design.  
  
3. Pegue o canto inferior direito do elemento e arraste-o para o tamanho desejado.  
  
   ![SSMRP_ResizeChart](../../reporting-services/mobile-reports/media/ssmrp-resizechart.png)  
  
   Essa é a grade de design **mestra**, em que você pode criar os elementos desejados no relatório. Posteriormente, você poderá [definir o layout do relatório para um tablet ou telefone](../../reporting-services/mobile-reports/lay-out-a-reporting-services-mobile-report-for-phone-or-tablet.md).     
     
   Em **Propriedades Visuais** abaixo da grade de design, observe as várias propriedades que você pode definir.  
     
4. Selecione a guia **Dados**, no canto superior esquerdo, e você verá que o gráfico já tem dados simulados associados a ele.   
  
   ![SSMRP_SimTable](../../reporting-services/mobile-reports/media/ssmrp-simtable.png)  
  
5. Selecione **Adicionar Dados** no canto superior direito.  
  
6. Selecione **Excel Local** ou **Servidor de Relatórios**.  
  
   >**Dicas**: se você estiver adicionando dados do Excel, verifique se:  
    >* Você [preparou os dados do Excel](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md) para funcionarem em seu relatório móvel.  
    >* Você fechou o arquivo primeiro.  
7. Selecione as planilhas que quer e selecione **Importar**.   
   Você pode adicionar mais de uma planilha de uma pasta de trabalho por vez.  
    
     ![SSMRP_AddExcelData](../../reporting-services/mobile-reports/media/ssmrp-addexceldata.png)  
  
8. Ainda na guia **Dados** na caixa **Propriedades dos Dados**, selecione a tabela e o campo desejados no gráfico.  
  
   ![SSMRP_DataProps](../../reporting-services/mobile-reports/media/ssmrp-dataprops.png)  
  
9. De volta à guia **Layout** da caixa **Propriedades Visuais**, você pode definir propriedades, como **Título**, **Unidade de Tempo**, e **Formato de Número**.  
  
   ![SSMRP_ChartVizProps](../../reporting-services/mobile-reports/media/ssmrp-chartvizprops.png)  
    
10. Selecione **Visualização** no canto superior esquerdo para ver como o relatório está remodelado.  
  
11. Hora de salvar o relatório. Selecione o ícone Salvar no canto superior esquerdo e **Salvar Localmente** ou **Salvar no Servidor**.  
  
   Para salvá-lo em um servidor, você precisa acessar um servidor de relatórios [!INCLUDE[PRODUCT_NAME](../../includes/sscurrent.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion.md)].  
     
   ### Consulte também  
     
-   [Criar e publicar relatórios móveis com o Publicador de Relatórios Móveis do SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)  
-   [Formatar um relatório móvel do Reporting Services para telefone ou tablet](../../reporting-services/mobile-reports/lay-out-a-reporting-services-mobile-report-for-phone-or-tablet.md)  
  
   