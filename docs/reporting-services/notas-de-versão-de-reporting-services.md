---
title: "Visualiza&#231;&#227;o T&#233;cnica dos relat&#243;rios do Power BI no SSRS - Notas de vers&#227;o | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4c2f20d7-a9f9-47e3-8dc3-c544a14457e0
caps.latest.revision: 5
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# Notas de vers&#227;o de Reporting Services
 ||  
|-|  
|**[!INCLUDE[applies](../includes/applies-md.md)]** Visualização Técnica de janeiro de 2017 dos relatórios do Power BI no SQL Server Reporting Services|

Este tópico descreve as limitações e problemas com a Visualização Técnica dos relatórios do Power BI no SQL Server Reporting Services.

- Para ler o que há de novo nesta versão, veja [Novidades no Reporting Service](../reporting-services/novidades-do-sql-server-reporting-services-ssrs.md).

 **Experimente:**    
   -   [![Fazer o download do Centro de downloads da Microsoft](../analysis-services/media/download.png)](https://go.microsoft.com/fwlink/?linkid=839351) Fazer o download da Visualização Técnica dos relatórios do Power BI no SQL Server Reporting Services e do Power BI Desktop (SQL Server Reporting Services), a partir do **[Centro de downloads da Microsoft](https://go.microsoft.com/fwlink/?linkid=839351)**


## <a name="january--2017"></a>Janeiro de 2017

### <a name="report-server"></a>Servidor de relatório

- Agora há suporte para Https. Isso não estava disponível na VM de Visualização Técnica que foi lançada em outubro de 2016. Para obter mais informações, veja [Configurar conexões SSL em um Servidor de Relatórios do Modo Nativo](../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md).
   - O Https é necessário para usar o suplemento de visualizador da Web do PowerPoint expondo os Relatórios de Power BI dentro dele.
- Agora há suporte para expansão. Isso não estava disponível na VM de Visualização Técnica que foi lançada em outubro de 2016. Para saber mais, veja [Configurar uma implantação em expansão do servidor de relatório em modo nativo](../reporting-services/install-windows/configure a native mode report server scale-out deployment.md).

### <a name="power-bi-reports"></a>Relatórios do Power BI

- Os relatórios do Power BI devem ser criados com o Power BI Desktop (SQL Server Reporting Services) para funcionar com o SQL Server Reporting Services. Você pode baixar o Power BI Desktop (SQL Server Reporting Services) do Centro de Avaliação.
- Os relatórios do Power BI só oferecem suporte a conexões ao vivo para o Analysis Services (tabela ou multidimensional).
- Não há suporte para elementos visuais personalizados.
- Não há suporte para elementos visuais do R.