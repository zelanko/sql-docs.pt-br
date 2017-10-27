---
title: "Removendo uma extensão de renderização | Microsoft Docs"
ms.custom: 
ms.date: 03/18/2017
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
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
caps.latest.revision: 38
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: ea37cf7ac15504a00aeb0f1379e9d48a71231e1c
ms.contentlocale: pt-br
ms.lasthandoff: 08/12/2017

---
# <a name="removing-a-rendering-extension"></a>Removendo uma extensão de renderização
  Para remover um [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] extensão de renderização, basta remover o **extensão** elemento para a sua extensão de renderização do arquivo rsreportserver. config, localizado em **%ProgramFiles%\Microsoft SQL Server\MSRS10_50.\< Nome da instância > services\reportserver.** pasta. Se você criou entradas para um Designer de relatórios, bem como um servidor de relatório, remova o **extensão** elemento a partir de [RSReportDesigner Configuration File](../../../reporting-services/report-server/rsreportdesigner-configuration-file.md) também. Após a remoção das informações de configuração, a extensão de renderização não estará mais disponível para o componente.  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos de configuração do Reporting Services](../../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Implementando uma extensão de renderização](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [Visão geral de extensões de renderização](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [Implementando a Interface IRenderingExtension](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [Considerações de segurança para extensões](../../../reporting-services/extensions/security-considerations-for-extensions.md)   
 [Implantando uma extensão de renderização](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
  

