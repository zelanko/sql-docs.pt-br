---
title: Usando os cabeçalhos SOAP do Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- SOAP headers [Reporting Services]
- SOAP [Reporting Services], headers
- XML Web service [Reporting Services], SOAP
ms.assetid: 306d2c06-a25a-40f8-8a35-13dd32e8841e
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 3a9e61cc8cc546156d24c209a68c3a523a0f8a29
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56015057"
---
# <a name="using-reporting-services-soap-headers"></a>Usando cabeçalhos SOAP do Reporting Services
  A comunicação com um método de serviço Web que usa o SOAP segue um formato padrão. Parte desse formato são os dados codificados em um documento XML. O documento XML consiste em um elemento raiz **Envelope** que, por sua vez, consiste em um elemento **Body** obrigatório e um elemento **Header** opcional. O elemento **Body** contém os dados específicos à mensagem. O elemento **Header** opcional pode conter informações adicionais que não estão diretamente relacionadas à mensagem específica. Cada elemento filho do elemento **Header** é chamado de cabeçalho SOAP.  
  
 Embora os cabeçalhos SOAP possam conter dados relacionados à mensagem, eles costumam conter informações processadas pela infraestrutura do servidor Web.  
  
 Os serviços Web do Servidor de Relatório definem várias classes para uso no cabeçalho SOAP: <xref:ReportService2005.BatchHeader>, <xref:ReportService2010.ItemNamespaceHeader>, <xref:ReportService2010.ServerInfoHeader>, <xref:ReportService2010.TrustedUserHeader> e <xref:ReportExecution2005.ExecutionHeader>.  
  
## <a name="in-this-section"></a>Nesta seção  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[Métodos de envio em lote](batching-methods.md)|Descreve como processar em lotes várias operações em uma única transação usando o <xref:ReportService2005.BatchHeader>.|  
|[Identificar o estado de execução](identifying-execution-state.md)|Descreve como gerenciar o estado de sessão no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usando o **SessionHeader**.|  
|[Definir o namespace Item para o método GetProperties](setting-the-item-namespace-for-the-getproperties-method.md)|Descreve como recuperar propriedades com base no caminho ou na ID de um item usando o método <xref:ReportService2010.ReportingService2010.GetProperties%2A> e o cabeçalho SOAP <xref:ReportService2010.ItemNamespaceHeader>.|  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](../report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Referência técnica &#40;SSRS&#41;](../technical-reference-ssrs.md)  
  
  
