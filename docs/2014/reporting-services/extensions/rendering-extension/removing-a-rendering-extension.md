---
title: Removendo uma extensão de renderização | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 5c8f55dd0fa663d5516938e9ca39b5a6dc2caed9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/11/2019
ms.locfileid: "56014618"
---
# <a name="removing-a-rendering-extension"></a>Removendo uma extensão de renderização
  Para remover uma [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] extensão de renderização, basta remover o `Extension` elemento para a sua extensão de renderização do arquivo rsreportserver. config, localizado em **%ProgramFiles%\Microsoft SQL Server\MSRS10_50.\< Nome da instância > \reporting** pasta. Se você criou entradas para um Designer de relatórios, bem como um servidor de relatório, remova os `Extension` elemento o [RSReportDesigner Configuration File](../../report-server/rsreportdesigner-configuration-file.md) também. Após a remoção das informações de configuração, a extensão de renderização não estará mais disponível para o componente.  
  
## <a name="see-also"></a>Consulte também  
 [Arquivos de configuração do Reporting Services](../../report-server/reporting-services-configuration-files.md)   
 [Implementando uma extensão de renderização](implementing-a-rendering-extension.md)   
 [Visão geral das extensões de renderização](rendering-extensions-overview.md)   
 [Implementando a interface IRenderingExtension](implementing-the-irenderingextension-interface.md)   
 [Considerações sobre segurança para extensões](../security-considerations-for-extensions.md)   
 [Implantando uma extensão de renderização](deploying-a-rendering-extension.md)  
  
  
