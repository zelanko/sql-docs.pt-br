---
title: Propriedade Detail | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: report-server-web-service-net-framework-exception-handling
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- Detail property
- SoapException class
ms.assetid: c1ddaeb6-c540-49fa-b06e-b6359d377ee8
caps.latest.revision: "33"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 19ad36153628f384ce4e552370777f5ab36088af
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2017
---
# <a name="detail-property"></a>Propriedade Detail
  A propriedade **Detail** da classe **SoapException** do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] tem a seguinte estrutura XML:  
  
## <a name="elements"></a>Elementos  
 **Detail**  
 O elemento de alto nível que contém todos os outros elementos de detalhe de erro.  
  
 **ErrorCode**  
 O código de erro específico do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 **HttpStatus**  
 O código de status HTTP.  
  
 **Mensagem**  
 A mensagem de erro e o código de erro atribuídos pelo servidor de relatório.  
  
 **HelpLink**  
 A URL do link de Ajuda para um site no qual poderão ser encontradas informações adicionais sobre o erro. Para obter mais informações, consulte [Elemento HelpLink](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/helplink-element.md).  
  
 **LinkID**  
 A ID atribuída ao link.  
  
 **ProductName**  
 O nome do produto. O valor padrão é **Microsoft SQL Server Reporting Services**.  
  
 **ProductVersion**  
 A versão do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)]. O tamanho máximo é de 15 caracteres. O formato do número da versão deve ser assim: 8.00.0xxx.00.  
  
 **ProductLocaleId**  
 A ID de localidade ou ID de idioma da DLL INTL do aplicativo (por exemplo, 0x41A).  
  
 **OperatingSystem**  
 O sistema operacional em que o [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] está instalado. Os valores válidos incluem **0** para o sistema operacional independente, **1** para o [!INCLUDE[win2kfamily](../../../includes/win2kfamily-md.md)] e **16** para o Windows XP.  
  
 **CountryLocaleId**  
 A ID de localidade ou a ID de idioma do sistema operacional. Por exemplo, o valor para a versão francesa de Windows é 0x040c.  
  
 **MoreInformation**  
 Uma cadeia de caracteres XML que contém exceções aninhadas ocorridas durante a execução do método.  
  
 **Origem**  
 Um elemento filho de **MoreInformation**. A origem do erro.  
  
 **Mensagem**  
 Um elemento filho de **MoreInformation**. A mensagem de erro de uma exceção aninhada. Esse elemento inclui atributos XML para **ErrorCode** e **HelpLink**.  
  
 **Warnings**  
 Uma cadeia de caracteres XML que contém os avisos retornados do processamento de relatório.  
  
## <a name="see-also"></a>Consulte também  
 [Introdução ao tratamento de exceção no Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/introducing-exception-handling-in-reporting-services.md)   
 [Classe SoapException do Reporting Services](../../../reporting-services/report-server-web-service-net-framework-exception-handling/soapexception-class/reporting-services-soapexception-class.md)   
 [Usar a propriedade Detail para manipular erros específicos](../../../reporting-services/report-server-web-service-net-framework-exception-handling/best-practices/using-the-detail-property-to-handle-specific-errors.md)  
  
  
