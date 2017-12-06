---
title: "Abrir um relatório móvel com parâmetros de cadeia de consulta específicos | Microsoft Docs"
ms.custom: 
ms.date: 10/25/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4eeb3204-e207-4ac0-aff3-bfc4926e5754
caps.latest.revision: "5"
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: e1432a8e51ce6ecc50f1ed614094bbf2e04d50d7
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="open-a-mobile-report-with-specific-query-string-parameters--reporting-services"></a>Abrir um relatório móvel com parâmetros de cadeia de consulta específicos | Reporting Services
Se você tiver um relatório móvel [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] com parâmetros e uma fonte de dados [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ou [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] , poderá incluir parâmetros de cadeia de consulta na URL do relatório, para que ele seja aberto automaticamente com os valores especificados. 
1.  Crie um [relatório móvel com parâmetros](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md).

2. Abra o relatório no Publicador de Relatórios Móveis e selecione a guia Dados. 

2. Encontre o nome do conjunto de dados na guia, na parte inferior da tabela, e o nome do campo desejado. 
    
    ![mobile-report-publisher-parameter-data-view](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-data-view.png)
    
2.  A sintaxe da URL depende de sua fonte de dados. 

     **Para uma fonte de dados do SQL Server Analysis Services**: compile uma URL com um parâmetro de cadeia de caracteres de consulta neste formato:

    `http://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.<field-name>=<parameter-value>`

    Por exemplo:
    
    `http://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.category=Clothing` 
    
     **Para uma fonte de dados do SQL Server**: o parâmetro de cadeia de caracteres de consulta é praticamente o mesma, mas tem o símbolo @ na frente do nome do campo:

    `http://<servername>/reports/<report-folder-name>/<report-name>?<dataset-name>.@<field-name>=<parameter-value>`

    Por exemplo:
    
      `http://sampleserver/reports/adventureworks-reports/adventureworks-load-on-demand?TimeChartLoD.@category=Clothing` 

    
3.  Essa URL abrirá o relatório no servidor, automaticamente filtrado para o valor de parâmetro especificado.

    ![mobile-report-publisher-parameter-web-portal-view](../../reporting-services/mobile-reports/media/mobile-report-publisher-parameter-web-portal-view.png)

### <a name="see-also"></a>Consulte também

[Adicionar parâmetros a um relatório móvel](../../reporting-services/mobile-reports/add-parameters-to-a-mobile-report-reporting-services.md)

