---
title: rsServerConfigurationError – Erro do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- rsServerConfigurationError
ms.assetid: 0913afc2-34b4-4713-b570-cfd5718975ac
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: a0017be7f7ac6117c1512cbaf3e46b662f0a06f0
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56021671"
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
  
 Para examinar as informações da mensagem de erro adicional que acompanha o `rsServerConfiguration` erro, examine os relatório server rastreamento arquivos de log, estão localizados em \Microsoft SQL Server\MSRS12.\< InstanceName > \reporting. Para obter mais informações, consulte [Fontes e arquivos de log do Reporting Services](../report-server/reporting-services-log-files-and-sources.md).  
  
## <a name="internal-only"></a>Somente interno  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos de configuração do Reporting Services](../report-server/reporting-services-configuration-files.md)   
 [Modificar um arquivo de configuração do Reporting Services &#40;RSreportserver.config&#41;](../report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)  
  
  
