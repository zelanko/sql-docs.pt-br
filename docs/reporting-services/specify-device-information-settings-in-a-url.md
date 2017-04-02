---
title: "Especificar configura&#231;&#245;es de informa&#231;&#245;es do dispositivo em uma URL | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "configurações de informações de dispositivo [Reporting Services], URLs"
  - "acesso de URL [Reporting Services], configurações de informações de dispositivo"
ms.assetid: cb7f7577-c6a8-4e6f-8e60-5ec0760f29c3
caps.latest.revision: 32
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 32
---
# Especificar configura&#231;&#245;es de informa&#231;&#245;es do dispositivo em uma URL
  As configurações de informações de dispositivo são parâmetros que são passados para uma extensão de renderização. Se você usar os métodos do serviço Web do servidor de relatório do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para renderizar um relatório, um elemento XML **DeviceInfo** será passado como um parâmetro de entrada. Os elementos filho do elemento **DeviceInfo** são específicos para as configurações de informações de dispositivo de extensões de renderização diferentes. Você pode incluir as configurações de informações de dispositivo em uma URL usando a cadeia de caracteres do parâmetro *rc:tag=value*, em que *tag* é o nome do elemento de configurações de informações de dispositivo que estão sendo acessados. Para obter mais informações sobre configurações de informações de dispositivo o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], consulte [Passando configurações de informações de dispositivos para extensões de renderização](../reporting-services/report-server-web-service/net-framework/passing-device-information-settings-to-rendering-extensions.md).  
  
## Exemplo  
 O exemplo a seguir define o formato do relatório especificado para JPEG usando a configuração de informações do dispositivo *OutputFormat* da extensão de renderização de imagem (as quebras de linha foram adicionadas para legibilidade):  
  
```  
http://servername/reportserver?/SampleReports  
/Employee Sales Summary&EmployeeID=38&rs:  
Command=Render&rs:Format=IMAGE&rc:OutputFormat=JPEG  
```  
  
## Consulte também  
 [Acesso à URL &#40;SSRS&#41;](../reporting-services/url-access-ssrs.md)   
 [Referência de parâmetro de acesso de URL](../reporting-services/url-access-parameter-reference.md)  
  
  