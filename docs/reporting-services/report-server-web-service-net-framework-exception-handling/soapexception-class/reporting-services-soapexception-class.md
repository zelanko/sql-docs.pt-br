---
title: Reporting Services classe SoapException | Microsoft Docs
ms.custom: 
ms.date: 03/16/2017
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
- exceptions [Reporting Services], SoapException class
- SoapException class
ms.assetid: 2cec49ee-20b1-40eb-a75b-0908d9c05b34
caps.latest.revision: 33
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: e24a518bee7b192505fc93ad26d4345f9d710143
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="reporting-services-soapexception-class"></a>Classe SoapException do Reporting Services
  Você deve tratar de erros específicos do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] que sabe que podem acontecer. Por exemplo, em um aplicativo onde você solicita que o usuário crie uma pasta, pode ser possível que ele tente criar uma pasta que já exista. Como desenvolvedor, você não tem controle sobre o que o usuário digita no nome da pasta e nos campos de caminho do seu aplicativo, mas tem controle sobre o que o usuário experimenta quando alguém incidentalmente tenta criar um item já existente.  
  
 Para facilitar a captura de condições de erro específicas, [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] classifica um código de erro para a exceção e retorna a classificação do erro usando propriedades do **SoapException** classe. Para obter mais informações, consulte "Classe SoapException" o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] documentação do SDK.  
  
 A tabela a seguir lista as propriedades públicas do **SoapException** classe.  
  
|Propriedade pública|Description|  
|---------------------|-----------------|  
|**Ator**|O código que causou a exceção. O valor é a URL para o método do serviço Web.|  
|**Detalhes**|Informações de erro específicas do aplicativo. O valor é definido pelo servidor de relatório e está em formato XML. Para obter mais informações, consulte [propriedade Detail](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/detail-property.md) e [usando a propriedade Detail para manipular erros específicos](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md).|  
|**HelpLink**|Uma URL ou URN para um arquivo de Ajuda associado ao erro. O valor é normalmente definido pelo serviço Web e define uma URL como Ajuda e Suporte do [!INCLUDE[msCoName](../../../includes/msconame-md.md)]. Porque [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] oferece suporte a vários links de ajuda para erros que ocorrem, o servidor de relatório define ajuda vincular informações como parte do **detalhes** propriedade. Para obter mais informações, consulte [elemento HelpLink](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/helplink-element.md).|  
|**Mensagem**|Uma mensagem descritiva e localizada que descreve o erro. Esse texto poderia aparecer na interface do usuário do aplicativo.|  
  
## <a name="see-also"></a>Consulte também  
 [Introdução ao tratamento de exceção no Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Tabela de erros SoapException](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/soapexception-errors-table.md)  
  
  
