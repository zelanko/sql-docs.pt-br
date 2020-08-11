---
title: Removendo uma extensão de renderização | Microsoft Docs
description: Saiba como remover uma extensão de renderização do Reporting Services para que ela não esteja mais disponível para o serviço de relatório e para o Designer de Relatórios.
ms.date: 03/18/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: extensions
ms.topic: reference
helpviewer_keywords:
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f71fceddd59141516453f9f392f8f913ba20cfad
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529432"
---
# <a name="removing-a-rendering-extension"></a>Removendo uma extensão de renderização
  Para remover uma extensão de renderização do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)], basta remover o elemento **Extension** da extensão de renderização do arquivo rsreportserver.config, localizado em **%ProgramFiles%\Microsoft SQL Server\MSRS10_50.\<Instance Name>\Reporting Services\ReportServer** folder. Se você criou entradas para um Designer de Relatórios, bem como para um servidor de relatório, remova o elemento **Extension** do [Arquivo de configuração RSReportDesigner](../../../reporting-services/report-server/rsreportdesigner-configuration-file.md) também. Após a remoção das informações de configuração, a extensão de renderização não estará mais disponível para o componente.  
  
## <a name="see-also"></a>Consulte Também  
 [Arquivos de configuração do Reporting Services](../../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Implementando uma extensão de renderização](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [Visão geral das extensões de renderização](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [Implementando a interface IRenderingExtension](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [Considerações sobre segurança para extensões](../../../reporting-services/extensions/security-considerations-for-extensions.md)   
 [Implantando uma extensão de renderização](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
  
