---
title: Acessando a API SOAP | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- XML Web service [Reporting Services], WSDL
- Web service [Reporting Services], SOAP
- calling Web service
- SOAP [Reporting Services], accessing
- Report Server Web service, SOAP
- Web service [Reporting Services], WSDL
- WSDL [Reporting Services]
- XML Web service [Reporting Services], SOAP
- Report Server Web service, WSDL
- referencing WSDL
ms.assetid: 63bb870a-4dbf-46bd-8921-78f8ebe5fd75
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 86dd39734b2f2d4fd82f6845f60be588cac2c95b
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/16/2018
ms.locfileid: "51812829"
---
# <a name="accessing-the-soap-api"></a>Acessando a API SOAP
  O serviço Web Serviço de Relatório usa o SOAP sobre HTTP e age como uma interface de comunicações entre programas cliente e o servidor de relatório. O serviço Web oferece dois pontos de extremidade - um para a execução de relatórios e outro para o gerenciamento de relatórios - e consiste em métodos e em um conjunto de objetos de tipo complexo que podem ser usados para o acesso da funcionalidade completa do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Para chamar o serviço, referencie a WSDL (Reporting Services Web Services Description Language).  
  
## <a name="referencing-the-reporting-services-wsdl"></a>Referenciando a WSDL do Reporting Services  
 Para chamar um serviço Web com êxito, você precisa saber como acessá-lo, a que operações ele dá suporte, que parâmetros ele espera e o que ele retorna. A WSDL oferece essas informações em um documento XML que pode ser lido ou processado por um computador.  
  
 Os serviços Web do Servidor de Relatório são expostos em três pontos de extremidade diferentes. O nome do arquivo WSDL é diferente para cada ponto de extremidade. O ponto de extremidade <xref:ReportService2010> contém métodos para gerenciar objetos em um Servidor de Relatório em modo nativo ou integrado do SharePoint. A WSDL para esse ponto de extremidade é acessada por meio do `ReportService2010.asmx?wsdl.`.  
  
> [!NOTE]  
>  Os pontos de extremidade <xref:ReportService2005> e <xref:ReportService2006> foram preteridos no [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]. O ponto de extremidade <xref:ReportService2010> inclui as funcionalidades dos dois pontos de extremidade e contém recursos de gerenciamento adicionais.  
  
-   O ponto de extremidade <xref:ReportExecution2005> permite que os desenvolvedores processem e renderizem relatórios programaticamente em um Servidor de Relatório. A WSDL para esse ponto de extremidade é acessada por meio de `ReportExecution2005.asmx?wsdl`.  
  
 A WSDL pode ser consumida por kits de desenvolvimento que dão suporte a SOAP e a serviços Web, como o SDK do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)].  
  
 O exemplo a seguir mostra o formato da URL para o arquivo WSDL de gerenciamento do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]:  
  
```  
https://server/reportserver/ReportService2010.asmx?wsdl  
```  
  
 A tabela a seguir descreve cada elemento da URL.  
  
|Elemento da URL|Descrição|  
|-----------------|-----------------|  
|*server*|O nome do servidor no qual o servidor de relatório é implantado.|  
|*reportserver*|O nome da pasta que contém o serviço Web XML. Configurado durante a instalação.|  
|*\<endpoint name>.asmx*|O nome do ponto de extremidade do serviço web.|  
  
 Para saber mais sobre o formato WSDL, veja a especificação de WSDL feita pelo W3C (World Wide Web Consortium) em https://www.w3.org/TR/wsdl.  
  
## <a name="see-also"></a>Consulte Também  
 [Criando aplicativos usando o serviço Web e o .NET Framework](../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Serviço Web do Servidor de Relatório](../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
