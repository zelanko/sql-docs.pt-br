---
title: Fornecendo argumentos de método de serviço Web | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- Report Server Web service, methods
- Web service [Reporting Services], methods
- methods [Reporting Services], arguments
- XML Web service [Reporting Services], methods
ms.assetid: f7b9ca05-fc4c-4b30-8e5d-172dd0f4a832
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: ad5251471fe9be594bf0ffb09c13f5f9afc35990
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/31/2020
ms.locfileid: "63128955"
---
# <a name="supplying-web-service-method-arguments"></a>Fornecendo argumentos de método de serviço Web
  Um método do serviço Web do servidor de relatório envia uma solicitação para o serviço em uma determinada URL usando o SOAP por meio do HTTP. O serviço recebe a solicitação, a processa e, em seguida, retorna uma resposta. Essas solicitações e respostas estão no formulário de documentos XML.  
  
## <a name="optional-parameters"></a>Parâmetros opcionais  
 Em alguns casos, um método de serviço Web pode ter parâmetros de entrada opcionais. Mesmo se um parâmetro de entrada de um método de serviço Web for opcional, você deverá incluí-lo e definir o valor do parâmetro como **null** (**Nothing** no [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]). A configuração de um valor de parâmetro como **null** define o valor do elemento com esse parâmetro na solicitação SOAP como **null**.  
  
 O exemplo a seguir usa o método <xref:ReportService2010.ReportingService2010.CreateFolder%2A> para criar uma nova pasta nomeada como Vendas de Produto na pasta Vendas. Ao fornecer um valor **null** para as propriedades da pasta, nenhuma propriedade específica ao usuário será fornecida para a pasta:  
  
```  
// C#  
rs.CreateFolder("Product Sales", "/Sales", null);  
```  
  
## <a name="complex-data-types"></a>Tipos dados complexos  
 A classe principal do serviço Web Servidor de Relatórios é <xref:ReportService2010.ReportingService2010>, que você usa para invocar as operações SOAP ou os métodos Web da classe proxy. Para suportar essa classe e seus métodos, o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] inclui tipos de dados complexos definidos pelo usuário que são específicos para os parâmetros de entrada e saída dos métodos de serviço Web. Esses tipos de dados complexos fazem parte da classe proxy gerada, que você poderá usar quando estiver desenvolvendo soluções no ambiente do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)].  
  
 Quando você gera uma classe de proxy, os tipos de dados complexos que são definidos no arquivo WSDL são representados pelas classes de proxy, que incluem propriedades que correspondem a vários elementos SOAP dos tipos de dados complexos. As sequências desses tipos de dados se tornam matrizes de objetos que você pode enumerar através de seu código. Isso elimina a necessidade de trabalhar diretamente com as estruturas de XML enviadas nas mensagens de SOAP. O [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] trata dessa tradução para você.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web Servidor de Relatórios](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Referência técnica &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
