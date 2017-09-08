---
title: "Fornecendo argumentos de método de serviço da Web | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
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
- Report Server Web service, methods
- Web service [Reporting Services], methods
- methods [Reporting Services], arguments
- XML Web service [Reporting Services], methods
ms.assetid: f7b9ca05-fc4c-4b30-8e5d-172dd0f4a832
caps.latest.revision: 38
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 761571f88c2321c823dc240cfa9bb3ba75d9414b
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="supplying-web-service-method-arguments"></a>Fornecendo argumentos de método de serviço Web
  Um método do serviço Web do servidor de relatório envia uma solicitação para o serviço em uma determinada URL usando o SOAP por meio do HTTP. O serviço recebe a solicitação, a processa e, em seguida, retorna uma resposta. Essas solicitações e respostas estão no formulário de documentos XML.  
  
## <a name="optional-parameters"></a>Parâmetros opcionais  
 Em alguns casos, um método de serviço Web pode ter parâmetros de entrada opcionais. Mesmo se um parâmetro de entrada para um método de serviço da Web é opcional, você deve ainda incluí-lo e definir o valor do parâmetro **nulo** (**nada** em [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]). Definir um valor de parâmetro **nulo** define o valor do elemento para aquele parâmetro na solicitação SOAP para **nulo**.  
  
 O exemplo a seguir usa o método <xref:ReportService2010.ReportingService2010.CreateFolder%2A> para criar uma nova pasta nomeada como Vendas de Produto na pasta Vendas. Fornecendo um **nulo** valor para as propriedades da pasta, não há propriedades específicas do usuário são fornecidos para a pasta:  
  
```  
// C#  
rs.CreateFolder("Product Sales", "/Sales", null);  
```  
  
## <a name="complex-data-types"></a>Tipos dados complexos  
 A classe principal do serviço Web Servidor de Relatórios é <xref:ReportService2010.ReportingService2010>, que você usa para invocar as operações SOAP ou os métodos Web da classe proxy. Para suportar essa classe e seus métodos, o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] inclui tipos de dados complexos definidos pelo usuário que são específicos para os parâmetros de entrada e saída dos métodos de serviço Web. Esses tipos de dados complexos fazem parte da classe proxy gerado, você pode usar ao desenvolver no [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] ambiente.  
  
 Quando você gera uma classe de proxy, os tipos de dados complexos que são definidos no arquivo WSDL são representados pelas classes de proxy, que incluem propriedades que correspondem a vários elementos SOAP dos tipos de dados complexos. As sequências desses tipos de dados se tornam matrizes de objetos que você pode enumerar através de seu código. Isso elimina a necessidade de trabalhar diretamente com as estruturas de XML enviadas nas mensagens de SOAP. O [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] trata dessa tradução para você.  
  
## <a name="see-also"></a>Consulte também  
 [Criando aplicativos que usam o serviço Web e o .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web servidor de relatório](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Referência técnica &#40; SSRS &#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
