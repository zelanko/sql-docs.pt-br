---
title: Usando os cabeçalhos SOAP do Reporting Services | Microsoft Docs
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service-net-framework-soap-headers
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- SOAP headers [Reporting Services]
- SOAP [Reporting Services], headers
- XML Web service [Reporting Services], SOAP
ms.assetid: 306d2c06-a25a-40f8-8a35-13dd32e8841e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 99a4ac18003defd2a6b3cffdd4bc1d2955c44816
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "63026007"
---
# <a name="using-reporting-services-soap-headers"></a>Usando cabeçalhos SOAP do Reporting Services
  A comunicação com um método de serviço Web que usa o SOAP segue um formato padrão. Parte desse formato são os dados codificados em um documento XML. O documento XML consiste em um elemento raiz **Envelope** que, por sua vez, consiste em um elemento **Body** obrigatório e um elemento **Header** opcional. O elemento **Body** contém os dados específicos à mensagem. O elemento **Header** opcional pode conter informações adicionais que não estão diretamente relacionadas à mensagem específica. Cada elemento filho do elemento **Header** é chamado de cabeçalho SOAP.  
  
 Embora os cabeçalhos SOAP possam conter dados relacionados à mensagem, eles costumam conter informações processadas pela infraestrutura do servidor Web.  
  
 Os serviços Web do Servidor de Relatório definem várias classes para uso no cabeçalho SOAP: <xref:ReportService2005.BatchHeader>, <xref:ReportService2010.ItemNamespaceHeader>, <xref:ReportService2010.ServerInfoHeader>, <xref:ReportService2010.TrustedUserHeader> e <xref:ReportExecution2005.ExecutionHeader>.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|DESCRIÇÃO|  
|-----------|-----------------|  
|[Métodos de envio em lote](../../reporting-services/report-server-web-service-net-framework-soap-headers/batching-methods.md)|Descreve como processar em lotes várias operações em uma única transação usando o <xref:ReportService2005.BatchHeader>.|  
|[Identificar o estado de execução](../../reporting-services/report-server-web-service-net-framework-soap-headers/identifying-execution-state.md)|Descreve como gerenciar o estado de sessão no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando o **SessionHeader**.|  
|[Definir o namespace Item para o método GetProperties](../../reporting-services/report-server-web-service-net-framework-soap-headers/setting-the-item-namespace-for-the-getproperties-method.md)|Descreve como recuperar propriedades com base no caminho ou na ID de um item usando o método <xref:ReportService2010.ReportingService2010.GetProperties%2A> e o cabeçalho SOAP <xref:ReportService2010.ItemNamespaceHeader>.|  
  
## <a name="see-also"></a>Consulte Também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Referência técnica &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
