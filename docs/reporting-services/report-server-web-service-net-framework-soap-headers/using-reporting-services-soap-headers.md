---
title: "Usando os cabeçalhos SOAP do Reporting Services | Microsoft Docs"
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
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- SOAP headers [Reporting Services]
- SOAP [Reporting Services], headers
- XML Web service [Reporting Services], SOAP
ms.assetid: 306d2c06-a25a-40f8-8a35-13dd32e8841e
caps.latest.revision: "39"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 60f5539eeaf9a529082a2c8db13decaa33d33ee1
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="using-reporting-services-soap-headers"></a>Usando cabeçalhos SOAP do Reporting Services
  A comunicação com um método de serviço Web que usa o SOAP segue um formato padrão. Parte desse formato são os dados codificados em um documento XML. O documento XML consiste em um elemento raiz **Envelope** que, por sua vez, consiste em um elemento **Body** obrigatório e um elemento **Header** opcional. O elemento **Body** contém os dados específicos à mensagem. O elemento **Header** opcional pode conter informações adicionais que não estão diretamente relacionadas à mensagem específica. Cada elemento filho do elemento **Header** é chamado de cabeçalho SOAP.  
  
 Embora os cabeçalhos SOAP possam conter dados relacionados à mensagem, eles costumam conter informações processadas pela infraestrutura do servidor Web.  
  
 Os serviços Web do Servidor de Relatório definem várias classes para uso no cabeçalho SOAP: <xref:ReportService2005.BatchHeader>, <xref:ReportService2010.ItemNamespaceHeader>, <xref:ReportService2010.ServerInfoHeader>, <xref:ReportService2010.TrustedUserHeader> e <xref:ReportExecution2005.ExecutionHeader>.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Métodos de envio em lote](../../reporting-services/report-server-web-service-net-framework-soap-headers/batching-methods.md)|Descreve como processar em lotes várias operações em uma única transação usando o <xref:ReportService2005.BatchHeader>.|  
|[Identificar o estado de execução](../../reporting-services/report-server-web-service-net-framework-soap-headers/identifying-execution-state.md)|Descreve como gerenciar o estado de sessão no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando o **SessionHeader**.|  
|[Definir o namespace Item para o método GetProperties](../../reporting-services/report-server-web-service-net-framework-soap-headers/setting-the-item-namespace-for-the-getproperties-method.md)|Descreve como recuperar propriedades com base no caminho ou na ID de um item usando o método <xref:ReportService2010.ReportingService2010.GetProperties%2A> e o cabeçalho SOAP <xref:ReportService2010.ItemNamespaceHeader>.|  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Referência técnica &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
