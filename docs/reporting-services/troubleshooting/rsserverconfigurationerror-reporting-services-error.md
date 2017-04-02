---
title: "rsServerConfigurationError - Erro do Reporting Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/20/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "rsServerConfigurationError"
ms.assetid: 0913afc2-34b4-4713-b570-cfd5718975ac
caps.latest.revision: 12
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 12
---
# rsServerConfigurationError - Erro do Reporting Services
    
## Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|rsServerConfiguration|  
|Origem do evento|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Texto da mensagem|O servidor de relatório encontrou um erro de configuração.|  
  
## Explicação  
 Este é um erro geral que ocorre quando o servidor de relatório ou uma ferramenta de criação de relatório tem definições inválidas de configuração. Normalmente, o erro é acompanhado de uma segunda mensagem que declara a causa real do erro.  
  
 A lista a seguir resume as possíveis causas:  
  
-   O arquivo RSReportServer.config ou RSReportDesigner.config não pode ser encontrado ou lido.  
  
-   Os elementos de XML em um desses arquivos de configuração estão ausentes ou são inválidos.  
  
-   Os valores para um ou mais elementos de XML estão ausentes ou são inválidos.  
  
-   As configurações de registro são inválidas.  
  
## Ação do usuário  
 Se o erro começar a ocorrer após você ter editado manualmente um arquivo de configuração, remova as alterações e insira o valor anterior, ou restaure uma versão anterior se possuir um backup.  
  
 Para examinar as informações sobre a mensagem de erro adicional que acompanha o erro **rsServerConfiguration**, verifique os arquivos de log de rastreamento do servidor de relatório, localizados em \Microsoft SQL Server\MSRS12.\<nome_da_instância >\Reporting Services\LogFiles. Para obter mais informações, consulte [Fontes e arquivos de log do Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
## Somente interno  
  
## Consulte também  
 [Arquivos de configuração do Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
  