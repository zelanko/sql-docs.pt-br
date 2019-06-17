---
title: Propriedades do sistema do servidor de relatório | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- report servers [Reporting Services], properties
- system-specific properties [Reporting Services]
ms.assetid: cd874117-00e5-4ae6-8629-eb9ba9f40478
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 935e60e0dadb55268fc31d92592d21b0c1df41cb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63260833"
---
# <a name="report-server-system-properties"></a>Propriedades do sistema do servidor de relatório
  Os seguintes nomes da propriedade do sistema estão reservados. Você não pode criar propriedades definidas pelo usuário com o mesmo nome. Você poderá ler ou modificar muitas dessas propriedades usando os métodos de serviço Web.  
  
## <a name="properties"></a>Propriedades  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|SiteName|O nome do site do servidor de relatório exibido na interface do usuário. O valor padrão é `Microsoft Report Server`. Essa propriedade pode ser uma cadeia de caracteres vazia. O tamanho máximo é de 8.000 caracteres.|  
|SystemSnapshotLimit|O número máximo de instantâneos que são armazenados para um relatório. Os valores válidos são de `-1` até `2`,`147`,`483`,`647`. Se o valor for `-1`, não haverá limite de instantâneo.|  
|SystemReportTimeout|O valor do tempo limite de processamento do relatório padrão, em segundos, para todos os relatórios gerenciados no namespace do servidor de relatório. Esse valor pode ser substituído no nível do relatório. Se a propriedade estiver definida, o servidor de relatórios tentará interromper o processamento de um relatório quando o tempo especificado expirar. Os valores válidos são de `-1` até `2`,`147`,`483`,`647`. Se o valor for `-1`, relatórios no namespace não expirarão durante o processamento. O valor padrão é `1800`.|  
|UseSessionCookies|Indica se o servidor de relatório dever usar cookies de sessão ao se comunicar com navegadores clientes. O valor padrão é `true`.|  
|SessionTimeout|A quantidade de tempo, em segundos, que uma sessão permanece ativa. O valor padrão é `600`.|  
|EnableMyReports|Indica se o recurso Meus Relatórios está habilitado. Um valor `true` indica que o recurso está habilitado.|  
|MyReportsRole|O nome da função usado ao criar políticas de segurança nas pastas de usuário Meus Relatórios. O valor padrão é `My Reports Role`.|  
|EnableExecutionLogging|Indica se o log de execução de relatório está habilitado. O valor padrão é `true`.|  
|ExecutionLogDaysKept|O número de dias para manter informações de execução de relatório no log de execução. Os valores válidos para essa propriedade incluem `0` até `2`,`147`,`483`,`647`. Se o valor for `0` as entradas não serão excluídas da tabela de log de execução. O valor padrão é `60`.|  
|SnapshotCompression|Define como os instantâneos são compactados. O valor padrão é `SQL`. Os valores válidos são os seguintes:<br /><br /> `SQL` = Instantâneos são compactados quando armazenados no banco de dados do servidor de relatório. Esse é o comportamento atual.<br /><br /> **None** = Instantâneos não são compactados.<br /><br /> `All` = Instantâneos são compactados para todas as opções de armazenamento que incluem o banco de dados do servidor de relatório ou o sistema de arquivos.|  
|EnableClientPrinting|Determina se o controle ActiveX de RSClientPrint está disponível para download no servidor de relatório. Os valores válidos são `true` e `false`. O valor padrão é `true`. Para obter mais informações sobre configurações adicionais necessárias para esse controle, consulte [Habilitar e desabilitar a impressão do lado do cliente para Reporting Services](../../report-server/enable-and-disable-client-side-printing-for-reporting-services.md).|  
|EnableIntegratedSecurity|Determina se a segurança integrada tem suporte para conexões de fonte de dados de relatório. O padrão é `True`. Os valores válidos são os seguintes:<br /><br /> `True` = a segurança integrada está habilitada.<br /><br /> `False` = a segurança integrada não está habilitada. As fontes de dados de relatório que são configuradas para usar segurança integrada não serão executadas.|  
|EnableRemoteErrors|Inclui informações de erro externo (por exemplo, informações de erros sobre fontes de dados de relatório) com as mensagens de erro retornadas aos usuários que solicitam relatórios de computadores remotos. Os valores válidos são `true` e `false`. O valor padrão é `false`. Para obter mais informações, consulte [Habilitar erros remotos &#40;Reporting Services&#41;](../../report-server/enable-remote-errors-reporting-services.md).|  
  
## <a name="see-also"></a>Consulte também  
 <xref:ReportService2010.ReportingService2010.GetSystemProperties%2A>   
 <xref:ReportService2010.ReportingService2010.SetSystemProperties%2A>   
 [Criando aplicativos usando o serviço Web e o .NET Framework](building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web do Servidor de Relatório](../report-server-web-service.md)   
 [Referência técnica &#40;SSRS&#41;](../../technical-reference-ssrs.md)  
  
  
