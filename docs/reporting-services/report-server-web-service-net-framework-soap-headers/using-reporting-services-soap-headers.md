---
title: "Usando o Reporting Services cabeçalhos SOAP | Microsoft Docs"
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
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- SOAP headers [Reporting Services]
- SOAP [Reporting Services], headers
- XML Web service [Reporting Services], SOAP
ms.assetid: 306d2c06-a25a-40f8-8a35-13dd32e8841e
caps.latest.revision: 39
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 08aec184077b69d05939fe493bf677043beb99d3
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="using-reporting-services-soap-headers"></a>Usando cabeçalhos SOAP do Reporting Services
  A comunicação com um método de serviço Web que usa o SOAP segue um formato padrão. Parte desse formato são os dados codificados em um documento XML. O documento XML consiste em uma raiz **Envelope** elemento, que por sua vez consiste em um arquivo **corpo** elemento e um opcional **cabeçalho** elemento. O **corpo** elemento contém os dados específicos da mensagem. Opcional **cabeçalho** elemento pode conter informações adicionais que não estão diretamente relacionadas à mensagem específica. Cada elemento filho do **cabeçalho** elemento é chamado de um cabeçalho SOAP.  
  
 Embora os cabeçalhos SOAP possam conter dados relacionados à mensagem, eles costumam conter informações processadas pela infraestrutura do servidor Web.  
  
 Os serviços Web do Servidor de Relatório definem várias classes para uso no cabeçalho SOAP: <xref:ReportService2005.BatchHeader>, <xref:ReportService2010.ItemNamespaceHeader>, <xref:ReportService2010.ServerInfoHeader>, <xref:ReportService2010.TrustedUserHeader> e <xref:ReportExecution2005.ExecutionHeader>.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Description|  
|-----------|-----------------|  
|[Métodos de envio em lote](../../reporting-services/report-server-web-service-net-framework-soap-headers/batching-methods.md)|Descreve como processar em lotes várias operações em uma única transação usando o <xref:ReportService2005.BatchHeader>.|  
|[Identificando o estado de execução](../../reporting-services/report-server-web-service-net-framework-soap-headers/identifying-execution-state.md)|Descreve como gerenciar o estado da sessão em [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando **SessionHeader**.|  
|[Definindo o Namespace Item para o método GetProperties](../../reporting-services/report-server-web-service-net-framework-soap-headers/setting-the-item-namespace-for-the-getproperties-method.md)|Descreve como recuperar propriedades com base no caminho ou na ID de um item usando o método <xref:ReportService2010.ReportingService2010.GetProperties%2A> e o cabeçalho SOAP <xref:ReportService2010.ItemNamespaceHeader>.|  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos que usam o serviço Web e o .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Referência técnica &#40; SSRS &#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
