---
title: rsServerConfigurationError – Erro do Reporting Services | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
helpviewer_keywords:
- rsServerConfigurationError
ms.assetid: 0913afc2-34b4-4713-b570-cfd5718975ac
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 4291245b101799238412115ced8b114de5a551be
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65572139"
---
# <a name="rsserverconfigurationerror---reporting-services-error"></a>rsServerConfigurationError - Erro do Reporting Services
    
## <a name="details"></a>Detalhes  
  
|||  
|-|-|  
|Nome do produto|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|ID do evento|rsServerConfiguration|  
|Origem do evento|Microsoft.ReportingServices.Diagnostics.Utilities.ErrorStrings|  
|Componente|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Texto da mensagem|O servidor de relatório encontrou um erro de configuração.|  
  
## <a name="explanation"></a>Explicação  
 Este é um erro geral que ocorre quando o servidor de relatório ou uma ferramenta de criação de relatório tem definições inválidas de configuração. Normalmente, o erro é acompanhado de uma segunda mensagem que declara a causa real do erro.  
  
 A lista a seguir resume as possíveis causas:  
  
-   O arquivo RSReportServer.config ou RSReportDesigner.config não pode ser encontrado ou lido.  
  
-   Os elementos de XML em um desses arquivos de configuração estão ausentes ou são inválidos.  
  
-   Os valores para um ou mais elementos de XML estão ausentes ou são inválidos.  
  
-   As configurações de registro são inválidas.  
  
## <a name="user-action"></a>Ação do usuário  
 Se o erro começar a ocorrer após você ter editado manualmente um arquivo de configuração, remova as alterações e insira o valor anterior, ou restaure uma versão anterior se possuir um backup.  
  
 Para examinar as informações da mensagem de erro adicionais que acompanha o erro **rsServerConfiguration**, examine os arquivos de log de rastreamento do servidor de relatório, localizados em \Microsoft SQL Server\MSRS12.\<instancename >\Reporting Services\LogFiles. Para obter mais informações, consulte [Fontes e arquivos de log do Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md).  
  
## <a name="internal-only"></a>Somente interno  
  
## <a name="see-also"></a>Consulte Também  
 [Arquivos de configuração do Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
  
