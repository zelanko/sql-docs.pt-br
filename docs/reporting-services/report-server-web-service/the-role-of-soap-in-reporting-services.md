---
title: "A função de SOAP no Reporting Services | Microsoft Docs"
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
- Web service [Reporting Services], SOAP
- SOAP [Reporting Services], role in Reporting Services
- Report Server Web service, SOAP
- XML Web service [Reporting Services], SOAP
ms.assetid: f229c3ef-f2ca-448f-98f1-b8df350b9992
caps.latest.revision: 34
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d860d17f29ca39fc5df422e616805c8bc040185d
ms.contentlocale: pt-br
ms.lasthandoff: 06/13/2017

---
# <a name="the-role-of-soap-in-reporting-services"></a>The Role of SOAP in Reporting Services
  O serviço Web do servidor de relatório usa o sistema de mensagens SOAP (Simple Object Access Protocol) para enviar comandos baseados em texto por meio de uma rede. Esses comandos assumem a forma de texto XML que é enviado por meio da Web usando HTTP. Usando o SOAP como seu protocolo de comunicação, o serviço Web do servidor de relatório permite aplicativos e componentes para trocar dados com o servidor de relatório usando uma infraestrutura largamente aceita e aberta. O padrão de SOAP é definido em www.w3.org/TR/SOAP.  
  
 Qualquer aplicativo cliente pode agir como um cliente de SOAP desde que seja o SOAP-atento e pode enviar solicitações de SOAP. O Gerenciador de Relatórios é um cliente de SOAP. Ele fornece uma interface para o banco de dados do servidor de relatório em que todos os relatórios e conteúdo relacionado a relatório são armazenados. Os usuários finais podem usar o aplicativo para navegar bem como gerenciar relatórios e pastas no namespace de servidor de relatório. O Gerenciador de Relatórios é criado na infraestrutura de serviço Web do servidor de relatório.  
  
 Um servidor de relatório age como um servidor de SOAP, um serviço do SOAP-atento que pode aceitar solicitações de clientes de SOAP e criar respostas apropriadas. O servidor trata as solicitações e envia respostas codificadas novamente para o cliente.  
  
 As mensagens de SOAP no [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] assumem muitas formas diferentes, dependendo do tipo de solicitação feita pelo cliente. O exemplo a seguir representa uma solicitação de cliente de SOAP simples para remover um item do banco de dados do servidor de relatório.  
  
```  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <soap:Body>  
        <DeleteItem xmlns="http://www.microsoft.com/sql/ReportingServer">  
            <item>/Samples/Report1</item>  
        </DeleteItem>  
    </soap:Body>  
</soap:Envelope>  
```  
  
 O SOAP em si requer que as mensagens sejam colocadas em um **Envelope** elemento, com a maior parte da mensagem em uma **corpo** elemento. Nesse exemplo, o corpo contém uma chamada para o método <xref:ReportService2010.ReportingService2010.DeleteItem%2A>, que assume um parâmetro de cadeia de caracteres representando o caminho do item a ser excluído. Você pode criar um [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] classe de proxy de cliente que encapsula todas as operações de SOAP em métodos. O seguinte [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[csprcs](../../includes/csprcs-md.md)] método representa o exemplo SOAP apresentado anteriormente.  
  
```  
public void DeleteItem(string item);  
```  
  
 A resposta do servidor pode se parecer com o seguinte:  
  
```  
<soap:Envelope xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">  
    <soap:Body>  
        <DeleteItemResponse xmlns="http://www.microsoft.com/sql/ReportingServer" />  
    </soap:Body>  
</soap:Envelope>  
```  
  
 O método <xref:ReportService2010.ReportingService2010.DeleteItem%2A> não tem nenhum valor de retorno, portanto, uma resposta vazia é retornada.  
  
## <a name="see-also"></a>Consulte também  
 [Acessando a API SOAP](../../reporting-services/report-server-web-service/accessing-the-soap-api.md)   
 [Gerenciador de Relatórios &#40;Modo Nativo do SSRS&#41;](http://msdn.microsoft.com/library/80949f9d-58f5-48e3-9342-9e9bf4e57896)   
 [Servidor de Relatório do Reporting Services](../../reporting-services/report-server-sharepoint/reporting-services-report-server.md)   
 [Serviço Web servidor de relatório](../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
