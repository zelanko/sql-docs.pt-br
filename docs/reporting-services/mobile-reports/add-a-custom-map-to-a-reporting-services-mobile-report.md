---
title: "Adicionar um mapa personalizado a um relat&#243;rio m&#243;vel do Reporting Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fd259b95-bb58-4eb1-a436-6aa12fc6f5f2
caps.latest.revision: 6
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 6
---
# Adicionar um mapa personalizado a um relat&#243;rio m&#243;vel do Reporting Services
Os mapas personalizados exigem dois arquivos:  
* Um arquivo .SHP para geometrias de forma  
* Um arquivo .DBF para metadados  
  
Leia mais sobre [mapas personalizados nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md).  
  
Armazene os dois arquivos na mesma pasta. Os nomes dos dois arquivos devem corresponder (por exemplo, canada.shp e canada.dbf). Os metadados (arquivos DBF) devem incluir o campo "NOME" com o valor do nome da forma correspondente (chave) a ser usada quando o mapa for populado com dados.   
  
## Carregar um mapa personalizado  
  
1. Na aba **Layout**, escolha um tipo de mapa: **Mapa de Calor de Gradiente**, **Mapa de Calor de Parada de Intervalo** ou **Mapa de Bolha**, arraste-o para a superfície de design e coloque-o no tamanho desejado.  
  
   ![SSMRP_MapsGallery](../../reporting-services/mobile-reports/media/ssmrp-mapsgallery.png)  
  
2. No modo de exibição **layout** > no painel **Propriedades Visuais** > **Mapa**, escolha **Personalizar Mapa a partir do Arquivo**.   
  
   ![SSMRP_SelectCustomMap](../../reporting-services/mobile-reports/media/ssmrp-selectcustommap.png)  
  
3. Na caixa de diálogo **Abrir**, navegue até o local dos arquivos SHP e DBF e selecione os dois.   
  
   ![SSMRP_SelectDBFandSHP](../../reporting-services/mobile-reports/media/ssmrp-selectdbfandshp.png)  
  
## Conectar os dados a um mapa personalizado  
Quando você adiciona primeiro o mapa personalizado ao relatório, o [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] preenche-o com dados de geografia simulada.  
  
![SSMRP_MapsData](../../reporting-services/mobile-reports/media/ssmrp-mapsdata.png)  
  
Exibir dados reais em seu mapa personalizado é o mesmo que exibir dados nos mapas internos. Siga as etapas em [Mapas nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md) para exibir seus dados.  
  
### Consulte também  
- [Mapas personalizados nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/custom-maps-in-reporting-services-mobile-reports.md)  
- [Mapas nos relatórios móveis do Reporting Services](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [Criar e publicar relatórios móveis com o Publicador de Relatórios Móveis do SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  
  
