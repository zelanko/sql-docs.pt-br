---
title: "Propriedades de sistema do servidor de relatório | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- report servers [Reporting Services], properties
- system-specific properties [Reporting Services]
ms.assetid: cd874117-00e5-4ae6-8629-eb9ba9f40478
caps.latest.revision: 55
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: fd0b6d58eb740f9398bd358429f91071b38eefaf
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="reporting-services-properties---report-server-system-properties"></a>Propriedades do Reporting Services - propriedades de sistema do servidor de relatório
  Os seguintes nomes da propriedade do sistema estão reservados. Você não pode criar propriedades definidas pelo usuário com o mesmo nome. Você poderá ler ou modificar muitas dessas propriedades usando os métodos de serviço Web.  
  
## <a name="properties"></a>Propriedades  
  
|Propriedade|Description|  
|--------------|-----------------|  
|SiteName|O nome do site do servidor de relatório exibido na interface do usuário. O valor padrão é **servidor de relatório do Microsoft**. Essa propriedade pode ser uma cadeia de caracteres vazia. O tamanho máximo é de 8.000 caracteres.|  
|SystemSnapshotLimit|O número máximo de instantâneos que são armazenados para um relatório. Os valores válidos são de **-1** até **2**,**147**,**483**,**647**. Se o valor for **-1**, não haverá limite de instantâneo.|  
|SystemReportTimeout|O valor do tempo limite de processamento do relatório padrão, em segundos, para todos os relatórios gerenciados no namespace do servidor de relatório. Esse valor pode ser substituído no nível do relatório. Se a propriedade estiver definida, o servidor de relatórios tentará interromper o processamento de um relatório quando o tempo especificado expirar. Os valores válidos são de **-1** até **2**,**147**,**483**,**647**. Se o valor for **-1**, relatórios no namespace não expirarão durante o processamento. O valor padrão é **1800**.|  
|UseSessionCookies|Indica se o servidor de relatório dever usar cookies de sessão ao se comunicar com navegadores clientes. O valor padrão é **true**.|  
|SessionTimeout|A quantidade de tempo, em segundos, que uma sessão permanece ativa. O valor padrão é **600**.|  
|EnableMyReports|Indica se o recurso Meus Relatórios está habilitado. Um valor **true** indica que o recurso está habilitado.|  
|MyReportsRole|O nome da função usado ao criar políticas de segurança nas pastas de usuário Meus Relatórios. O valor padrão é **My Reports Role**.|  
|EnableExecutionLogging|Indica se o log de execução de relatório está habilitado. O valor padrão é **true**.|  
|ExecutionLogDaysKept|O número de dias para manter informações de execução de relatório no log de execução. Os valores válidos para essa propriedade incluem **0** até **2**,**147**,**483**,**647**. Se o valor for **0** as entradas não serão excluídas da tabela de log de execução. O valor padrão é **60**.|  
|SnapshotCompression|Define como os instantâneos são compactados. O valor padrão é **SQL**. Os valores válidos são os seguintes:<br /><br /> **SQL** = instantâneos são compactados quando armazenados no banco de dados de servidor de relatório. Esse é o comportamento atual.<br /><br /> **None** = Instantâneos não são compactados.<br /><br /> **Todos os** = instantâneos são compactados para todas as opções de armazenamento, que incluem o banco de dados do servidor de relatório ou o sistema de arquivos.|  
|EnableClientPrinting|Determina se o controle ActiveX de RSClientPrint está disponível para download no servidor de relatório. Os valores válidos são **true** e **false**. O valor padrão é **true**. Para obter mais informações sobre configurações adicionais necessárias para esse controle, consulte [Habilitar e desabilitar a impressão do lado do cliente para Reporting Services](../../../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md).|  
|EnableIntegratedSecurity|Determina se a segurança integrada tem suporte para conexões de fonte de dados de relatório. O padrão é **True**. Os valores válidos são os seguintes:<br /><br /> **True** = Integrated security está habilitada.<br /><br /> **False** = Integrated security não está habilitado. As fontes de dados de relatório que são configuradas para usar segurança integrada não serão executadas.|  
|EnableRemoteErrors|Inclui informações de erro externo (por exemplo, informações de erros sobre fontes de dados de relatório) com as mensagens de erro retornadas aos usuários que solicitam relatórios de computadores remotos. Os valores válidos são **true** e **false**. O valor padrão é **false**. Para obter mais informações, consulte [Habilitar erros remotos &#40;Reporting Services&#41;](../../../reporting-services/report-server/enable-remote-errors-reporting-services.md).|  
  
## <a name="see-also"></a>Consulte também  
 <xref:ReportService2010.ReportingService2010.GetSystemProperties%2A>   
 <xref:ReportService2010.ReportingService2010.SetSystemProperties%2A>   
 [Criando aplicativos que usam o serviço Web e o .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web servidor de relatório](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Referência técnica &#40; SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
