---
title: "Passando configurações de informações de dispositivos para extensões de renderização | Microsoft Docs"
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
- device information settings [Reporting Services]
- Render method
- Report Server Web service, device information settings
- Web service [Reporting Services], device information settings
- XML Web service [Reporting Services], device information settings
- passing device information [Reporting Services]
- rendering extensions [Reporting Services], device information settings
- rendering [Reporting Services], settings
- device information settings [Reporting Services], about device information settings
- extensions [Reporting Services], device information settings
ms.assetid: fe718939-7efe-4c7f-87cb-5f5b09caeff4
caps.latest.revision: 47
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: dfbc65590c676278c89ca2646dae0d347abcd3ee
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="passing-device-information-settings-to-rendering-extensions"></a>Passando configurações de informações de dispositivos para extensões de renderização
  No [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], as configurações de informações de dispositivo são usadas para passar parâmetros de renderização para uma extensão de renderização. As configurações do serviço Web Servidor de Relatórios são passadas como um elemento XML **DeviceInfo** e são processadas pelo servidor de relatório. Como configurações de informações de dispositivo têm valores padrão, elas são consideradas argumentos opcionais no processo de renderização. Porém, você pode usar configurações de informações de dispositivo para personalizar a renderização e substituir os valores padrão que são fornecidos pelo servidor.  
  
 Você pode especificar configurações de informações de dispositivo de diversas formas. Programaticamente, você pode usar o método de renderização. Se você estiver acessando um relatório através da sua URL, poderá especificar informações de dispositivo como parâmetros URL. Você também pode editar as configurações de informações de dispositivo nos arquivos de configuração do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] para especificar parâmetros de renderização globalmente. Para obter mais informações sobre como especificar parâmetros de renderização globalmente, consulte [personalizar os parâmetros de extensão de renderização em rsreportserver. config](../../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md).  
  
## <a name="passing-device-information-using-the-render-method"></a>Passando informações de dispositivo através do método de renderização  
 To pass device information settings to a rendering extension, use the **M:Microsoft.WSSUX.ReportingServicesWebService.RSExecutionService2005.ReportExecutionService.Render(System.String,System.String,System.String@,System.String@,System.String@,Microsoft.WSSUX.ReportingServicesWebService.RSExecutionService2005.Warning[]@,System.String[]@)** method. Por exemplo, a seguinte cadeia de caracteres XML pode ser passada para o <xref:ReportExecution2005.ReportExecutionService.Render%2A> método para criar um fragmento de HTML durante a renderização em HTML.  
  
```  
<DeviceInfo>  
   <HTMLFragment>True</HTMLFragment>  
</DeviceInfo>  
```  
  
 Quando um relatório é renderizado como um fragmento HTML, o conteúdo do relatório está contido dentro de um elemento TABLE sem o uso de um elemento HTML ou BODY. Você pode usar o fragmento de HTML para incorporar o relatório em um documento HTML existente. Para obter mais informações sobre configurações de informações do dispositivo para a saída HTML, consulte [HTML Device Information Settings](../../../reporting-services/html-device-information-settings.md).  
  
## <a name="passing-device-information-using-url-access"></a>Passando informações do dispositivo através do acesso à URL  
 Você também pode passar configurações de informações de dispositivo através do acesso à URL. Configurações de informações de dispositivo são passadas como parâmetros URL. A cadeia de caracteres de acesso à URL a seguir pode ser passada ao servidor de relatório para gerar um relatório renderizado sem a barra de ferramentas do visualizador de HTML.  
  
```  
http://<Server Name>/reportserver?/SampleReports/Sales Order Detail&rs:Command=Render&rs:Format=HTML4.0&rc:Toolbar=False  
```  
  
 Para obter mais informações, consulte [especificar configurações de informações de dispositivo em uma URL](../../../reporting-services/specify-device-information-settings-in-a-url.md).  
  
## <a name="see-also"></a>Consulte também  
 [Configurações de informações de dispositivo para renderização de extensões &#40; Reporting Services &#41;](../../../reporting-services/device-information-settings-for-rendering-extensions-reporting-services.md)   
 [Personalizar parâmetros de extensão de renderização em rsreportserver. config](../../../reporting-services/customize-rendering-extension-parameters-in-rsreportserver-config.md)   
 [Criando aplicativos que usam o serviço Web e o .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)  
  
  
